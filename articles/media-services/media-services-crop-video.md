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
# <a name="crop-videos-with-media-encoder-standard"></a>Rogner des vidéos avec l’encodeur multimédia standard
Vous pouvez utiliser Media Encoder Standard (MES) toocrop votre entrée vidéo. Rognage consiste hello en sélectionnant une fenêtre rectangulaire dans les images vidéo hello et encodage simplement les pixels hello dans cette fenêtre. Hello suivant schéma permet d’illustrer le processus de hello.

![Rogner une vidéo](./media/media-services-crop-video/media-services-crop-video01.png)

Vous disposez en tant qu’entrée une vidéo qui a une résolution de 1920 x 1080 pixels (rapport 16:9), mais n’a noires (zones pilier) sur hello gauche et droite, afin que seuls une fenêtre 4:3 ou 1440 x 1080 pixels contient vidéo active. Vous pouvez utiliser MES toocrop ou modifier des barres de hello noir et coder la région de 1440 x 1080 hello.

Rognage dans MES étant une étape de prétraitement, les paramètres de rognage hello dans la valeur prédéfinie d’encodage hello s’appliquent toohello de vidéo d’entrée d’origine. L’encodage est à un stade ultérieur, et les paramètres de largeur/hauteur de hello s’appliquent toohello *traité au préalable* vidéo et toohello pas de vidéo d’origine. Lors de la conception de votre présélection toodo, hello éléments suivants sont nécessaires : (un), sélectionnez les paramètres de culture hello hello de vidéo d’entrée d’origine et (b), sélectionnez votre encoder des paramètres en fonction de hello rognée vidéo. Si vous ne correspondent pas votre Encoder toohello paramètres rognée vidéo, la sortie de hello ne sera pas comme prévu.

Hello [suivant](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) rubrique indique comment toocreate un travail d’encodage avec MES et comment toospecify personnalisé prédéfini pour hello tâche d’encodage. 

## <a name="creating-a-custom-preset"></a>Création d’une présélection personnalisée
Dans l’exemple hello hello illustré :

1. L’entrée d’origine est 1920 x 1080.
2. Il doit toobe rognée sortie tooan de 1440 x 1080, qui est centrée dans le cadre d’entrée de hello
3. Cela implique un décalage X de (1920 – 1440)/2 = 240 et un décalage Y de zéro.
4. Hello largeur et hauteur du rectangle de rognage hello sont respectivement 1440 et 1080,
5. Bonjour étape coder, hello poser est tooproduce trois couches, sont respectivement les résolutions 1440 x 1080, 960 x 720 et 480 x 360,

### <a name="json-preset"></a>Présélection JSON
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


## <a name="restrictions-on-cropping"></a>Restrictions sur le rognage
Hello rogner la fonction est censée toobe manuel. Vous devez tooload votre entrée vidéo dans un outil d’édition approprié qui vous permet de sélectionner les images d’intérêt, positionner hello curseur toodetermine offsets pour hello rectangle de rognage, toodetermine hello valeur prédéfinie d’encodage qui est réglé pour que des vidéos, etc. particulier. Cette fonctionnalité n’est pas destinée tooenable des éléments tels que : détection automatique et la suppression des bordures noir letterbox/pillarbox de votre entrée vidéo.

Les contraintes suivantes s’appliquent à toohello rogner la fonctionnalité. Si elles ne sont pas remplies, hello encoder la tâche peut échouer ou produire une sortie inattendue.

1. Hello les coordonnées et la taille du rectangle de rognage hello ont toofit au sein de la vidéo d’entrée de hello
2. Comme indiqué ci-dessus, hello largeur et hauteur Bonjour Encoder paramètres ont toohello toocorrespond rognée vidéo
3. Rognage s’applique toovideos capturée dans le mode paysage (autrement dit, non applicable toovideos enregistrés avec un smartphone maintenus verticalement ou en mode portrait)
4. Fonctionne mieux avec une vidéo progressive capturée avec des pixels carrés.

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Étape suivante
Consultez toohelp de chemins d’accès que vous en savoir plus sur les fonctionnalités offertes par AMS de formation Azure Media Services.  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
