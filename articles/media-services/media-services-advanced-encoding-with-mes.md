---
title: "Effectuer un encodage avancé en personnalisant les présélections MES | Microsoft Docs"
description: "Cette rubrique explique comment effectuer un encodage avancé en personnalisant les présélections de tâches Media Encoder Standard."
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
ms.openlocfilehash: 8de3bdd45261c84a0e1bb90f1c58863ad740dd5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="c3625-103">Effectuer un encodage avancé en personnalisant les présélections MES</span><span class="sxs-lookup"><span data-stu-id="c3625-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="c3625-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c3625-104">Overview</span></span>

<span data-ttu-id="c3625-105">Cette rubrique montre comment personnaliser des présélections Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="c3625-105">This topic shows how to customize Media Encoder Standard presets.</span></span> <span data-ttu-id="c3625-106">La rubrique [Encodage avec Media Encoder Standard à l’aide de présélections personnalisées](media-services-custom-mes-presets-with-dotnet.md) explique comment utiliser .NET pour créer une tâche de codage et une tâche qui exécute cette tâche.</span><span class="sxs-lookup"><span data-stu-id="c3625-106">The [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how to use .NET to create an encoding task and a job that executes this task.</span></span> <span data-ttu-id="c3625-107">Une fois que vous avez personnalisé une présélection, fournissez les présélections personnalisées pour la tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="c3625-107">Once you customize a preset, supply the custom presets to the encoding task.</span></span> 

>[!NOTE]
><span data-ttu-id="c3625-108">Si vous utilisez une présélection XML, veillez à conserver l’ordre des éléments, comme indiqué dans les exemples XML ci-dessous (par exemple, KeyFrameInterval doit précéder SceneChangeDetection).</span><span class="sxs-lookup"><span data-stu-id="c3625-108">If using an XML preset, make sure to preserve the order of elements, as shown in XML samples below (for example, KeyFrameInterval should precede SceneChangeDetection).</span></span>
>

<span data-ttu-id="c3625-109">Cette rubrique présente les présélections personnalisées qui exécutent les tâches d’encodage suivantes.</span><span class="sxs-lookup"><span data-stu-id="c3625-109">In this topic, the custom presets that perform the following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="c3625-110">Prise en charge des tailles relatives</span><span class="sxs-lookup"><span data-stu-id="c3625-110">Support for relative sizes</span></span>

<span data-ttu-id="c3625-111">Lors de la génération de miniatures, il est inutile de toujours spécifier la largeur et la hauteur de la sortie en pixels.</span><span class="sxs-lookup"><span data-stu-id="c3625-111">When generating thumbnails, you do not need to always specify output width and height in pixels.</span></span> <span data-ttu-id="c3625-112">Vous pouvez les spécifier en pourcentages, dans la plage [1 %,..., 100 %].</span><span class="sxs-lookup"><span data-stu-id="c3625-112">You can specify them in percentages, in the range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="c3625-113">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="c3625-113">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="c3625-114">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="c3625-114">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <span data-ttu-id="c3625-115"><a id="thumbnails"></a>Génération de miniatures</span><span class="sxs-lookup"><span data-stu-id="c3625-115"><a id="thumbnails"></a>Generate thumbnails</span></span>

<span data-ttu-id="c3625-116">Cette section montre comment personnaliser une présélection qui génère des miniatures.</span><span class="sxs-lookup"><span data-stu-id="c3625-116">This section shows how to customize a preset that generates thumbnails.</span></span> <span data-ttu-id="c3625-117">La présélection définie ci-dessous contient des informations sur la façon dont vous souhaitez encoder votre fichier, ainsi que les informations nécessaires à la génération des miniatures.</span><span class="sxs-lookup"><span data-stu-id="c3625-117">The preset defined below contains information on how you want to encode your file as well as information needed to generate thumbnails.</span></span> <span data-ttu-id="c3625-118">Vous pouvez utiliser l’une des présélections MES documentées dans [cette](media-services-mes-presets-overview.md) section et ajouter le code qui génère des miniatures.</span><span class="sxs-lookup"><span data-stu-id="c3625-118">You can take any of the MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="c3625-119">Le paramètre **SceneChangeDetection** figurant dans la présélection qui suit ne peut présenter la valeur true que si votre encodage porte sur une vidéo à vitesse de transmission unique.</span><span class="sxs-lookup"><span data-stu-id="c3625-119">The **SceneChangeDetection** setting in the following preset can only be set to true if you are encoding to a single  bitrate video.</span></span> <span data-ttu-id="c3625-120">Si votre encodage s’applique à une vidéo à plusieurs vitesses de transmission et que vous définissez **SceneChangeDetection** sur True, l’encodeur renvoie une erreur.</span><span class="sxs-lookup"><span data-stu-id="c3625-120">If you are encoding to a multi-bitrate video and set **SceneChangeDetection** to true, the encoder returns an error.</span></span>  
>
>

<span data-ttu-id="c3625-121">Pour plus d’informations sur le schéma, consultez [cette](media-services-mes-schema.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="c3625-121">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="c3625-122">Assurez-vous d’examiner la section [Considérations](#considerations) .</span><span class="sxs-lookup"><span data-stu-id="c3625-122">Make sure to review the [Considerations](#considerations) section.</span></span>

### <span data-ttu-id="c3625-123"><a id="json"></a>Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="c3625-123"><a id="json"></a>JSON preset</span></span>
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


### <span data-ttu-id="c3625-124"><a id="xml"></a>Présélection XML</span><span class="sxs-lookup"><span data-stu-id="c3625-124"><a id="xml"></a>XML preset</span></span>
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

### <a name="considerations"></a><span data-ttu-id="c3625-125">Considérations</span><span class="sxs-lookup"><span data-stu-id="c3625-125">Considerations</span></span>

<span data-ttu-id="c3625-126">Les considérations suivantes s'appliquent :</span><span class="sxs-lookup"><span data-stu-id="c3625-126">The following considerations apply:</span></span>

* <span data-ttu-id="c3625-127">L’utilisation d’horodatages explicites pour Début/Étape/Plage suppose que la source d’entrée a une longueur minimale de 1 minute.</span><span class="sxs-lookup"><span data-stu-id="c3625-127">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span></span>
* <span data-ttu-id="c3625-128">Les éléments Jpg/Png/BmpImage possèdent les attributs de chaîne Start, Step et Range, qui peuvent être interprétés comme suit :</span><span class="sxs-lookup"><span data-stu-id="c3625-128">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="c3625-129">Entiers non négatifs : nombre d’images, par exemple "Start": "120",</span><span class="sxs-lookup"><span data-stu-id="c3625-129">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="c3625-130">Présence du suffixe % : durée par rapport à la source, par exemple "Start": "15%", OU</span><span class="sxs-lookup"><span data-stu-id="c3625-130">Relative to source duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="c3625-131">Horodatage, s’il est exprimé au format</span><span class="sxs-lookup"><span data-stu-id="c3625-131">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="c3625-132">HH:MM:SS, par exemple « Start » : « 00:01:00 »</span><span class="sxs-lookup"><span data-stu-id="c3625-132">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="c3625-133">Vous pouvez combiner et apparier les notations à votre guise.</span><span class="sxs-lookup"><span data-stu-id="c3625-133">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="c3625-134">En outre, Start prend également en charge une macro spéciale, {Best}, qui tente de déterminer la première image de contenu « intéressante ». REMARQUE : Step et Range sont ignorés quand Start est défini sur {Best}.</span><span class="sxs-lookup"><span data-stu-id="c3625-134">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span></span>
  * <span data-ttu-id="c3625-135">La configuration par défaut est « Start:{Best} ».</span><span class="sxs-lookup"><span data-stu-id="c3625-135">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="c3625-136">Le format de sortie doit être fourni explicitement pour chaque format d’image : Png/Jpg/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="c3625-136">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="c3625-137">Quand il est présent, MES fait correspondre JpgVideo à JpgFormat et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="c3625-137">When present, MES matches JpgVideo to JpgFormat and so on.</span></span> <span data-ttu-id="c3625-138">OutputFormat introduit une nouvelle macro spécifique au codec d’image, {Index}, qui doit être présente (une fois seulement) pour les formats de sortie d’image.</span><span class="sxs-lookup"><span data-stu-id="c3625-138">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span></span>

## <span data-ttu-id="c3625-139"><a id="trim_video"></a>Rognage d’une vidéo (extrait)</span><span class="sxs-lookup"><span data-stu-id="c3625-139"><a id="trim_video"></a>Trim a video (clipping)</span></span>
<span data-ttu-id="c3625-140">Cette section explique comment modifier les présélections de l’encodeur pour découper ou rogner la vidéo d’entrée, dans laquelle l’entrée est ce que l’on appelle un fichier mezzanine ou un fichier à la demande.</span><span class="sxs-lookup"><span data-stu-id="c3625-140">This section talks about modifying the encoder presets to clip or trim the input video where the input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="c3625-141">L’encodeur peut également servir à découper ou rogner un élément multimédia capturé ou archivé à partir d’un streaming en direct. Pour obtenir des détails à ce sujet, consultez [ce blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="c3625-141">The encoder can also be used to clip or trim an asset, which is captured or archived from a live stream – the details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="c3625-142">Pour découper vos vidéos, vous pouvez utiliser l’une des présélections MES documentées dans [cette](media-services-mes-presets-overview.md) section et modifier l’élément **Sources** (comme indiqué ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="c3625-142">To trim your videos, you can take any of the MES presets documented [this](media-services-mes-presets-overview.md) section and modify the **Sources** element (as shown below).</span></span> <span data-ttu-id="c3625-143">La valeur de StartTime doit correspondre aux horodatages absolus de la vidéo d'entrée.</span><span class="sxs-lookup"><span data-stu-id="c3625-143">The value of StartTime needs to match the absolute timestamps of the input video.</span></span> <span data-ttu-id="c3625-144">Par exemple, si la première image de la vidéo d'entrée a un horodatage de 12:00:10.000, la valeur de StartTime doit être égale ou supérieure à 12:00:10.000.</span><span class="sxs-lookup"><span data-stu-id="c3625-144">For example, if the first frame of the input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="c3625-145">Dans l'exemple ci-dessous, nous supposons que la vidéo d'entrée a un horodatage de début égal à zéro.</span><span class="sxs-lookup"><span data-stu-id="c3625-145">In the example below, we assume that the input video has a starting timestamp of zero.</span></span> <span data-ttu-id="c3625-146">**Sources** doit être placé au début de la présélection.</span><span class="sxs-lookup"><span data-stu-id="c3625-146">**Sources** should be placed at the beginning of the preset.</span></span>

### <span data-ttu-id="c3625-147"><a id="json"></a>Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="c3625-147"><a id="json"></a>JSON preset</span></span>
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

### <a name="xml-preset"></a><span data-ttu-id="c3625-148">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="c3625-148">XML preset</span></span>
<span data-ttu-id="c3625-149">Pour découper vos vidéos, vous pouvez utiliser l’une des présélections MES documentées [ici](media-services-mes-presets-overview.md) et modifier l’élément **Sources** (comme indiqué ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="c3625-149">To trim your videos, you can take any of the MES presets documented [here](media-services-mes-presets-overview.md) and modify the **Sources** element (as shown below).</span></span>

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

## <span data-ttu-id="c3625-150"><a id="overlay"></a>Création d’une superposition</span><span class="sxs-lookup"><span data-stu-id="c3625-150"><a id="overlay"></a>Create an overlay</span></span>

<span data-ttu-id="c3625-151">Media Encoder Standard vous permet de superposer une image sur une vidéo existante.</span><span class="sxs-lookup"><span data-stu-id="c3625-151">The Media Encoder Standard allows you to overlay an image onto an existing video.</span></span> <span data-ttu-id="c3625-152">Les formats suivants sont actuellement pris en charge : png, jpg, gif et bmp.</span><span class="sxs-lookup"><span data-stu-id="c3625-152">Currently, the following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="c3625-153">La présélection définie ci-dessous illustre un exemple de superposition vidéo de base.</span><span class="sxs-lookup"><span data-stu-id="c3625-153">The preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="c3625-154">Après avoir défini un fichier de présélection, vous devez également indiquer à Media Services quel fichier de la ressource représente l’image de superposition et quel fichier représente la vidéo source sur laquelle vous souhaitez superposer l’image.</span><span class="sxs-lookup"><span data-stu-id="c3625-154">In addition to defining a preset file, you also have to let Media Services know which file in the asset is the overlay image and which file is the source video onto which you want to overlay the image.</span></span> <span data-ttu-id="c3625-155">Le fichier vidéo doit être le fichier **principal** .</span><span class="sxs-lookup"><span data-stu-id="c3625-155">The video file has to be the **primary** file.</span></span>

<span data-ttu-id="c3625-156">Si vous utilisez .NET, ajoutez les deux fonctions suivantes à l’exemple .NET défini dans [cette](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) rubrique.</span><span class="sxs-lookup"><span data-stu-id="c3625-156">If you are using .NET, add the following two functions to the .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="c3625-157">La fonction **UploadMediaFilesFromFolder** charge les fichiers d'un dossier (par exemple, BigBuckBunny.mp4 et Image001.png) et définit le fichier mp4 comme fichier principal dans la ressource.</span><span class="sxs-lookup"><span data-stu-id="c3625-157">The **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets the mp4 file to be the primary file in the asset.</span></span> <span data-ttu-id="c3625-158">La fonction **EncodeWithOverlay** utilise le fichier de présélection personnalisé qu’elle a reçu (par exemple, la présélection suivante) pour créer la tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="c3625-158">The **EncodeWithOverlay** function uses the custom preset file that was passed to it (for example, the preset that follows) to create the encoding task.</span></span>


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // The following code assumes 
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
        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify the input assets to be encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset to contain the results of the job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> <span data-ttu-id="c3625-159">Limitations actuelles :</span><span class="sxs-lookup"><span data-stu-id="c3625-159">Current limitations:</span></span>
>
> <span data-ttu-id="c3625-160">Le paramètre d’opacité de superposition n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c3625-160">The overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="c3625-161">Votre fichier vidéo source et le fichier d'image de superposition doivent être dans le même élément multimédia, et le fichier vidéo doit être défini en tant que fichier principal dans cet élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="c3625-161">Your source video file and the overlay image file have to be in the same asset, and the video file needs to be set as the primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="c3625-162">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="c3625-162">JSON preset</span></span>
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


### <a name="xml-preset"></a><span data-ttu-id="c3625-163">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="c3625-163">XML preset</span></span>
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


## <span data-ttu-id="c3625-164"><a id="silent_audio"></a>Insertion d’une piste audio en mode silencieux lorsque l’entrée ne produit pas de son</span><span class="sxs-lookup"><span data-stu-id="c3625-164"><a id="silent_audio"></a>Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="c3625-165">Par défaut, si vous envoyez à l’encodeur une entrée contenant uniquement de la vidéo (sans contenu audio), l’élément multimédia de sortie regroupe les fichiers qui contiennent uniquement des données vidéo.</span><span class="sxs-lookup"><span data-stu-id="c3625-165">By default, if you send an input to the encoder that contains only video, and no audio, then the output asset contains files that contain only video data.</span></span> <span data-ttu-id="c3625-166">Certains lecteurs ne sont peut-être pas capables de gérer ces flux de sortie.</span><span class="sxs-lookup"><span data-stu-id="c3625-166">Some players may not be able to handle such output streams.</span></span> <span data-ttu-id="c3625-167">Dans ce cas, vous pouvez utiliser ce paramètre pour forcer l’encodeur à ajouter à la sortie une piste audio en mode silencieux.</span><span class="sxs-lookup"><span data-stu-id="c3625-167">You can use this setting to force the encoder to add a silent audio track to the output in that scenario.</span></span>

<span data-ttu-id="c3625-168">Pour forcer l’encodeur à produire un élément multimédia contenant une piste audio en mode silencieux lorsque l’entrée ne comporte pas de son, spécifiez la valeur « InsertSilenceIfNoAudio ».</span><span class="sxs-lookup"><span data-stu-id="c3625-168">To force the encoder to produce an asset that contains a silent audio track when input has no audio, specify the "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="c3625-169">Vous pouvez utiliser l’une des présélections MES documentées dans [cette](media-services-mes-presets-overview.md) section et apporter la modification suivante :</span><span class="sxs-lookup"><span data-stu-id="c3625-169">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="c3625-170">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="c3625-170">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="c3625-171">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="c3625-171">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <span data-ttu-id="c3625-172"><a id="deinterlacing"></a>Désactiver le désentrelacement automatique</span><span class="sxs-lookup"><span data-stu-id="c3625-172"><a id="deinterlacing"></a>Disable auto de-interlacing</span></span>
<span data-ttu-id="c3625-173">Si les clients souhaitent que le contenu d’entrelacement soit automatiquement désentrelacé, aucune action n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c3625-173">Customers don’t need to do anything if they like the interlace contents to be automatically de-interlaced.</span></span> <span data-ttu-id="c3625-174">Quand le désentrelacement automatique est activé (par défaut), MES détecte automatiquement les images entrelacées et désentrelace uniquement les images marquées comme entrelacées.</span><span class="sxs-lookup"><span data-stu-id="c3625-174">When the auto de-interlacing is on (default) the MES does the auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="c3625-175">Vous pouvez désactiver le désentrelacement automatique.</span><span class="sxs-lookup"><span data-stu-id="c3625-175">You can turn the auto de-interlacing off.</span></span> <span data-ttu-id="c3625-176">Cette option n’est pas recommandée.</span><span class="sxs-lookup"><span data-stu-id="c3625-176">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="c3625-177">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="c3625-177">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="c3625-178">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="c3625-178">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <span data-ttu-id="c3625-179"><a id="audio_only"></a>Présélections audio uniquement</span><span class="sxs-lookup"><span data-stu-id="c3625-179"><a id="audio_only"></a>Audio-only presets</span></span>
<span data-ttu-id="c3625-180">Cette section présente deux présélections MES audio uniquement : Audio AAC et Bonne qualité audio AAC.</span><span class="sxs-lookup"><span data-stu-id="c3625-180">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="c3625-181">Audio AAC</span><span class="sxs-lookup"><span data-stu-id="c3625-181">AAC Audio</span></span>
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

### <a name="aac-good-quality-audio"></a><span data-ttu-id="c3625-182">Bonne qualité audio AAC</span><span class="sxs-lookup"><span data-stu-id="c3625-182">AAC Good Quality Audio</span></span>
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

## <span data-ttu-id="c3625-183"><a id="concatenate"></a>Concaténation de deux fichiers vidéo ou plus</span><span class="sxs-lookup"><span data-stu-id="c3625-183"><a id="concatenate"></a>Concatenate two or more video files</span></span>

<span data-ttu-id="c3625-184">L'exemple suivant décrit comment générer une présélection pour concaténer deux fichiers vidéo ou plus.</span><span class="sxs-lookup"><span data-stu-id="c3625-184">The following example illustrates how you can generate a preset to concatenate two or more video files.</span></span> <span data-ttu-id="c3625-185">Le scénario le plus courant consiste à ajouter une amorce de début ou de fin à la vidéo principale.</span><span class="sxs-lookup"><span data-stu-id="c3625-185">The most common scenario is when you want to add a header or a trailer to the main video.</span></span> <span data-ttu-id="c3625-186">Dans le cadre de l’utilisation prévue, les fichiers vidéo en cours de modification conjointe partagent des propriétés (résolution vidéo, fréquence d’images, nombre de pistes audio, etc.).</span><span class="sxs-lookup"><span data-stu-id="c3625-186">The intended use is when the video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="c3625-187">Vous devez prendre soin de ne pas mélanger des vidéos de différentes fréquences d’images ou comportant un nombre différent de pistes audio.</span><span class="sxs-lookup"><span data-stu-id="c3625-187">You should take care not to mix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="c3625-188">La conception actuelle de la fonctionnalité de concaténation suppose que les clips vidéo d’entrée soient cohérents en termes de résolution, de fréquence d’images etc.</span><span class="sxs-lookup"><span data-stu-id="c3625-188">The current design of the concatenation feature expects that the input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="c3625-189">Conditions requises et éléments à prendre en compte</span><span class="sxs-lookup"><span data-stu-id="c3625-189">Requirements and considerations</span></span>

* <span data-ttu-id="c3625-190">Les vidéos d'entrée ne doivent avoir qu'une seule piste audio.</span><span class="sxs-lookup"><span data-stu-id="c3625-190">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="c3625-191">Les vidéos d'entrée doivent avoir la même fréquence d'images.</span><span class="sxs-lookup"><span data-stu-id="c3625-191">Input videos should all have the same frame rate.</span></span>
* <span data-ttu-id="c3625-192">Vous devez télécharger vos vidéos dans des éléments multimédias séparés et définir les vidéos comme fichier primaire de chaque élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="c3625-192">You must upload your videos into separate assets and set the videos as the primary file in each asset.</span></span>
* <span data-ttu-id="c3625-193">Vous devez connaître la durée de vos vidéos.</span><span class="sxs-lookup"><span data-stu-id="c3625-193">You need to know the duration of your videos.</span></span>
* <span data-ttu-id="c3625-194">Les exemples prédéfinis ci-dessous supposent que toutes les vidéos d'entrée commencent avec un timestamp égal à zéro.</span><span class="sxs-lookup"><span data-stu-id="c3625-194">The preset examples below assumes that all the input videos start with a timestamp of zero.</span></span> <span data-ttu-id="c3625-195">Vous devez modifier les valeurs StartTime si les vidéos ont un timestamp de début différent, comme c’est généralement le cas avec les archives en direct.</span><span class="sxs-lookup"><span data-stu-id="c3625-195">You need to modify the StartTime values if the videos have different starting timestamp, as is typically the case with live archives.</span></span>
* <span data-ttu-id="c3625-196">La présélection JSON fait des références explicites aux valeurs AssetID des éléments multimédias d’entrée.</span><span class="sxs-lookup"><span data-stu-id="c3625-196">The JSON preset makes explicit references to the AssetID values of the input assets.</span></span>
* <span data-ttu-id="c3625-197">L'exemple de code suppose que la présélection JSON a été enregistrée dans un fichier local, par exemple « C:\supportFiles\preset.json ».</span><span class="sxs-lookup"><span data-stu-id="c3625-197">The sample code assumes that the JSON preset has been saved to a local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="c3625-198">Il suppose également que les deux éléments multimédias ont été créés en téléchargeant deux fichiers vidéo et que vous connaissez les valeurs AssetID résultantes.</span><span class="sxs-lookup"><span data-stu-id="c3625-198">It also assumes that two assets have been created by uploading two video files, and that you know the resultant AssetID values.</span></span>
* <span data-ttu-id="c3625-199">L'extrait de code et la présélection JSON montrent un exemple de concaténation de deux fichiers vidéo.</span><span class="sxs-lookup"><span data-stu-id="c3625-199">The code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="c3625-200">Vous pouvez l'étendre à plus de deux vidéos en :</span><span class="sxs-lookup"><span data-stu-id="c3625-200">You can extend it to more than two videos by:</span></span>

  1. <span data-ttu-id="c3625-201">Appelant task.InputAssets.Add() à plusieurs reprises pour ajouter d’autres vidéos, dans l'ordre.</span><span class="sxs-lookup"><span data-stu-id="c3625-201">Calling task.InputAssets.Add() repeatedly to add more videos, in order.</span></span>
  2. <span data-ttu-id="c3625-202">Apportant les modifications correspondantes à l'élément « Sources » dans le JSON, en ajoutant d’autres entrées, dans le même ordre.</span><span class="sxs-lookup"><span data-stu-id="c3625-202">Making corresponding edits to the "Sources" element in the JSON, by adding more entries, in the same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="c3625-203">Code .NET</span><span class="sxs-lookup"><span data-stu-id="c3625-203">.NET code</span></span>

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass to it the name of the
    // processor to use for the specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load the XML (or JSON) from the local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify the input videos to be concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset to contain the results of the job.
    // This output is specified as AssetCreationOptions.None, which
    // means the output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a><span data-ttu-id="c3625-204">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="c3625-204">JSON preset</span></span>

<span data-ttu-id="c3625-205">Mettez à jour votre présélection personnalisée avec les ID des éléments multimédias à concaténer et le segment de temps approprié pour chaque vidéo.</span><span class="sxs-lookup"><span data-stu-id="c3625-205">Update your custom preset with ids of the assets that you want to concatenate, and with the appropriate time segment for each video.</span></span>

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

## <span data-ttu-id="c3625-206"><a id="crop"></a>Rogner des vidéos avec l’encodeur multimédia standard</span><span class="sxs-lookup"><span data-stu-id="c3625-206"><a id="crop"></a>Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="c3625-207">Consultez la rubrique [Rogner des vidéos avec l’encodeur multimédia standard](media-services-crop-video.md) .</span><span class="sxs-lookup"><span data-stu-id="c3625-207">See the [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <span data-ttu-id="c3625-208"><a id="no_video"></a>Insertion d’une piste vidéo lorsque l’entrée ne comporte aucune vidéo</span><span class="sxs-lookup"><span data-stu-id="c3625-208"><a id="no_video"></a>Insert a video track when input has no video</span></span>

<span data-ttu-id="c3625-209">Par défaut, si vous envoyez à l’encodeur une entrée contenant uniquement de l’audio (sans contenu vidéo), l’élément multimédia de sortie regroupe les fichiers qui contiennent uniquement des données audio.</span><span class="sxs-lookup"><span data-stu-id="c3625-209">By default, if you send an input to the encoder that contains only audio, and no video, then the output asset contains files that contain only audio data.</span></span> <span data-ttu-id="c3625-210">Certains lecteurs, y compris Azure Media Player (consultez [ceci](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) peuvent ne pas être en mesure de gérer ces flux.</span><span class="sxs-lookup"><span data-stu-id="c3625-210">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able to handle such streams.</span></span> <span data-ttu-id="c3625-211">Dans ce cas, vous pouvez utiliser ce paramètre pour forcer l’encodeur à ajouter à la sortie une piste vidéo monochrome.</span><span class="sxs-lookup"><span data-stu-id="c3625-211">You can use this setting to force the encoder to add a monochrome video track to the output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="c3625-212">Le fait de forcer l’encodeur à insérer une piste vidéo de sortie augmente la taille de l’élément multimédia de sortie, et ainsi les coûts associés à la tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="c3625-212">Forcing the encoder to insert an output video track increases the size of the output Asset, and thereby the cost incurred for the encoding Task.</span></span> <span data-ttu-id="c3625-213">Vous devez exécuter des tests pour vérifier que cette augmentation résultante n’a qu’une légère incidence sur vos frais mensuels.</span><span class="sxs-lookup"><span data-stu-id="c3625-213">You should run tests to verify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>

### <a name="inserting-video-at-only-the-lowest-bitrate"></a><span data-ttu-id="c3625-214">Insertion de vidéo uniquement avec le débit le plus bas</span><span class="sxs-lookup"><span data-stu-id="c3625-214">Inserting video at only the lowest bitrate</span></span>

<span data-ttu-id="c3625-215">Supposons que vous utilisez un encodage à plusieurs vitesses de transmission prédéfinies, par exemple [« H264 multidébit 720p »](media-services-mes-preset-h264-multiple-bitrate-720p.md) pour encoder à des fins de diffusion en continu votre catalogue d’entrée tout entier, qui contient un mélange de fichiers vidéo et audio uniquement.</span><span class="sxs-lookup"><span data-stu-id="c3625-215">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) to encode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="c3625-216">Dans ce scénario, lorsque l’entrée ne comporte aucune vidéo, vous pouvez vouloir forcer l’encodeur à insérer une piste vidéo monochrome au plus faible débit uniquement, et non à toutes les vitesses de transmission de sortie.</span><span class="sxs-lookup"><span data-stu-id="c3625-216">In this scenario, when the input has no video, you may want to force the encoder to insert a monochrome video track at just the lowest bitrate, as opposed to inserting video at every output bitrate.</span></span> <span data-ttu-id="c3625-217">Pour ce faire, vous devez utiliser l’indicateur **InsertBlackIfNoVideoBottomLayerOnly**.</span><span class="sxs-lookup"><span data-stu-id="c3625-217">To achieve this, you need to use the **InsertBlackIfNoVideoBottomLayerOnly** flag.</span></span>

<span data-ttu-id="c3625-218">Vous pouvez utiliser l’une des présélections MES documentées dans [cette](media-services-mes-presets-overview.md) section et apporter la modification suivante :</span><span class="sxs-lookup"><span data-stu-id="c3625-218">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="c3625-219">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="c3625-219">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="c3625-220">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="c3625-220">XML preset</span></span>

<span data-ttu-id="c3625-221">Avec le XML, utilisez Condition="InsertBlackIfNoVideoBottomLayerOnly" en tant qu’attribut pour l’élément **H264Video** et Condition="InsertSilenceIfNoAudio" en tant qu’attribut pour **AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="c3625-221">When using XML, use Condition="InsertBlackIfNoVideoBottomLayerOnly" as an attribute to the **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute to **AACAudio**.</span></span>

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

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="c3625-222">Insertion de vidéo à tous les débits binaires de sortie</span><span class="sxs-lookup"><span data-stu-id="c3625-222">Inserting video at all output bitrates</span></span>
<span data-ttu-id="c3625-223">Supposons que vous utilisez un encodage à plusieurs vitesses de transmission prédéfinies, par exemple [« H264 multidébit 720p »](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) pour encoder à des fins de diffusion en continu votre catalogue d’entrée tout entier, qui contient un mélange de fichiers vidéo et audio uniquement.</span><span class="sxs-lookup"><span data-stu-id="c3625-223">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) to encode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="c3625-224">Dans ce scénario, lorsque l’entrée ne comporte aucune vidéo, vous pouvez vouloir forcer l’encodeur à insérer une piste vidéo monochrome à toutes les vitesses de transmission de sortie.</span><span class="sxs-lookup"><span data-stu-id="c3625-224">In this scenario, when the input has no video, you may want to force the encoder to insert a monochrome video track at all the output bitrates.</span></span> <span data-ttu-id="c3625-225">Cela garantit que vos éléments multimédias de sortie sont tous homogènes en ce qui concerne le nombre de pistes vidéo et de pistes audio.</span><span class="sxs-lookup"><span data-stu-id="c3625-225">This ensures that your output Assets are all homogenous with respect to number of video tracks and audio tracks.</span></span> <span data-ttu-id="c3625-226">Pour ce faire, vous devez spécifier l’indicateur « InsertBlackIfNoVideo ».</span><span class="sxs-lookup"><span data-stu-id="c3625-226">To achieve this, you need to specify the "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="c3625-227">Vous pouvez utiliser l’une des présélections MES documentées dans [cette](media-services-mes-presets-overview.md) section et apporter la modification suivante :</span><span class="sxs-lookup"><span data-stu-id="c3625-227">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="c3625-228">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="c3625-228">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="c3625-229">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="c3625-229">XML preset</span></span>

<span data-ttu-id="c3625-230">Avec le XML, utilisez Condition="InsertBlackIfNoVideo" en tant qu’attribut pour l’élément **H264Video** et Condition="InsertSilenceIfNoAudio" en tant qu’attribut pour **AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="c3625-230">When using XML, use Condition="InsertBlackIfNoVideo" as an attribute to the **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute to **AACAudio**.</span></span>

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

## <span data-ttu-id="c3625-231"><a id="rotate_video"></a>Faire pivoter une vidéo</span><span class="sxs-lookup"><span data-stu-id="c3625-231"><a id="rotate_video"></a>Rotate a video</span></span>
<span data-ttu-id="c3625-232">[Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) prend en charge les angles de rotation 0, 90,180 et 270.</span><span class="sxs-lookup"><span data-stu-id="c3625-232">The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="c3625-233">Le comportement par défaut est « Auto », ce qui signifie qu’il tente de détecter les métadonnées de rotation dans le fichier vidéo entrant et de les compenser.</span><span class="sxs-lookup"><span data-stu-id="c3625-233">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming video file and compensate for it.</span></span> <span data-ttu-id="c3625-234">Incluez l’élément **Sources** suivant dans l’une des présélections définies dans [cette](media-services-mes-presets-overview.md) section :</span><span class="sxs-lookup"><span data-stu-id="c3625-234">Include the following **Sources** element to one of the presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="c3625-235">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="c3625-235">JSON preset</span></span>
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
### <a name="xml-preset"></a><span data-ttu-id="c3625-236">Présélection XML</span><span class="sxs-lookup"><span data-stu-id="c3625-236">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="c3625-237">Consultez également [cette](media-services-mes-schema.md#PreserveResolutionAfterRotation) rubrique pour plus d’informations sur la manière dont l’encodeur interprète les paramètres de largeur et de hauteur dans la présélection, lorsque la compensation de la rotation est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="c3625-237">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how the encoder interprets the Width and Height settings in the preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="c3625-238">Vous pouvez utiliser la valeur « 0 » pour indiquer à l’encodeur d’ignorer les métadonnées de rotation, le cas échéant, dans la vidéo d’entrée.</span><span class="sxs-lookup"><span data-stu-id="c3625-238">You can use the value "0" to indicate to the encoder to ignore rotation metadata, if present, in the input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c3625-239">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="c3625-239">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c3625-240">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="c3625-240">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="c3625-241">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c3625-241">See Also</span></span>
[<span data-ttu-id="c3625-242">Vue d’ensemble de l’encodage de Media Services</span><span class="sxs-lookup"><span data-stu-id="c3625-242">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
