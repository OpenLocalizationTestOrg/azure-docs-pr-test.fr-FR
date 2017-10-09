---
title: "aaaPerform avancée en personnalisant MES Présélections d’encodage | Documents Microsoft"
description: "Cette rubrique montre comment tooperform avancée en personnalisant les présélections de tâches Media Encoder Standard de codage."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="ccb9d-103">Effectuer un encodage avancé en personnalisant les présélections MES</span><span class="sxs-lookup"><span data-stu-id="ccb9d-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="ccb9d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ccb9d-104">Overview</span></span>

<span data-ttu-id="ccb9d-105">Cette rubrique montre comment toocustomize Media Encoder Standard prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-105">This topic shows how toocustomize Media Encoder Standard presets.</span></span> <span data-ttu-id="ccb9d-106">Hello [encodage avec Media Encoder Standard à l’aide des paramètres prédéfinis personnalisés](media-services-custom-mes-presets-with-dotnet.md) rubrique indique comment toouse .NET toocreate est un encodage de tâches et d’une tâche qui exécute cette tâche.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-106">hello [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how toouse .NET toocreate an encoding task and a job that executes this task.</span></span> <span data-ttu-id="ccb9d-107">Une fois que vous personnalisez une présélection de tâche d’encodage approvisionnement hello Présélections personnalisées toohello.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-107">Once you customize a preset, supply hello custom presets toohello encoding task.</span></span> 

>[!NOTE]
><span data-ttu-id="ccb9d-108">Si vous utilisez une présélection XML, vérifiez qu’ordre de hello toopreserve des éléments, comme indiqué dans les exemples XML ci-dessous (par exemple, KeyFrameInterval doit précéder SceneChangeDetection).</span><span class="sxs-lookup"><span data-stu-id="ccb9d-108">If using an XML preset, make sure toopreserve hello order of elements, as shown in XML samples below (for example, KeyFrameInterval should precede SceneChangeDetection).</span></span>
>

<span data-ttu-id="ccb9d-109">Dans cette rubrique, hello des paramètres prédéfinis personnalisés qui effectuent hello suivant les tâches d’encodage sont illustrées.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-109">In this topic, hello custom presets that perform hello following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="ccb9d-110">Prise en charge des tailles relatives</span><span class="sxs-lookup"><span data-stu-id="ccb9d-110">Support for relative sizes</span></span>

<span data-ttu-id="ccb9d-111">Lors de la génération de miniatures, vous n’avez pas besoin tooalways spécifier la largeur de sortie et la hauteur en pixels.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-111">When generating thumbnails, you do not need tooalways specify output width and height in pixels.</span></span> <span data-ttu-id="ccb9d-112">Vous pouvez les spécifier en pourcentages, dans la plage de hello [% 1, …, 100 %].</span><span class="sxs-lookup"><span data-stu-id="ccb9d-112">You can specify them in percentages, in hello range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="ccb9d-113">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="ccb9d-113">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="ccb9d-114">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="ccb9d-114">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <span data-ttu-id="ccb9d-115"><a id="thumbnails"></a>Génération de miniatures</span><span class="sxs-lookup"><span data-stu-id="ccb9d-115"><a id="thumbnails"></a>Generate thumbnails</span></span>

<span data-ttu-id="ccb9d-116">Cette section montre comment toocustomize une présélection qui génère les miniatures.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-116">This section shows how toocustomize a preset that generates thumbnails.</span></span> <span data-ttu-id="ccb9d-117">Hello présélection définie ci-dessous contient des informations sur la façon dont vous souhaitez que tooencode votre fichier ainsi que les informations nécessaires toogenerate miniatures.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-117">hello preset defined below contains information on how you want tooencode your file as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="ccb9d-118">Vous pouvez prendre l’une des présélections MES hello documentées [cela](media-services-mes-presets-overview.md) section et ajoutez le code qui génère des miniatures.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-118">You can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="ccb9d-119">Hello **SceneChangeDetection** paramètre Bonjour suivant prédéfini ne peut être définie tootrue si vous codez tooa à débit binaire unique vidéo.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-119">hello **SceneChangeDetection** setting in hello following preset can only be set tootrue if you are encoding tooa single  bitrate video.</span></span> <span data-ttu-id="ccb9d-120">Si vous codez débits tooa vidéo et définir **SceneChangeDetection** tootrue, l’encodeur de hello retourne une erreur.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-120">If you are encoding tooa multi-bitrate video and set **SceneChangeDetection** tootrue, hello encoder returns an error.</span></span>  
>
>

<span data-ttu-id="ccb9d-121">Pour plus d’informations sur le schéma, consultez [cette](media-services-mes-schema.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-121">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="ccb9d-122">Assurez-vous que tooreview hello [considérations](#considerations) section.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-122">Make sure tooreview hello [Considerations](#considerations) section.</span></span>

### <span data-ttu-id="ccb9d-123"><a id="json"></a>Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="ccb9d-123"><a id="json"></a>JSON preset</span></span>
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
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
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
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <span data-ttu-id="ccb9d-124"><a id="xml"></a>Présélection XML</span><span class="sxs-lookup"><span data-stu-id="ccb9d-124"><a id="xml"></a>XML preset</span></span>
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
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a><span data-ttu-id="ccb9d-125">Considérations</span><span class="sxs-lookup"><span data-stu-id="ccb9d-125">Considerations</span></span>

<span data-ttu-id="ccb9d-126">Hello suivant considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="ccb9d-126">hello following considerations apply:</span></span>

* <span data-ttu-id="ccb9d-127">Utilisez Hello des horodateurs explicite pour la plage de début/étape suppose que cette source d’entrée hello est 1 minute au moins.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-127">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="ccb9d-128">Les éléments Jpg/Png/BmpImage possèdent les attributs de chaîne Start, Step et Range, qui peuvent être interprétés comme suit :</span><span class="sxs-lookup"><span data-stu-id="ccb9d-128">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="ccb9d-129">Entiers non négatifs : nombre d’images, par exemple "Start": "120",</span><span class="sxs-lookup"><span data-stu-id="ccb9d-129">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="ccb9d-130">Durée toosource relatif si exprimée sous la forme %-suivi du suffixe, par exemple « Start » : « 15 % », ou</span><span class="sxs-lookup"><span data-stu-id="ccb9d-130">Relative toosource duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="ccb9d-131">Horodatage, s’il est exprimé au format</span><span class="sxs-lookup"><span data-stu-id="ccb9d-131">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="ccb9d-132">HH:MM:SS, par exemple « Start » : « 00:01:00 »</span><span class="sxs-lookup"><span data-stu-id="ccb9d-132">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="ccb9d-133">Vous pouvez combiner et apparier les notations à votre guise.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-133">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="ccb9d-134">En outre, début prend également en charge une Macro spéciale : {meilleures}, qui tente de toodetermine hello premier « intéressantes » frame de contenu de hello Remarque : (étape et la plage sont ignorés lorsque le démarrage est défini trop {meilleures})</span><span class="sxs-lookup"><span data-stu-id="ccb9d-134">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="ccb9d-135">La configuration par défaut est « Start:{Best} ».</span><span class="sxs-lookup"><span data-stu-id="ccb9d-135">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="ccb9d-136">Format de sortie doit toobe explicitement fourni pour chaque format d’Image : Jpg/Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-136">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="ccb9d-137">Le cas échéant, MES correspond JpgVideo tooJpgFormat et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-137">When present, MES matches JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="ccb9d-138">OutputFormat introduit une nouvelle Macro spécifique codec d’image : {Index}, laquelle doit toobe présent (une fois et une seule fois) pour les formats de sortie d’image.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-138">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <span data-ttu-id="ccb9d-139"><a id="trim_video"></a>Rognage d’une vidéo (extrait)</span><span class="sxs-lookup"><span data-stu-id="ccb9d-139"><a id="trim_video"></a>Trim a video (clipping)</span></span>
<span data-ttu-id="ccb9d-140">Cette section aborde les modification encodeur de hello prédéfinit tooclip ou rogner la vidéo d’entrée de hello où hello entrée est un fichier de ce que l'on appelle mezzanine ou à la demande.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-140">This section talks about modifying hello encoder presets tooclip or trim hello input video where hello input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="ccb9d-141">Hello encodeur peut également être utilisé tooclip ou supprimer un élément multimédia, qui est capturé ou à partir d’un flux en direct : hello détails de ce sont disponibles dans [ce billet de blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="ccb9d-141">hello encoder can also be used tooclip or trim an asset, which is captured or archived from a live stream – hello details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="ccb9d-142">tootrim vos vidéos, vous pouvez effectuer les présélections MES hello documentées [cela](media-services-mes-presets-overview.md) section et modifier hello **Sources** élément (comme indiqué ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="ccb9d-142">tootrim your videos, you can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and modify hello **Sources** element (as shown below).</span></span> <span data-ttu-id="ccb9d-143">valeur de Hello de StartTime doit toomatch hello des horodateurs absolu de la vidéo d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-143">hello value of StartTime needs toomatch hello absolute timestamps of hello input video.</span></span> <span data-ttu-id="ccb9d-144">Par exemple, si hello du premier frame de la vidéo d’entrée de hello a un horodateur de 12:00:10.000, StartTime doit être au moins 12:00:10.000 et supérieur.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-144">For example, if hello first frame of hello input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="ccb9d-145">Dans l’exemple hello ci-dessous, nous supposons qu’entrée hello vidéo a un horodateur de début égale à zéro.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-145">In hello example below, we assume that hello input video has a starting timestamp of zero.</span></span> <span data-ttu-id="ccb9d-146">**Sources** doivent être placés au début de hello hello prédéfini.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-146">**Sources** should be placed at hello beginning of hello preset.</span></span>

### <span data-ttu-id="ccb9d-147"><a id="json"></a>Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="ccb9d-147"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="xml-preset"></a><span data-ttu-id="ccb9d-148">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="ccb9d-148">XML preset</span></span>
<span data-ttu-id="ccb9d-149">tootrim vos vidéos, vous pouvez effectuer les présélections MES hello documentées [ici](media-services-mes-presets-overview.md) et modifier hello **Sources** élément (comme indiqué ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="ccb9d-149">tootrim your videos, you can take any of hello MES presets documented [here](media-services-mes-presets-overview.md) and modify hello **Sources** element (as shown below).</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
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
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="ccb9d-150"><a id="overlay"></a>Création d’une superposition</span><span class="sxs-lookup"><span data-stu-id="ccb9d-150"><a id="overlay"></a>Create an overlay</span></span>

<span data-ttu-id="ccb9d-151">Hello Media Encoder Standard vous permet de toooverlay une image sur une vidéo existante.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-151">hello Media Encoder Standard allows you toooverlay an image onto an existing video.</span></span> <span data-ttu-id="ccb9d-152">Actuellement, hello suivant les formats est pris en charge : png, jpg, gif et bmp.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-152">Currently, hello following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="ccb9d-153">Bonjour présélection définie ci-dessous est un exemple de base d’une superposition vidéo.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-153">hello preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="ccb9d-154">En outre toodefining un fichier prédéfini, vous avez également toolet Media Services connaître le fichier d’élément multimédia de hello est l’image de superposition hello et le fichier est hello source vidéo sur lequel vous souhaitez l’image de hello toooverlay.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-154">In addition toodefining a preset file, you also have toolet Media Services know which file in hello asset is hello overlay image and which file is hello source video onto which you want toooverlay hello image.</span></span> <span data-ttu-id="ccb9d-155">fichier vidéo de Hello a toobe hello **principal** fichier.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-155">hello video file has toobe hello **primary** file.</span></span>

<span data-ttu-id="ccb9d-156">Si vous utilisez .NET, ajoutez hello suivant deux fonctions toohello .NET exemple défini dans [cela](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) rubrique.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-156">If you are using .NET, add hello following two functions toohello .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="ccb9d-157">Hello **UploadMediaFilesFromFolder** fonction télécharge les fichiers à partir d’un dossier (par exemple, BigBuckBunny.mp4 et Image001.png) et jeux hello fichier toobe hello principal fichier mp4 dans un élément multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-157">hello **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets hello mp4 file toobe hello primary file in hello asset.</span></span> <span data-ttu-id="ccb9d-158">Hello **EncodeWithOverlay** fonction utilise hello prédéfini fichier personnalisé qui a été passé à tooit (par exemple, hello prédéfini qui suit) toocreate hello tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-158">hello **EncodeWithOverlay** function uses hello custom preset file that was passed tooit (for example, hello preset that follows) toocreate hello encoding task.</span></span>


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> <span data-ttu-id="ccb9d-159">Limitations actuelles :</span><span class="sxs-lookup"><span data-stu-id="ccb9d-159">Current limitations:</span></span>
>
> <span data-ttu-id="ccb9d-160">paramètre d’opacité superposition Hello n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-160">hello overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="ccb9d-161">Votre fichier vidéo source et le fichier d’image de superposition hello ont toobe dans hello même actif et hello fichier vidéo besoins toobe ensemble en tant que fichier primaire de hello dans cet élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-161">Your source video file and hello overlay image file have toobe in hello same asset, and hello video file needs toobe set as hello primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="ccb9d-162">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="ccb9d-162">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a><span data-ttu-id="ccb9d-163">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="ccb9d-163">XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <span data-ttu-id="ccb9d-164"><a id="silent_audio"></a>Insertion d’une piste audio en mode silencieux lorsque l’entrée ne produit pas de son</span><span class="sxs-lookup"><span data-stu-id="ccb9d-164"><a id="silent_audio"></a>Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="ccb9d-165">Par défaut, si vous envoyez un encodeur toohello d’entrée qui contient uniquement, audio et vidéo aucun, hello élément multimédia de sortie contient des fichiers qui contiennent des données vidéo uniquement.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-165">By default, if you send an input toohello encoder that contains only video, and no audio, then hello output asset contains files that contain only video data.</span></span> <span data-ttu-id="ccb9d-166">Certains lecteurs ne pourront peut-être toohandle ce flux de sortie.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-166">Some players may not be able toohandle such output streams.</span></span> <span data-ttu-id="ccb9d-167">Vous pouvez utiliser cette tooadd d’encodeur de paramètre tooforce hello une sortie toohello de piste audio en mode silencieux dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-167">You can use this setting tooforce hello encoder tooadd a silent audio track toohello output in that scenario.</span></span>

<span data-ttu-id="ccb9d-168">tooforce hello encodeur tooproduce un élément multimédia contenant une piste audio en mode silencieux lors de l’entrée ne contient aucune donnée audio, spécifier la valeur de « InsertSilenceIfNoAudio » hello.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-168">tooforce hello encoder tooproduce an asset that contains a silent audio track when input has no audio, specify hello "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="ccb9d-169">Vous pouvez effectuer les hello MES Présélections documentées dans [cela](media-services-mes-presets-overview.md) section et rendre hello après modification :</span><span class="sxs-lookup"><span data-stu-id="ccb9d-169">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="ccb9d-170">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="ccb9d-170">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="ccb9d-171">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="ccb9d-171">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <span data-ttu-id="ccb9d-172"><a id="deinterlacing"></a>Désactiver le désentrelacement automatique</span><span class="sxs-lookup"><span data-stu-id="ccb9d-172"><a id="deinterlacing"></a>Disable auto de-interlacing</span></span>
<span data-ttu-id="ccb9d-173">Les clients ne doivent toodo rien si elles comme hello entrelacement toobe contenu automatiquement désactivé entrelacée.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-173">Customers don’t need toodo anything if they like hello interlace contents toobe automatically de-interlaced.</span></span> <span data-ttu-id="ccb9d-174">Lorsque hello automatique désentrelacement est sur hello (par défaut) MES hello détection d’images entrelacées automatique et uniquement, déduplication interlaces frames marqués comme entrelacé.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-174">When hello auto de-interlacing is on (default) hello MES does hello auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="ccb9d-175">Vous pouvez désactiver automatiquement hello désentrelacement.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-175">You can turn hello auto de-interlacing off.</span></span> <span data-ttu-id="ccb9d-176">Cette option n’est pas recommandée.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-176">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="ccb9d-177">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="ccb9d-177">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="ccb9d-178">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="ccb9d-178">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <span data-ttu-id="ccb9d-179"><a id="audio_only"></a>Présélections audio uniquement</span><span class="sxs-lookup"><span data-stu-id="ccb9d-179"><a id="audio_only"></a>Audio-only presets</span></span>
<span data-ttu-id="ccb9d-180">Cette section présente deux présélections MES audio uniquement : Audio AAC et Bonne qualité audio AAC.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-180">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="ccb9d-181">Audio AAC</span><span class="sxs-lookup"><span data-stu-id="ccb9d-181">AAC Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a><span data-ttu-id="ccb9d-182">Bonne qualité audio AAC</span><span class="sxs-lookup"><span data-stu-id="ccb9d-182">AAC Good Quality Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="ccb9d-183"><a id="concatenate"></a>Concaténation de deux fichiers vidéo ou plus</span><span class="sxs-lookup"><span data-stu-id="ccb9d-183"><a id="concatenate"></a>Concatenate two or more video files</span></span>

<span data-ttu-id="ccb9d-184">Hello exemple suivant illustre comment vous pouvez générer une présélection tooconcatenate deux ou plusieurs fichiers vidéos.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-184">hello following example illustrates how you can generate a preset tooconcatenate two or more video files.</span></span> <span data-ttu-id="ccb9d-185">scénario le plus courant Hello est lorsque vous souhaitez tooadd un en-tête ou une vidéo principale toohello de code de fin.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-185">hello most common scenario is when you want tooadd a header or a trailer toohello main video.</span></span> <span data-ttu-id="ccb9d-186">Hello prévu est lorsque les fichiers vidéo hello en cours de modification ensemble partagent des propriétés (résolution, fréquence d’images, nombre de pistes audio, etc.).</span><span class="sxs-lookup"><span data-stu-id="ccb9d-186">hello intended use is when hello video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="ccb9d-187">Vous devez prendre soin pas toomix vidéos de fréquences d’images différent ou avec le même nombre de pistes audio.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-187">You should take care not toomix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="ccb9d-188">Hello conception actuelle de la fonctionnalité de concaténation hello attend que hello entrée clips vidéo sont cohérentes en termes de résolution, etc. fréquence d’images.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-188">hello current design of hello concatenation feature expects that hello input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="ccb9d-189">Conditions requises et éléments à prendre en compte</span><span class="sxs-lookup"><span data-stu-id="ccb9d-189">Requirements and considerations</span></span>

* <span data-ttu-id="ccb9d-190">Les vidéos d'entrée ne doivent avoir qu'une seule piste audio.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-190">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="ccb9d-191">Entrée vidéos doivent tous avoir hello même fréquence d’images.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-191">Input videos should all have hello same frame rate.</span></span>
* <span data-ttu-id="ccb9d-192">Vous devez télécharger vos vidéos dans des éléments multimédias séparés et définir les vidéos hello comme fichier principal de hello dans chaque élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-192">You must upload your videos into separate assets and set hello videos as hello primary file in each asset.</span></span>
* <span data-ttu-id="ccb9d-193">Vous devez la durée de hello tooknow des vidéos.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-193">You need tooknow hello duration of your videos.</span></span>
* <span data-ttu-id="ccb9d-194">Hello prédéfinis exemples ci-dessous suppose que toutes les vidéos d’entrée hello démarrer avec un horodatage égal à zéro.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-194">hello preset examples below assumes that all hello input videos start with a timestamp of zero.</span></span> <span data-ttu-id="ccb9d-195">Vous devez les valeurs StartTime toomodify hello si les vidéos hello ont cachet temporel de départ différentes, comme c’est généralement hello cas avec des archives en direct.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-195">You need toomodify hello StartTime values if hello videos have different starting timestamp, as is typically hello case with live archives.</span></span>
* <span data-ttu-id="ccb9d-196">Hello présélection JSON, les références explicites toohello AssetID valeurs d’éléments multimédias en entrée hello.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-196">hello JSON preset makes explicit references toohello AssetID values of hello input assets.</span></span>
* <span data-ttu-id="ccb9d-197">exemple de code Hello suppose que hello que JSON prédéfini a été enregistré tooa fichier local, tel que « C:\supportFiles\preset.json ».</span><span class="sxs-lookup"><span data-stu-id="ccb9d-197">hello sample code assumes that hello JSON preset has been saved tooa local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="ccb9d-198">Il suppose également que les deux composants ont été créés en téléchargeant des fichiers vidéos deux, et connaître les valeurs résultantes AssetID hello.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-198">It also assumes that two assets have been created by uploading two video files, and that you know hello resultant AssetID values.</span></span>
* <span data-ttu-id="ccb9d-199">Hello extrait de code et JSON présélection montre un exemple de la concaténation de deux fichiers vidéos.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-199">hello code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="ccb9d-200">Vous pouvez l’étendre toomore que deux vidéos par :</span><span class="sxs-lookup"><span data-stu-id="ccb9d-200">You can extend it toomore than two videos by:</span></span>

  1. <span data-ttu-id="ccb9d-201">Tâche de l’appel. InputAssets.Add() à plusieurs reprises tooadd plus de vidéos, dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-201">Calling task.InputAssets.Add() repeatedly tooadd more videos, in order.</span></span>
  2. <span data-ttu-id="ccb9d-202">Rendre correspondant modifie élément toohello « Sources » Bonjour JSON, en ajoutant des entrées de plus, Bonjour même ordre.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-202">Making corresponding edits toohello "Sources" element in hello JSON, by adding more entries, in hello same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="ccb9d-203">Code .NET</span><span class="sxs-lookup"><span data-stu-id="ccb9d-203">.NET code</span></span>

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a><span data-ttu-id="ccb9d-204">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="ccb9d-204">JSON preset</span></span>

<span data-ttu-id="ccb9d-205">Mettre à jour votre paramètre prédéfini avec les ID des ressources hello que vous souhaitez tooconcatenate et avec le segment du moment opportun hello pour chaque vidéo.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-205">Update your custom preset with ids of hello assets that you want tooconcatenate, and with hello appropriate time segment for each video.</span></span>

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
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
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="ccb9d-206"><a id="crop"></a>Rogner des vidéos avec l’encodeur multimédia standard</span><span class="sxs-lookup"><span data-stu-id="ccb9d-206"><a id="crop"></a>Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="ccb9d-207">Consultez hello [rogner vidéos avec Media Encoder Standard](media-services-crop-video.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-207">See hello [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <span data-ttu-id="ccb9d-208"><a id="no_video"></a>Insertion d’une piste vidéo lorsque l’entrée ne comporte aucune vidéo</span><span class="sxs-lookup"><span data-stu-id="ccb9d-208"><a id="no_video"></a>Insert a video track when input has no video</span></span>

<span data-ttu-id="ccb9d-209">Par défaut, si vous envoyez un encodeur toohello d’entrée qui contient uniquement des données audio et aucune vidéo, hello élément multimédia de sortie contient des fichiers qui contiennent des données audio uniquement.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-209">By default, if you send an input toohello encoder that contains only audio, and no video, then hello output asset contains files that contain only audio data.</span></span> <span data-ttu-id="ccb9d-210">Certains lecteurs, y compris Azure Media Player (consultez [cela](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) ne peut pas être en mesure de toohandle ces flux de données.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-210">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able toohandle such streams.</span></span> <span data-ttu-id="ccb9d-211">Vous pouvez utiliser cette tooadd d’encodeur paramètre tooforce hello une sortie de toohello monochrome piste vidéo dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-211">You can use this setting tooforce hello encoder tooadd a monochrome video track toohello output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="ccb9d-212">Forcer le hello encodeur tooinsert une piste vidéo sortie augmente la taille hello Hello Asset de sortie et hello ainsi les coûts pour hello tâche de codage.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-212">Forcing hello encoder tooinsert an output video track increases hello size of hello output Asset, and thereby hello cost incurred for hello encoding Task.</span></span> <span data-ttu-id="ccb9d-213">Vous devez exécuter des tests tooverify cette augmentation résultante a uniquement un faible impact sur votre facture mensuelle.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-213">You should run tests tooverify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a><span data-ttu-id="ccb9d-214">Insertion de vidéo avec uniquement le débit de la plus basse hello</span><span class="sxs-lookup"><span data-stu-id="ccb9d-214">Inserting video at only hello lowest bitrate</span></span>

<span data-ttu-id="ccb9d-215">Supposons que vous utilisez un encodage de vitesse de transmission plusieurs prédéfini tel que [« H264 plusieurs débits binaires 720p «](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode l’intégralité de votre entrée de catalogue pour la diffusion en continu, qui contient un mélange de fichiers vidéos et audio uniquement.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-215">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="ccb9d-216">Dans ce scénario, lorsque hello entrée ne comporte aucune vidéo, vous souhaiterez tooforce hello encodeur tooinsert un monochrome vidéo suivre à simplement hello plus faible vitesse de transmission, sous la forme d’opposition tooinserting vidéo à chaque vitesse de transmission de sortie.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-216">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at just hello lowest bitrate, as opposed tooinserting video at every output bitrate.</span></span> <span data-ttu-id="ccb9d-217">tooachieve, vous devez toouse hello **InsertBlackIfNoVideoBottomLayerOnly** indicateur.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-217">tooachieve this, you need toouse hello **InsertBlackIfNoVideoBottomLayerOnly** flag.</span></span>

<span data-ttu-id="ccb9d-218">Vous pouvez effectuer les hello MES Présélections documentées dans [cela](media-services-mes-presets-overview.md) section et rendre hello après modification :</span><span class="sxs-lookup"><span data-stu-id="ccb9d-218">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="ccb9d-219">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="ccb9d-219">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="ccb9d-220">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="ccb9d-220">XML preset</span></span>

<span data-ttu-id="ccb9d-221">Lors de l’utilisation de XML, utilisez la Condition = « InsertBlackIfNoVideoBottomLayerOnly » comme un attribut de toohello **H264Video** élément et la Condition = « InsertSilenceIfNoAudio » en tant qu’attribut trop**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-221">When using XML, use Condition="InsertBlackIfNoVideoBottomLayerOnly" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="ccb9d-222">Insertion de vidéo à tous les débits binaires de sortie</span><span class="sxs-lookup"><span data-stu-id="ccb9d-222">Inserting video at all output bitrates</span></span>
<span data-ttu-id="ccb9d-223">Supposons que vous utilisez un encodage de vitesse de transmission plusieurs prédéfini tel que [« H264 plusieurs débits binaires 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode l’intégralité de votre entrée de catalogue pour la diffusion en continu, qui contient un mélange de fichiers vidéos et audio uniquement.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-223">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="ccb9d-224">Dans ce scénario, lorsque hello entrée ne comporte aucune vidéo, vous souhaiterez tooforce hello encodeur tooinsert suivre d’une vidéo monochrome à tous les débits binaires de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-224">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at all hello output bitrates.</span></span> <span data-ttu-id="ccb9d-225">Cela garantit que votre sortie actifs sont tous homogènes avec toonumber en ce qui concerne des pistes vidéo et des pistes audio.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-225">This ensures that your output Assets are all homogenous with respect toonumber of video tracks and audio tracks.</span></span> <span data-ttu-id="ccb9d-226">tooachieve, vous devez toospecify hello indicateur de « InsertBlackIfNoVideo ».</span><span class="sxs-lookup"><span data-stu-id="ccb9d-226">tooachieve this, you need toospecify hello "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="ccb9d-227">Vous pouvez effectuer les hello MES Présélections documentées dans [cela](media-services-mes-presets-overview.md) section et rendre hello après modification :</span><span class="sxs-lookup"><span data-stu-id="ccb9d-227">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="ccb9d-228">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="ccb9d-228">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="ccb9d-229">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="ccb9d-229">XML preset</span></span>

<span data-ttu-id="ccb9d-230">Lors de l’utilisation de XML, utilisez la Condition = « InsertBlackIfNoVideo » comme un attribut de toohello **H264Video** élément et la Condition = « InsertSilenceIfNoAudio » en tant qu’attribut trop**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-230">When using XML, use Condition="InsertBlackIfNoVideo" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <span data-ttu-id="ccb9d-231"><a id="rotate_video"></a>Faire pivoter une vidéo</span><span class="sxs-lookup"><span data-stu-id="ccb9d-231"><a id="rotate_video"></a>Rotate a video</span></span>
<span data-ttu-id="ccb9d-232">Hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) prend en charge de la rotation par les angles de 0/90/180/270.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-232">hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="ccb9d-233">comportement par défaut de Hello est « Auto », où il tente de métadonnées de rotation toodetect hello dans le fichier vidéo entrant hello et compensation.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-233">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming video file and compensate for it.</span></span> <span data-ttu-id="ccb9d-234">Suivants de hello **Sources** tooone élément des présélections hello défini dans [cela](media-services-mes-presets-overview.md) section :</span><span class="sxs-lookup"><span data-stu-id="ccb9d-234">Include hello following **Sources** element tooone of hello presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="ccb9d-235">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="ccb9d-235">JSON preset</span></span>
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a><span data-ttu-id="ccb9d-236">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="ccb9d-236">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="ccb9d-237">Consultez également [cela](media-services-mes-schema.md#PreserveResolutionAfterRotation) rubrique pour plus d’informations sur comment encoder de hello interprète les paramètres de largeur et hauteur hello Bonjour prédéfini, lorsque la compensation de rotation est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-237">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how hello encoder interprets hello Width and Height settings in hello preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="ccb9d-238">Vous pouvez utiliser hello la valeur « 0 » tooindicate toohello encodeur tooignore rotation métadonnées, le cas échéant, dans la vidéo d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="ccb9d-238">You can use hello value "0" tooindicate toohello encoder tooignore rotation metadata, if present, in hello input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ccb9d-239">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="ccb9d-239">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ccb9d-240">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="ccb9d-240">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="ccb9d-241">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ccb9d-241">See Also</span></span>
[<span data-ttu-id="ccb9d-242">Vue d’ensemble de l’encodage de Media Services</span><span class="sxs-lookup"><span data-stu-id="ccb9d-242">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
