---
title: "aaaMedia Workflow d’encodeur Premium codecs et formats | Documents Microsoft"
description: "Cette rubrique offre une vue d’ensemble des codecs et formats de Media Encoder Premium Workflow"
services: media-services
documentationcenter: 
author: juliako
manager: erik43
editor: 
ms.assetid: b197fce8-3b9b-4189-8d08-486810c0426f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: e781384ca8f08926f00c83b6710fd413ce2a3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a>Codecs et formats de Media Encoder Premium Workflow
> [!NOTE]
> Pour les questions relatives à Encoder Premium, envoyez un e-mail à mepd sur Microsoft.com.
> 
> Le processeur multimédia Media Encoder Premium Workflow présenté dans cette rubrique n’est pas disponible en Chine. 
> 
> 

Ce document contient une liste de formats de fichier d’entrée et de sortie et les codecs sont pris en charge par la version préliminaire publique de hello Hello **Workflow d’encodeur multimédia Premium** encodeur.

[Codecs et formats d’entrée de Media Encoder Premium Workflow](#input_formats)

[Codecs et formats de sortie de Media Encoder Premium Workflow](#output_formats)

**Media Encoder Premium Workflow** prend en charge le sous-titrage décrit dans [cette](#closed_captioning) section 

## <a id="input_formats"></a>Codecs et formats d’entrée de Media Encoder Premium Workflow
Hello après section répertorie hello codecs et formats de fichier qui prend en charge par ce processeur multimédia en tant qu’entrée.

### <a name="input-containerfile-formats"></a>Formats de conteneurs/fichiers d’entrée
* Adobe® Flash® F4V
* MXF/SMPTE 377M
* GXF
* MPEG-2 Transport Streams
* MPEG-2 Program Streams
* MPEG-4/MP4
* Windows Media/ASF
* AVI (8 bits/10 bits non compressé)

### <a name="input-video-codecs"></a>Codecs vidéo d’entrée
* AVC 8/10 bits bits, des too4:2:2, y compris AVCIntra
* Avid DNxHD (dans MXF)
* DVCPro/DVCProHD (dans MXF)
* JPEG2000
* MPEG-2 (profil de too422 et de niveau élevé, notamment les variantes telles que XDCAM, XDCAM HD, XDCAM IMX, CableLabs® et D10)
* MPEG-1
* Windows Media Video/VC-1

### <a name="input-audio-codecs"></a>Codecs audio d’entrée
* AES (SMPTE 331M et 302M, AES3-2003)
* Dolby® E
* Dolby® Digital (AC3)
* AAC (AAC-LC, HE-AAC et AAC-HEv2 ; des too5.1)
* MPEG Layer 2
* MP3 (MPEG-1 Audio Layer 3)
* Windows Media Audio
* WAV/PCM

## <a id="output_format"></a>Codecs et formats de sortie de Media Encoder Premium Workflow
Hello section suivante répertorie hello codecs et formats de fichier pris en charge en tant que sortie à partir de ce processeur multimédia.

### <a name="output-containerfile-formats"></a>Formats de conteneurs/fichiers de sortie
* Adobe® Flash® F4V
* MXF (OP1a, XDCAM et AS02)
* DPP (y compris AS11)
* GXF
* MPEG-4/MP4
* Windows Media/ASF
* AVI (8 bits/10 bits non compressé)
* Format de fichier Smooth Streaming (PIFF 1.3)
* MPEG-TS 

### <a name="output-video-codecs"></a>Codecs vidéo de sortie
* AVC (H.264 ; 8 bits ; jusqu'à tooHigh profil, niveau 5.2 ; HD Ultra de 4 Ko ; AVC Intra)
* Avid DNxHD (dans MXF)
* DVCPro/DVCProHD (dans MXF)
* MPEG-2 (profil de too422 et de niveau élevé, notamment les variantes telles que XDCAM, XDCAM HD, XDCAM IMX, CableLabs® et D10)
* MPEG-1
* Windows Media Video/VC-1
* Création de miniatures JPEG

### <a name="output-audio-codecs"></a>Codecs audio de sortie
* AES (SMPTE 331M et 302M, AES3-2003)
* Dolby® Digital (AC3)
* Dolby® Digital Plus (E-AC3) des too7.1
* AAC (AAC-LC, HE-AAC et AAC-HEv2 ; des too5.1)
* MPEG Layer 2
* MP3 (MPEG-1 Audio Layer 3)
* Windows Media Audio

>[!NOTE]
>Si vous codez tooDolby® Digital (AC3), hello sortie peuvent uniquement être écrites dans un fichier MP4 ISO.

## <a id="closed_captioning"></a>Prise en charge du sous-titrage
En entrée, **Media Encoder Premium Workflow** prend en charge :

1. Fichiers sous contrôle de code source (SCC)
2. Fichiers SMPTE-TT
3. CEA-608/CEA-708 : transporté comme données utilisateur (messages SEI de flux élémentaires H.264, ATSC/53, SCTE20) ou comme données connexes dans des fichiers MXF/GXF
4. Fichiers de sous-titres STL

En sortie, hello options suivantes est disponible :

1. CEA-608 tooCEA-708 traduction
2. Transition CEA-608/CEA-708 (incorporé dans des messages SEI de flux élémentaires H.264 ou transporté comme données connexes dans des fichiers MXF)
3. SCC
4. SMPTE Timed Text (de la source CEA-608 par SMPTE RP2052 ; création de fichiers DFXP incluse)
5. Fichier de sous-titre SRT
6. Flux de sous-titres DVB

Remarque : toutes les hello au-dessus de formats de sortie sont pris en charge pour la remise par diffusion en continu dans Azure Media Services.

## <a name="known-issues"></a>Problèmes connus
Si votre vidéo d’entrée ne contient pas de sous-titrage, hello de sortie Qu'actif contient toujours un fichier TTML vide. 

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

