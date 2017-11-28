---
title: "Présélection Media Encoder Standard H264 - Vitesse de transmission unique - 16 x 9 SD - Azure | Microsoft Docs"
description: "La rubrique présente une vue d’ensemble de la présélection de travaux **H264 - Vitesse de transmission unique - 16 x 9 SD**."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ce0efc07-3461-44f6-a7bc-c4877bc09529
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 746dc845f1e32d6be3f207448523d8966da9f8a0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="h264-single-bitrate-16x9-sd"></a><span data-ttu-id="cc77f-103">H264 – Vitesse de transmission unique – 16 x 9 SD</span><span class="sxs-lookup"><span data-stu-id="cc77f-103">H264 Single Bitrate 16x9 SD</span></span>
<span data-ttu-id="cc77f-104">`Media Encoder Standard` définit un ensemble de présélections d’encodage à utiliser lors de la création de travaux d’encodage.</span><span class="sxs-lookup"><span data-stu-id="cc77f-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="cc77f-105">Vous pouvez utiliser un `preset name` afin de spécifier le format dans lequel vous souhaitez encoder votre fichier multimédia.</span><span class="sxs-lookup"><span data-stu-id="cc77f-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="cc77f-106">Sinon, vous pouvez créer vos propres présélections basées sur JSON ou XML (à l’aide de l’encodage UTF-8 ou UTF-16).</span><span class="sxs-lookup"><span data-stu-id="cc77f-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="cc77f-107">Vous pouvez ensuite transmettre la présélection personnalisée à l’encodeur.</span><span class="sxs-lookup"><span data-stu-id="cc77f-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="cc77f-108">Pour obtenir la liste de tous les noms de présélections pris en charge par cet encodeur `Media Encoder Standard`, consultez [Présélections de tâches pour Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cc77f-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="cc77f-109">Cette rubrique représente la présélection `H264 Single Bitrate 16x9 SD` aux formats XML et JSON.</span><span class="sxs-lookup"><span data-stu-id="cc77f-109">This topic shows the `H264 Single Bitrate 16x9 SD` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="cc77f-110">Cette présélection produit un fichier MP4 unique avec une vitesse de transmission de 2 200 kbit/s, et de l’audio stéréo AAC.</span><span class="sxs-lookup"><span data-stu-id="cc77f-110">This preset produces a single MP4 file with a bitrate of 2200 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="cc77f-111">Pour plus d’informations sur le profil, la vitesse de transmission, la fréquence d’échantillonnage, etc. de cette présélection, examinez le format XML ou JSON défini ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cc77f-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="cc77f-112">Pour consulter une explication de la signification des éléments des présélections et les valeurs valides pour chaque élément, consultez la rubrique [Media Encoder Standard schema](media-services-mes-schema.md) (Schéma Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="cc77f-112">For explanations of what each element in these presets means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
 <span data-ttu-id="cc77f-113">XML</span><span class="sxs-lookup"><span data-stu-id="cc77f-113">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>2200</Bitrate>  
          <Width>848</Width>  
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
          <MaxBitrate>2200</MaxBitrate>  
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
  
 <span data-ttu-id="cc77f-114">JSON</span><span class="sxs-lookup"><span data-stu-id="cc77f-114">JSON</span></span>  
  
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
          "Bitrate": 2200,  
          "MaxBitrate": 2200,  
          "BufferWindow": "00:00:05",  
          "Width": 848,  
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
