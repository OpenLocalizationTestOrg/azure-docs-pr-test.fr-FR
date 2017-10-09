---
title: codecs et formats de codage Standard aaaMedia
description: "Cette rubrique fournit une vue d’ensemble des codecs et formats Media Encoder Standard."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f334b1ce-2f56-4968-a019-f0a2b0016d9f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 51a67f372dff579383ffcfa988e8f4d38ad44a72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-formats-and-codecs"></a>Codecs et formats standard de l’encodeur multimédia
Ce document contient une liste des formats de fichier d’exportation que vous pouvez utiliser avec Media Encoder Standard hello plus commun d’importation.

## <a name="input-containerfile-formats"></a>Formats de conteneurs/fichiers d’entrée
| Formats de fichier (extensions de fichier) | Pris en charge |
| --- | --- | --- | --- |
| FLV (avec les codecs H.264 et AAC) (.flv) |Oui |
| MXF    (.mxf) |OUI |
| GXF    (.gxf) |OUI |
| MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg) |OUI |
| Windows Media Video (WMV)/ASF (.wmv, .asf) |OUI |
| AVI (8 bits/10 bits non compressé) (.avi) |OUI |
| MP4 (.mp4, .m4a, .m4v)/ISMV (.isma, .ismv) |OUI |
| [Microsoft Digital Video Recording (DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) (.dvr-ms) |OUI |
| Matroska/WebM (.mkv) |OUI |
| WAVE/WAV (.wav) |OUI |
| QuickTime (.mov) |Oui |

> [!NOTE]
> Ci-dessus est une liste des extensions de fichier hello plus courants. Media Encoder Standard prend en charge de nombreuses autres extensions (par exemple : .m2ts, .mpeg2video, .qt). Si vous essayez de tooencode un fichier et que vous obtenez un message d’erreur sur le format hello n’est ne pas pris en charge, veuillez fournir une rétroaction [ici](https://feedback.azure.com/forums/169396-media-services/category/144411-encoding-and-processing/).
> 
> 

### <a name="audio-formats-in-input-containers"></a>Formats audio dans des conteneurs d’entrée
Media Encoder Standard prend en charge le transport hello suivant formats audio dans des conteneurs d’entrée :

* Fichiers MXF, GXF et QuickTime contenant des pistes audio avec des échantillons Interleaved Stereo ou 5.1

ou

* Fichiers MXF, GXF et QuickTime où audio de hello est exécutée en tant que pistes PCM distinctes mais mappage de canal hello (toostereo ou 5.1) peut être déduit à partir des métadonnées du fichier hello

Notez qui prennent en charge pour le mappage d’explicite/fourni par l’utilisateur le canal sera fournie dans hello futur proche.

## <a name="input-video-codecs"></a>Codecs vidéo d’entrée
| Codecs vidéo d’entrée | Pris en charge |
| --- | --- | --- | --- |
| AVC 8/10 bits bits, des too4:2:2, y compris AVCIntra |8 bits 4:2:0 et 4:2:2 |
| Avid DNxHD (dans MXF) |OUI |
| DVCPro/DVCProHD (dans MXF) |OUI |
| Vidéo numérique (dans les fichiers AVI) |OUI |
| JPEG 2000 |Oui |
| MPEG-2 (profil de too422 et de niveau élevé, notamment les variantes telles que XDCAM, XDCAM HD, XDCAM IMX, CableLabs® et D10) |Profil de too422 |
| MPEG-1 |OUI |
| VC-1/WMV9 |OUI |
| Canopus HQ/HQX |Non |
| MPEG-4 partie 2 |OUI |
| [Theora](https://en.wikipedia.org/wiki/Theora) |OUI |
| YUV420 non compressé ou mezzanine |OUI |
| Apple ProRes 422 |OUI |
| Apple ProRes 422 LT |OUI |
| Apple ProRes 422 HQ |OUI |
| Apple ProRes Proxy |OUI |
| Apple ProRes 4444 |OUI |
| Apple ProRes 4444 XQ |OUI |

## <a name="input-audio-codecs"></a>Codecs audio d’entrée
| Codecs audio d’entrée | Pris en charge |
| --- | --- | --- | --- |
| AAC (AAC-LC, HE-AAC et AAC-HEv2 ; des too5.1) |Oui |
| MPEG Layer 2 |OUI |
| MP3 (MPEG-1 Audio Layer 3) |OUI |
| Windows Media Audio |OUI |
| WAV/PCM |OUI |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |OUI |
| [Opus](http://go.microsoft.com/fwlink/?LinkId=822667) |OUI |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |OUI |
| AMR (adaptive multi-rate) |OUI |
| AES (SMPTE 331M et 302M, AES3-2003) |Non |
| Dolby® E |Non |
| Dolby® Digital (AC3) |Non |
| Dolby® Digital Plus (E-AC3) |Non |

## <a name="output-formats-and-codecs"></a>Formats de sortie et codecs
Hello tableau suivant répertorie les hello codecs et formats de fichier pris en charge pour l’exportation.

| Format de fichier | Codec vidéo | Codec audio |
| --- | --- | --- |
| MP4  <br/><br/>(y compris les conteneurs MP4 à vitesses de transmission multiples) |H.264 (profils High, Main et Baseline) |AAC-LC, HE-AAC v1, HE-AAC v2 |
| MPEG2-TS |H.264 (profils High, Main et Baseline) |AAC-LC, HE-AAC v1, HE-AAC v2 |

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Voir aussi
[Encodage de contenu à la demande avec Azure Media Services](media-services-encode-asset.md)

[Comment tooencode avec Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md)

