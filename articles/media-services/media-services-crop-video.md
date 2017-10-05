---
title: "Guide pratique pour rogner des vidéos avec Media Encoder Standard - Azure | Microsoft Docs"
description: "Cet article explique comment rogner des vidéos avec Media Encoder Standard."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 7628f674-2005-4531-8b61-d7a4f53e46ba
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/09/2017
ms.author: anilmur;juliako;
ms.openlocfilehash: 60d0ce14a271fcbe698559da95ca011cb888b221
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="d2599-103">Rogner des vidéos avec l’encodeur multimédia standard</span><span class="sxs-lookup"><span data-stu-id="d2599-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="d2599-104">Vous pouvez utiliser Media Encoder Standard (MES) pour rogner votre vidéo d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d2599-104">You can use Media Encoder Standard (MES) to crop your input video.</span></span> <span data-ttu-id="d2599-105">Le rognage consiste à sélectionner une fenêtre rectangulaire dans l’image vidéo et à encoder uniquement les pixels dans cette fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d2599-105">Cropping is the process of selecting a rectangular window within the video frame, and encoding just the pixels within that window.</span></span> <span data-ttu-id="d2599-106">Le schéma suivant permet d’illustrer le processus.</span><span class="sxs-lookup"><span data-stu-id="d2599-106">The following diagram helps illustrate the process.</span></span>

![Rogner une vidéo](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="d2599-108">Vous disposez en tant qu’entrée d’une vidéo présentant une résolution de 1920 x 1080 pixels (proportions 16:9), avec des barres noires (pillarbox) à gauche et à droite, de manière à ce que seule une fenêtre de 4:3 ou 1440 x 1080 pixels puisse contenir une vidéo active.</span><span class="sxs-lookup"><span data-stu-id="d2599-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at the left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="d2599-109">Vous pouvez utiliser MES pour rogner ou modifier les barres noires, et coder la région 1440 x 1080.</span><span class="sxs-lookup"><span data-stu-id="d2599-109">You can use MES to crop or edit out the black bars, and encode the 1440x1080 region.</span></span>

<span data-ttu-id="d2599-110">Le rognage dans MES étant une étape de prétraitement, les paramètres de rognage de la présélection d’encodage s’appliquent à la vidéo d’entrée d’origine.</span><span class="sxs-lookup"><span data-stu-id="d2599-110">Cropping in MES is a pre-processing stage, so the cropping parameters in the encoding preset apply to the original input video.</span></span> <span data-ttu-id="d2599-111">L’encodage s’effectue à un stade ultérieur, et les paramètres de largeur/hauteur s’appliquent à la vidéo *prétraitée* et non à la vidéo d’origine.</span><span class="sxs-lookup"><span data-stu-id="d2599-111">Encoding is a subsequent stage, and the width/height settings apply to the *pre-processed* video, and not to the original video.</span></span> <span data-ttu-id="d2599-112">Lorsque vous concevez votre présélection, vous devez effectuer les opérations suivantes : (a) sélectionnez les paramètres de rognage en fonction de la vidéo d’entrée d’origine et (b) sélectionnez vos paramètres d’encodage en fonction de la vidéo rognée.</span><span class="sxs-lookup"><span data-stu-id="d2599-112">When designing your preset you need to do the following: (a) select the crop parameters based on the original input video, and (b) select your encode settings based on the cropped video.</span></span> <span data-ttu-id="d2599-113">Si vos paramètres d’encodage ne correspondent pas à la vidéo rognée, le résultat ne répondra pas à vos attentes.</span><span class="sxs-lookup"><span data-stu-id="d2599-113">If you do not match your encode settings to the cropped video, the output will not be as you expect.</span></span>

<span data-ttu-id="d2599-114">La rubrique [suivante](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) montre comment créer une tâche d’encodage avec MES et comment spécifier une présélection personnalisée pour la tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="d2599-114">The [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how to create an encoding job with MES and how to specify a custom preset for the encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="d2599-115">Création d’une présélection personnalisée</span><span class="sxs-lookup"><span data-stu-id="d2599-115">Creating a custom preset</span></span>
<span data-ttu-id="d2599-116">Dans l’exemple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d2599-116">In the example shown in the diagram:</span></span>

1. <span data-ttu-id="d2599-117">L’entrée d’origine est 1920 x 1080.</span><span class="sxs-lookup"><span data-stu-id="d2599-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="d2599-118">Elle doit être rognée sur une sortie de 1440 x 1080, centrée dans le cadre d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d2599-118">It needs to be cropped to an output of 1440x1080, which is centered in the input frame</span></span>
3. <span data-ttu-id="d2599-119">Cela implique un décalage X de (1920 – 1440)/2 = 240 et un décalage Y de zéro.</span><span class="sxs-lookup"><span data-stu-id="d2599-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="d2599-120">La largeur et la hauteur du rectangle de rognage sont de 1440 et 1080, respectivement.</span><span class="sxs-lookup"><span data-stu-id="d2599-120">The Width and Height of the Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="d2599-121">Dans la phase de codage, la tâche consiste à produire trois couches avec des résolutions respectives de 1440 x 1080, 960 x 720 et 480 x 360.</span><span class="sxs-lookup"><span data-stu-id="d2599-121">In the encode stage, the ask is to produce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="d2599-122">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="d2599-122">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "Crop": {
                "X": 240,
                "Y": 0,
                "Width": 1440,
                "Height": 1080
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
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1440,
              "Height": 1080,
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
              "Bitrate": 1250,
              "MaxBitrate": 1250,
              "BufferWindow": "00:00:05",
              "Width": 480,
              "Height": 360,
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="d2599-123">Restrictions sur le rognage</span><span class="sxs-lookup"><span data-stu-id="d2599-123">Restrictions on cropping</span></span>
<span data-ttu-id="d2599-124">La fonctionnalité de rognage est destinée à être manuelle.</span><span class="sxs-lookup"><span data-stu-id="d2599-124">The cropping feature is meant to be manual.</span></span> <span data-ttu-id="d2599-125">Vous devez charger votre vidéo d’entrée dans un outil d’édition approprié qui vous permet de sélectionner des images d’intérêt, de positionner le curseur pour déterminer les décalages du rectangle de rognage, de déterminer que la présélection d’encodage est réglée pour une vidéo en particulier, etc. Cette fonctionnalité n’est pas destinée à activer des éléments tels que la détection automatique et la suppression des bordures noires letterbox/pillarbox de votre vidéo d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d2599-125">You would need to load your input video into a suitable editing tool that lets you select frames of interest, position the cursor to determine offsets for the cropping rectangle, to determine the encoding preset that is tuned for that particular video, etc. This feature is not meant to enable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="d2599-126">Les contraintes suivantes s’appliquent à la fonctionnalité de rognage.</span><span class="sxs-lookup"><span data-stu-id="d2599-126">Following constraints apply to the cropping feature.</span></span> <span data-ttu-id="d2599-127">Si elles ne sont pas remplies, la tâche de codage peut échouer ou produire un résultat inattendu.</span><span class="sxs-lookup"><span data-stu-id="d2599-127">If these are not met, the encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="d2599-128">Les coordonnées et la taille du rectangle de rognage doivent tenir dans la vidéo d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d2599-128">The co-ordinates and size of the Crop rectangle have to fit within the input video</span></span>
2. <span data-ttu-id="d2599-129">Comme mentionné ci-dessus, la largeur et la hauteur dans les paramètres d’encodage doivent correspondre à la vidéo rognée.</span><span class="sxs-lookup"><span data-stu-id="d2599-129">As mentioned above, the Width & Height in the encode settings have to correspond to the cropped video</span></span>
3. <span data-ttu-id="d2599-130">Le rognage s’applique aux vidéos capturées en mode paysage (c’est-à-dire qu’il ne s’applique pas aux vidéos enregistrées avec un smartphone maintenu verticalement ou en mode portrait).</span><span class="sxs-lookup"><span data-stu-id="d2599-130">Cropping applies to videos captured in landscape mode (i.e. not applicable to videos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="d2599-131">Fonctionne mieux avec une vidéo progressive capturée avec des pixels carrés.</span><span class="sxs-lookup"><span data-stu-id="d2599-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="d2599-132">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="d2599-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="d2599-133">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="d2599-133">Next step</span></span>
<span data-ttu-id="d2599-134">Consultez les parcours d’apprentissage Azure Media Services pour en savoir plus sur les fonctionnalités exceptionnelles offertes par AMS.</span><span class="sxs-lookup"><span data-stu-id="d2599-134">See Azure Media Services learning paths to help you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
