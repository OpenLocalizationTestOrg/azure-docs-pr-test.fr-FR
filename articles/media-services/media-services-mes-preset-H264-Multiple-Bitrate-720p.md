---
title: "aaaH264 plusieurs débits binaires 720p présélection Media Encoder Standard - Azure | Documents Microsoft"
description: "rubrique de Hello donne une vue d’ensemble de hello ** H264 plusieurs débits binaires 720 p ** présélection de tâches."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 10dfad38-2112-42ab-b99b-8f74a94513c3
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: bea3e879d2c6ae8c7a2af483360202697c1a082c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="h264-multiple-bitrate-720p"></a><span data-ttu-id="1661f-103">H264 multidébit 720 pixels</span><span class="sxs-lookup"><span data-stu-id="1661f-103">H264 Multiple Bitrate 720p</span></span>
<span data-ttu-id="1661f-104">`Media Encoder Standard` définit un ensemble de présélections d’encodage à utiliser lors de la création de travaux d’encodage.</span><span class="sxs-lookup"><span data-stu-id="1661f-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="1661f-105">Vous pouvez utiliser un `preset name` toospecify dans le format que tooencode votre fichier multimédia.</span><span class="sxs-lookup"><span data-stu-id="1661f-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="1661f-106">Sinon, vous pouvez créer vos propres présélections basées sur JSON ou XML (à l’aide de l’encodage UTF-8 ou UTF-16).</span><span class="sxs-lookup"><span data-stu-id="1661f-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="1661f-107">Vous pouvez ensuite transmettre encodeur personnalisé toohello prédéfini de hello.</span><span class="sxs-lookup"><span data-stu-id="1661f-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="1661f-108">Pour la liste de tous les hello hello présélection noms pris en charge par ce `Media Encoder Standard` encodeur, consultez [Présélections de tâches pour Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1661f-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="1661f-109">Cette rubrique montre hello `H264 Multiple Bitrate 720p` prédéfinie au format XML et JSON.</span><span class="sxs-lookup"><span data-stu-id="1661f-109">This topic shows hello `H264 Multiple Bitrate 720p` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="1661f-110">Cette valeur prédéfinie génère un ensemble de 6 fichiers MP4 alignés GOP, allant des 3400 Kbits/s de too400 Kbits/s et audio AAC stéréo.</span><span class="sxs-lookup"><span data-stu-id="1661f-110">This preset produces a set of 6 GOP-aligned MP4 files, ranging from 3400 kbps too400 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="1661f-111">Pour obtenir des informations détaillées sur le profil, vitesse de transmission, d’échantillonnage, le taux, etc. cela prédéfinies, examiner hello XML ou JSON défini ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1661f-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="1661f-112">Pour obtenir des explications quelles chaque élément de ces moyens de paramètres prédéfinis et que les valeurs valides de hello pour chaque élément, consultez hello [schéma Media Encoder Standard](media-services-mes-schema.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="1661f-112">For explanations of what each element in these presets means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="1661f-113">Lorsque vous modifiez hello `Width` et `Height` couches, les valeurs s’assurer que proportions hello reste cohérente.</span><span class="sxs-lookup"><span data-stu-id="1661f-113">When modifying hello `Width` and `Height` values across layers, make sure that hello aspect ratio remains consistent.</span></span> <span data-ttu-id="1661f-114">Par exemple : 1 920 x 1 080, 1 280 x 720, 1 080 x 576, 640 x 360.</span><span class="sxs-lookup"><span data-stu-id="1661f-114">For example: 1920x1080, 1280x720, 1080x576, 640x360.</span></span> <span data-ttu-id="1661f-115">Vous ne devez pas utiliser un mélange de proportions, comme : 1 280 x 720, 720 x 480, 640 x 360.</span><span class="sxs-lookup"><span data-stu-id="1661f-115">You should not use a mixture of aspect ratios, such as: 1280x720, 720x480, 640x360.</span></span>  
  
 <span data-ttu-id="1661f-116">XML</span><span class="sxs-lookup"><span data-stu-id="1661f-116">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
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
  
 <span data-ttu-id="1661f-117">JSON</span><span class="sxs-lookup"><span data-stu-id="1661f-117">JSON</span></span>  
  
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
```
