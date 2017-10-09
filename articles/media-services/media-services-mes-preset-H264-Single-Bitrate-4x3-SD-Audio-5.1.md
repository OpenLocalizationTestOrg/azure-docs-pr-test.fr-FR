---
title: "aaaH264 de transmission unique – 4 x 3 SD – Audio 5.1 | Documents Microsoft"
description: "rubrique de Hello donne une vue d’ensemble de hello ** H264 unique 4 x 3 SD – Audio 5.1* * présélection de tâches."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: e55dd302-2f42-46b5-ae17-bd3c72329c03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 48b29432d1675de55a2ee5102c9a3cbd8b034d27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-4x3-sd-audio-51"></a><span data-ttu-id="a9199-103">H264 – Vitesse de transmission unique – 4 x 3 SD – Audio 5.1</span><span class="sxs-lookup"><span data-stu-id="a9199-103">H264 Single Bitrate 4x3 SD Audio 5.1</span></span>
<span data-ttu-id="a9199-104">`Media Encoder Standard` définit un ensemble de présélections d’encodage à utiliser lors de la création de travaux d’encodage.</span><span class="sxs-lookup"><span data-stu-id="a9199-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="a9199-105">Vous pouvez utiliser un `preset name` toospecify dans le format que tooencode votre fichier multimédia.</span><span class="sxs-lookup"><span data-stu-id="a9199-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="a9199-106">Sinon, vous pouvez créer vos propres présélections basées sur JSON ou XML (à l’aide de l’encodage UTF-8 ou UTF-16).</span><span class="sxs-lookup"><span data-stu-id="a9199-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="a9199-107">Vous pouvez ensuite transmettre encodeur personnalisé toohello prédéfini de hello.</span><span class="sxs-lookup"><span data-stu-id="a9199-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="a9199-108">Pour la liste de tous les hello hello présélection noms pris en charge par ce `Media Encoder Standard` encodeur, consultez [Présélections de tâches pour Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a9199-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="a9199-109">Cette rubrique montre hello `H264 Single Bitrate 4x3 SD Audio 5.1` prédéfinie au format XML et JSON.</span><span class="sxs-lookup"><span data-stu-id="a9199-109">This topic shows hello `H264 Single Bitrate 4x3 SD Audio 5.1` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="a9199-110">Cette présélection produit un fichier MP4 unique avec une vitesse de transmission de 1800 kbit/s, et de l’audio AAC 5.1.</span><span class="sxs-lookup"><span data-stu-id="a9199-110">This preset produces a single MP4 file with a bitrate of 1800 kbps, and AAC 5.1 audio.</span></span> <span data-ttu-id="a9199-111">Pour obtenir des informations détaillées sur le profil, vitesse de transmission, d’échantillonnage, le taux, etc. cela prédéfinies, examiner hello XML ou JSON défini ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a9199-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="a9199-112">Pour des explications signifie de chaque élément et les valeurs valides de hello pour chaque élément, consultez hello [schéma Media Encoder Standard](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a9199-112">For explanations of what each element means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>  
  
 <span data-ttu-id="a9199-113">XML</span><span class="sxs-lookup"><span data-stu-id="a9199-113">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>1800</Bitrate>  
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
          <MaxBitrate>1800</MaxBitrate>  
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
  
 <span data-ttu-id="a9199-114">JSON</span><span class="sxs-lookup"><span data-stu-id="a9199-114">JSON</span></span>  
  
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
          "Bitrate": 1800,  
          "MaxBitrate": 1800,  
          "BufferWindow": "00:00:05",  
          "Width": 640,  
          "Height": 480,  
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
