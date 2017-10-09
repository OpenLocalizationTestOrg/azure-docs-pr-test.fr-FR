---
title: "présélection de transmission unique – 4K Media Encoder Standard aaaH264 - Azure | Documents Microsoft"
description: "rubrique de Hello donne une vue d’ensemble de hello ** h264 – vitesse de transmission unique – 4 K ** présélection de tâches."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 8e437aea-8193-49a0-9ff2-4fd391c80972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 3a88207ba89baaefddfea631aa5d4c1c74194c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-4k"></a><span data-ttu-id="90be6-103">H264 multidébit 4K</span><span class="sxs-lookup"><span data-stu-id="90be6-103">H264 Single Bitrate 4K</span></span>
<span data-ttu-id="90be6-104">`Media Encoder Standard` définit un ensemble de présélections d’encodage à utiliser lors de la création de travaux d’encodage.</span><span class="sxs-lookup"><span data-stu-id="90be6-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="90be6-105">Vous pouvez utiliser un `preset name` toospecify dans le format que tooencode votre fichier multimédia.</span><span class="sxs-lookup"><span data-stu-id="90be6-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="90be6-106">Sinon, vous pouvez créer vos propres présélections basées sur JSON ou XML (à l’aide de l’encodage UTF-8 ou UTF-16).</span><span class="sxs-lookup"><span data-stu-id="90be6-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="90be6-107">Vous pouvez ensuite transmettre encodeur personnalisé toohello prédéfini de hello.</span><span class="sxs-lookup"><span data-stu-id="90be6-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="90be6-108">Pour la liste de tous les hello hello présélection noms pris en charge par ce `Media Encoder Standard` encodeur, consultez [Présélections de tâches pour Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="90be6-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="90be6-109">Cette rubrique montre hello `H264 Single Bitrate 4K` prédéfinie au format XML et JSON.</span><span class="sxs-lookup"><span data-stu-id="90be6-109">This topic shows hello `H264 Single Bitrate 4K` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="90be6-110">Cette présélection produit un fichier MP4 unique avec une vitesse de transmission de 18 000 kbit/s, et de l’audio stéréo AAC.</span><span class="sxs-lookup"><span data-stu-id="90be6-110">This preset produces a single MP4 file with a bitrate of 18000 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="90be6-111">Pour obtenir des informations détaillées sur le profil, vitesse de transmission, d’échantillonnage, le taux, etc. cela prédéfinies, examiner hello XML ou JSON défini ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="90be6-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="90be6-112">Pour obtenir des explications quelles chaque élément de ces moyens de paramètres prédéfinis et que les valeurs valides de hello pour chaque élément, consultez hello [schéma Media Encoder Standard](media-services-mes-schema.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="90be6-112">For explanations of what each element in these presets means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="90be6-113">Vous devez obtenir hello prime réservé encode du type d’unité avec 4 Ko.</span><span class="sxs-lookup"><span data-stu-id="90be6-113">You should get hello Premium reserved unit type with 4K encodes.</span></span> <span data-ttu-id="90be6-114">Pour plus d’informations, consultez [comment tooScale codage](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span><span class="sxs-lookup"><span data-stu-id="90be6-114">For more information, see [How tooScale Encoding](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span></span>  
  
 <span data-ttu-id="90be6-115">XML</span><span class="sxs-lookup"><span data-stu-id="90be6-115">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>18000</Bitrate>  
          <Width>3840</Width>  
          <Height>2160</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>18000</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
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
```  
  
 <span data-ttu-id="90be6-116">JSON</span><span class="sxs-lookup"><span data-stu-id="90be6-116">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 18000,  
          "MaxBitrate": 18000,  
          "BufferWindow": "00:00:05",  
          "Width": 3840,  
          "Height": 2160,  
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
```
