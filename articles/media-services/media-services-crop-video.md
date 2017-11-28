---
title: "vidéos de toocrop aaaHow avec Media Encoder Standard - Azure | Documents Microsoft"
description: "Cet article explique comment les vidéos toocrop avec Media Encoder Standard."
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
ms.openlocfilehash: 2b4ac3d96228b93c890a38c57c4913988de1e8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="79722-103">Rogner des vidéos avec l’encodeur multimédia standard</span><span class="sxs-lookup"><span data-stu-id="79722-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="79722-104">Vous pouvez utiliser Media Encoder Standard (MES) toocrop votre entrée vidéo.</span><span class="sxs-lookup"><span data-stu-id="79722-104">You can use Media Encoder Standard (MES) toocrop your input video.</span></span> <span data-ttu-id="79722-105">Rognage consiste hello en sélectionnant une fenêtre rectangulaire dans les images vidéo hello et encodage simplement les pixels hello dans cette fenêtre.</span><span class="sxs-lookup"><span data-stu-id="79722-105">Cropping is hello process of selecting a rectangular window within hello video frame, and encoding just hello pixels within that window.</span></span> <span data-ttu-id="79722-106">Hello suivant schéma permet d’illustrer le processus de hello.</span><span class="sxs-lookup"><span data-stu-id="79722-106">hello following diagram helps illustrate hello process.</span></span>

![Rogner une vidéo](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="79722-108">Vous disposez en tant qu’entrée une vidéo qui a une résolution de 1920 x 1080 pixels (rapport 16:9), mais n’a noires (zones pilier) sur hello gauche et droite, afin que seuls une fenêtre 4:3 ou 1440 x 1080 pixels contient vidéo active.</span><span class="sxs-lookup"><span data-stu-id="79722-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at hello left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="79722-109">Vous pouvez utiliser MES toocrop ou modifier des barres de hello noir et coder la région de 1440 x 1080 hello.</span><span class="sxs-lookup"><span data-stu-id="79722-109">You can use MES toocrop or edit out hello black bars, and encode hello 1440x1080 region.</span></span>

<span data-ttu-id="79722-110">Rognage dans MES étant une étape de prétraitement, les paramètres de rognage hello dans la valeur prédéfinie d’encodage hello s’appliquent toohello de vidéo d’entrée d’origine.</span><span class="sxs-lookup"><span data-stu-id="79722-110">Cropping in MES is a pre-processing stage, so hello cropping parameters in hello encoding preset apply toohello original input video.</span></span> <span data-ttu-id="79722-111">L’encodage est à un stade ultérieur, et les paramètres de largeur/hauteur de hello s’appliquent toohello *traité au préalable* vidéo et toohello pas de vidéo d’origine.</span><span class="sxs-lookup"><span data-stu-id="79722-111">Encoding is a subsequent stage, and hello width/height settings apply toohello *pre-processed* video, and not toohello original video.</span></span> <span data-ttu-id="79722-112">Lors de la conception de votre présélection toodo, hello éléments suivants sont nécessaires : (un), sélectionnez les paramètres de culture hello hello de vidéo d’entrée d’origine et (b), sélectionnez votre encoder des paramètres en fonction de hello rognée vidéo.</span><span class="sxs-lookup"><span data-stu-id="79722-112">When designing your preset you need toodo hello following: (a) select hello crop parameters based on hello original input video, and (b) select your encode settings based on hello cropped video.</span></span> <span data-ttu-id="79722-113">Si vous ne correspondent pas votre Encoder toohello paramètres rognée vidéo, la sortie de hello ne sera pas comme prévu.</span><span class="sxs-lookup"><span data-stu-id="79722-113">If you do not match your encode settings toohello cropped video, hello output will not be as you expect.</span></span>

<span data-ttu-id="79722-114">Hello [suivant](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) rubrique indique comment toocreate un travail d’encodage avec MES et comment toospecify personnalisé prédéfini pour hello tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="79722-114">hello [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how toocreate an encoding job with MES and how toospecify a custom preset for hello encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="79722-115">Création d’une présélection personnalisée</span><span class="sxs-lookup"><span data-stu-id="79722-115">Creating a custom preset</span></span>
<span data-ttu-id="79722-116">Dans l’exemple hello hello illustré :</span><span class="sxs-lookup"><span data-stu-id="79722-116">In hello example shown in hello diagram:</span></span>

1. <span data-ttu-id="79722-117">L’entrée d’origine est 1920 x 1080.</span><span class="sxs-lookup"><span data-stu-id="79722-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="79722-118">Il doit toobe rognée sortie tooan de 1440 x 1080, qui est centrée dans le cadre d’entrée de hello</span><span class="sxs-lookup"><span data-stu-id="79722-118">It needs toobe cropped tooan output of 1440x1080, which is centered in hello input frame</span></span>
3. <span data-ttu-id="79722-119">Cela implique un décalage X de (1920 – 1440)/2 = 240 et un décalage Y de zéro.</span><span class="sxs-lookup"><span data-stu-id="79722-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="79722-120">Hello largeur et hauteur du rectangle de rognage hello sont respectivement 1440 et 1080,</span><span class="sxs-lookup"><span data-stu-id="79722-120">hello Width and Height of hello Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="79722-121">Bonjour étape coder, hello poser est tooproduce trois couches, sont respectivement les résolutions 1440 x 1080, 960 x 720 et 480 x 360,</span><span class="sxs-lookup"><span data-stu-id="79722-121">In hello encode stage, hello ask is tooproduce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="79722-122">Présélection JSON</span><span class="sxs-lookup"><span data-stu-id="79722-122">JSON preset</span></span>
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="79722-123">Restrictions sur le rognage</span><span class="sxs-lookup"><span data-stu-id="79722-123">Restrictions on cropping</span></span>
<span data-ttu-id="79722-124">Hello rogner la fonction est censée toobe manuel.</span><span class="sxs-lookup"><span data-stu-id="79722-124">hello cropping feature is meant toobe manual.</span></span> <span data-ttu-id="79722-125">Vous devez tooload votre entrée vidéo dans un outil d’édition approprié qui vous permet de sélectionner les images d’intérêt, positionner hello curseur toodetermine offsets pour hello rectangle de rognage, toodetermine hello valeur prédéfinie d’encodage qui est réglé pour que des vidéos, etc. particulier. Cette fonctionnalité n’est pas destinée tooenable des éléments tels que : détection automatique et la suppression des bordures noir letterbox/pillarbox de votre entrée vidéo.</span><span class="sxs-lookup"><span data-stu-id="79722-125">You would need tooload your input video into a suitable editing tool that lets you select frames of interest, position hello cursor toodetermine offsets for hello cropping rectangle, toodetermine hello encoding preset that is tuned for that particular video, etc. This feature is not meant tooenable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="79722-126">Les contraintes suivantes s’appliquent à toohello rogner la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="79722-126">Following constraints apply toohello cropping feature.</span></span> <span data-ttu-id="79722-127">Si elles ne sont pas remplies, hello encoder la tâche peut échouer ou produire une sortie inattendue.</span><span class="sxs-lookup"><span data-stu-id="79722-127">If these are not met, hello encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="79722-128">Hello les coordonnées et la taille du rectangle de rognage hello ont toofit au sein de la vidéo d’entrée de hello</span><span class="sxs-lookup"><span data-stu-id="79722-128">hello co-ordinates and size of hello Crop rectangle have toofit within hello input video</span></span>
2. <span data-ttu-id="79722-129">Comme indiqué ci-dessus, hello largeur et hauteur Bonjour Encoder paramètres ont toohello toocorrespond rognée vidéo</span><span class="sxs-lookup"><span data-stu-id="79722-129">As mentioned above, hello Width & Height in hello encode settings have toocorrespond toohello cropped video</span></span>
3. <span data-ttu-id="79722-130">Rognage s’applique toovideos capturée dans le mode paysage (autrement dit, non applicable toovideos enregistrés avec un smartphone maintenus verticalement ou en mode portrait)</span><span class="sxs-lookup"><span data-stu-id="79722-130">Cropping applies toovideos captured in landscape mode (i.e. not applicable toovideos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="79722-131">Fonctionne mieux avec une vidéo progressive capturée avec des pixels carrés.</span><span class="sxs-lookup"><span data-stu-id="79722-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="79722-132">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="79722-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="79722-133">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="79722-133">Next step</span></span>
<span data-ttu-id="79722-134">Consultez toohelp de chemins d’accès que vous en savoir plus sur les fonctionnalités offertes par AMS de formation Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="79722-134">See Azure Media Services learning paths toohelp you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
