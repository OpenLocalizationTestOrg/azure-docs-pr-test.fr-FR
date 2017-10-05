---
title: "H264 - Vitesse de transmission multiple - 4 x 3 SD -Audio 5.1 | Microsoft Docs"
description: "Cette rubrique offre une vue d’ensemble de la présélection de travaux **H264 -Vitesse de transmission multiple -4 x 3 SD - Audio 5.1**."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 24faec4f-a69c-4ae5-afd4-308e03046a3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: ff918754b224b0ee9158d73d57aa514dbec595ed
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="h264-multiple-bitrate-4x3-sd-audio-51"></a><span data-ttu-id="b518f-103">H264 – Vitesse de transmission multiple – 4 x 3 SD – Audio 5.1</span><span class="sxs-lookup"><span data-stu-id="b518f-103">H264 Multiple Bitrate 4x3 SD Audio 5.1</span></span>
<span data-ttu-id="b518f-104">`Media Encoder Standard` définit un ensemble de présélections d’encodage à utiliser lors de la création de travaux d’encodage.</span><span class="sxs-lookup"><span data-stu-id="b518f-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="b518f-105">Vous pouvez utiliser un `preset name` afin de spécifier le format dans lequel vous souhaitez encoder votre fichier multimédia.</span><span class="sxs-lookup"><span data-stu-id="b518f-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="b518f-106">Sinon, vous pouvez créer vos propres présélections basées sur JSON ou XML (à l’aide de l’encodage UTF-8 ou UTF-16).</span><span class="sxs-lookup"><span data-stu-id="b518f-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="b518f-107">Vous pouvez ensuite transmettre la présélection personnalisée à l’encodeur.</span><span class="sxs-lookup"><span data-stu-id="b518f-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="b518f-108">Pour obtenir la liste de tous les noms de présélections pris en charge par cet encodeur `Media Encoder Standard`, consultez [Présélections de tâches pour Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b518f-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="b518f-109">Cette rubrique représente la présélection `H264 Multiple Bitrate 4x3 SD Audio 5.1` aux formats XML et JSON.</span><span class="sxs-lookup"><span data-stu-id="b518f-109">This topic shows the `H264 Multiple Bitrate 4x3 SD Audio 5.1` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="b518f-110">Cette présélection produit un ensemble de 5 fichiers MP4 alignés sur le groupe d’images, de 1 600 kbit/s à 400 kbit/s, et de l’audio AAC 5.1.</span><span class="sxs-lookup"><span data-stu-id="b518f-110">This preset produces a set of 5 GOP-aligned MP4 files, ranging from 1600 kbps to 400 kbps, and AAC 5.1 audio.</span></span> <span data-ttu-id="b518f-111">Pour plus d’informations sur le profil, la vitesse de transmission, la fréquence d’échantillonnage, etc. de cette présélection, examinez le format XML ou JSON défini ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b518f-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="b518f-112">Pour consulter une explication de la signification des éléments et les valeurs valides pour chaque élément, consultez la rubrique [Media Encoder Standard schema](media-services-mes-schema.md) (Schéma Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="b518f-112">For explanations of what each element means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md)..</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b518f-113">Lorsque vous modifiez les valeurs `Width` et `Height` sur les couches, assurez-vous que les proportions demeurent constantes.</span><span class="sxs-lookup"><span data-stu-id="b518f-113">When modifying the `Width` and `Height` values across layers, make sure that the aspect ratio remains consistent.</span></span> <span data-ttu-id="b518f-114">Par exemple : 1 920 x 1 080, 1 280 x 720, 1 080 x 576, 640 x 360.</span><span class="sxs-lookup"><span data-stu-id="b518f-114">For example: 1920x1080, 1280x720, 1080x576, 640x360.</span></span> <span data-ttu-id="b518f-115">Vous ne devez pas utiliser un mélange de proportions, comme : 1 280 x 720, 720 x 480, 640 x 360.</span><span class="sxs-lookup"><span data-stu-id="b518f-115">You should not use a mixture of aspect ratios, such as: 1280x720, 720x480, 640x360.</span></span>  
  
 <span data-ttu-id="b518f-116">XML</span><span class="sxs-lookup"><span data-stu-id="b518f-116">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>1600</Bitrate>  
          <Width>640</Width>  
          <Height>480</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>1600</MaxBitrate>  
        </H264Layer>  
        <H264Layer>  
          <Bitrate>1300</Bitrate>  
          <Width>640</Width>  
          <Height>480</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>1300</MaxBitrate>  
        </H264Layer>  
        <H264Layer>  
          <Bitrate>800</Bitrate>  
          <Width>480</Width>  
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
          <MaxBitrate>800</MaxBitrate>  
        </H264Layer>  
        <H264Layer>  
          <Bitrate>600</Bitrate>  
          <Width>480</Width>  
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
          <MaxBitrate>600</MaxBitrate>  
        </H264Layer>  
        <H264Layer>  
          <Bitrate>400</Bitrate>  
          <Width>360</Width>  
          <Height>240</Height>  
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
      <Chapters />  
    </H264Video>  
    <AACAudio>  
      <Profile>AACLC</Profile>  
      <Channels>6</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>384</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 <span data-ttu-id="b518f-117">JSON</span><span class="sxs-lookup"><span data-stu-id="b518f-117">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 1600,  
          "MaxBitrate": 1600,  
          "BufferWindow": "00:00:05",  
          "Width": 640,  
          "Height": 480,  
          "BFrames": 3,  
          "ReferenceFrames": 3,  
          "AdaptiveBFrame": true,  
          "Type": "H264Layer",  
          "FrameRate": "0/1"  
        },  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 1300,  
          "MaxBitrate": 1300,  
          "BufferWindow": "00:00:05",  
          "Width": 640,  
          "Height": 480,  
          "BFrames": 3,  
          "ReferenceFrames": 3,  
          "AdaptiveBFrame": true,  
          "Type": "H264Layer",  
          "FrameRate": "0/1"  
        },  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 800,  
          "MaxBitrate": 800,  
          "BufferWindow": "00:00:05",  
          "Width": 480,  
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
          "Bitrate": 600,  
          "MaxBitrate": 600,  
          "BufferWindow": "00:00:05",  
          "Width": 480,  
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
          "Width": 360,  
          "Height": 240,  
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
      "Channels": 6,  
      "SamplingRate": 48000,  
      "Bitrate": 384,  
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
```
