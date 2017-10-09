---
title: "Présélections aaaTask pour MES (Media Encoder Standard) | Documents Microsoft"
description: "fournit les rubrique Hello et vue d’ensemble de présélections de tâches pour MES (Media Encoder Standard)."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: f243ed1c-ac9c-4300-a5f7-f092cf9853b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 56e098d6d8c8f84031421ec59f087f20370ba111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="task-presets-for-mes-media-encoder-standard"></a>Présélections de travaux pour MES (Media Encoder Standard)

**Media Encoder Standard** définit un ensemble de présélections d’encodage à utiliser lors de la création des travaux d’encodage. Il est recommandé de hello toouse « Diffusion adaptative en continu » prédéfini si vous souhaitez tooencode une vidéo de diffusion en continu avec Media Services. Lorsque vous spécifiez cette présélection, Media Encoder Standard [générera automatiquement une échelle des vitesses de transmission](media-services-autogen-bitrate-ladder-with-mes.md). 

Toutefois, si vous devez toocustomize une valeur prédéfinie d’encodage, vous devez prendre une des hello encodage Présélections définies dans cette section en tant que modèle pour personnaliser votre configuration. Pour obtenir des explications quelles chaque élément de ces moyens de paramètres prédéfinis et que les valeurs valides de hello pour chaque élément, consultez hello [schéma Media Encoder Standard](media-services-mes-schema.md) rubrique.  
  
> [!NOTE]
>  Lorsque vous utilisez une présélection de 4k encode, vous devez obtenir hello `S3` réservé de type d’unité. Pour plus d’informations, consultez [comment tooScale codage](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).  
  
Lorsque vous opérez avec Media Encoder Standard, la rotation est activée par défaut. Si votre vidéo a été enregistré sur un smartphone ou un autre périphérique mobile en mode Portrait, puis ces paramètres prédéfinis seront, par défaut, les faire pivoter tooencoding préalable de mode tooLandscape (à la différence, lorsque vous travaillez avec Azure Media Encoder, où la rotation de la vidéo est une opération manuelle, comme décrit dans [cela](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) blog, sous « Rotation vidéo »).  
  
Présélections disponibles :  
  
 [H264 – vitesse plusieurs 1080p – Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) génère un ensemble de 8 fichiers MP4 alignés GOP, allant des Kbits/s de too400 6000 Kbits/s et audio AAC 5.1.  
  
 [H264 plusieurs débits binaires 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) génère un ensemble de 8 fichiers MP4 alignés GOP, allant des Kbits/s de too400 6000 Kbits/s et audio AAC stéréo.  
  
 [Plusieurs h264 16 x 9 pour iOS](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) génère un ensemble de 8 fichiers MP4 alignés GOP, allant des Kbits/s de too200 8500 Kbits/s et audio AAC stéréo.  
  
 [H264 plusieurs débits binaires 16 x 9 SD – Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) produit un ensemble de 5 fichiers MP4 alignés GOP, allant des Kbits/s de too400 1900 Kbits/s et audio AAC 5.1.  
  
 [H264 plusieurs débits binaires 16 x 9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) produit un ensemble de 5 fichiers MP4 alignés GOP, allant des Kbits/s de too400 1900 Kbits/s et audio AAC stéréo.  
  
 [H264 plusieurs débits binaires 4K – Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) génère un ensemble de 12 fichiers MP4 alignés GOP, allant des 20000 Kbits/s de too1000 Kbits/s et audio AAC 5.1.  
  
 [H264 plusieurs débits binaires 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) génère un ensemble de 12 fichiers MP4 alignés GOP, allant des 20000 Kbits/s de too1000 Kbits/s et audio AAC stéréo.  
  
 [Plusieurs h264 4 x 3 pour iOS](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) génère un ensemble de 8 fichiers MP4 alignés GOP, allant des Kbits/s de too200 8500 Kbits/s et audio AAC stéréo.  
  
 [H264 plusieurs débits binaires 4 x 3 SD – Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) produit un ensemble de 5 fichiers MP4 alignés GOP, allant des Kbits/s de 1600 Kbits/s too400 et audio AAC 5.1.  
  
 [H264 plusieurs débits binaires 4 x 3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) produit un ensemble de 5 fichiers MP4 alignés GOP, allant des Kbits/s de 1600 Kbits/s too400 et audio AAC stéréo.  
  
 [H264 – vitesse plusieurs 720 pixels – Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) génère un ensemble de 6 fichiers MP4 alignés GOP, allant des Kbits/s de too400 3400 Kbits/s et audio AAC 5.1.  
  
 [H264 plusieurs débits binaires 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) génère un ensemble de 6 fichiers MP4 alignés GOP, allant des Kbits/s de too400 3400 Kbits/s et audio AAC stéréo.  
  
 [H264 - Vitesse de transmission unique - 1 080 pixels - Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md) produit un seul fichier MP4 avec une vitesse de transmission de 6 750 kbit/s, et de l’audio AAC 5.1.  
  
 [H264 - Vitesse de transmission unique - 1 080 pixels](media-services-mes-preset-H264-Single-Bitrate-1080p.md) produit un seul fichier MP4 avec une vitesse de transmission de 6 750 kbit/s, et de l’audio stéréo AAC.  
  
 [H264 - Vitesse de transmission unique - 4K - Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md) produit un seul fichier MP4 avec une vitesse de transmission de 18 000 kbit/s, et de l’audio AAC 5.1.  
  
 [H264 - Vitesse de transmission unique - 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md) produit un seul fichier MP4 avec une vitesse de transmission de 18 000 kbit/s, et de l’audio stéréo AAC.  
  
 [H264 - Vitesse de transmission unique - 4 x 3 SD - Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md) produit un seul fichier MP4 avec une vitesse de transmission de 1 800 kbit/s, et de l’audio AAC 5.1.  
  
 [H264 - Vitesse de transmission unique - 4 x 3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md) produit un seul fichier MP4 avec une vitesse de transmission de 1 800 kbit/s, et de l’audio stéréo AAC.  
  
 [H264 - Vitesse de transmission unique - 16 x 9 SD - Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md) produit un seul fichier MP4 avec une vitesse de transmission de 2 200 kbit/s, et de l’audio AAC 5.1.  
  
 [H264 - Vitesse de transmission unique - 16 x 9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md) produit un seul fichier MP4 avec une vitesse de transmission de 2 200 kbit/s, et de l’audio stéréo AAC.  
  
 [H264 - Vitesse de transmission unique - 720p - Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md) produit un seul fichier MP4 avec une vitesse de transmission de 4 500 kbit/s, et de l’audio AAC 5.1.  
  
 [H264 - Vitesse de transmission unique - 720p pour Android](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md) produit un seul fichier MP4 avec une vitesse de transmission de 2 000 kbit/s, et de l’audio stéréo AAC.  
  
 [H264 - Vitesse de transmission unique - 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md) produit un seul fichier MP4 avec une vitesse de transmission de 4 500 kbit/s, et de l’audio stéréo AAC.  
  
 [H264 - Vitesse de transmission unique haute qualité SD pour Android](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md) produit un seul fichier MP4 avec une vitesse de transmission de 500 kbit/s, et de l’audio stéréo AAC.  
  
 [H264 - Vitesse de transmission unique qualité faible SD pour Android](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md) produit un seul fichier MP4 avec une vitesse de transmission de 56 kbit/s, et de l’audio stéréo AAC.  
  
 Pour plus d’informations connexes tooMedia Services encodeurs, consultez [encodage à la demande avec Azure Media Services](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/).
