---
title: "schéma de codage Standard aaaMedia | Documents Microsoft"
description: "rubrique de Hello donne une vue d’ensemble du schéma de Media Encoder Standard hello."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 4c060062-8ef2-41d9-834e-e81e8eafcf2e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 82bad27b9546f75557ac691ff148b46990647632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-schema"></a>Schéma Media Encoder Standard
Cette rubrique décrit certains des éléments de hello et types de schéma XML de hello sur lequel [prédéfinit Media Encoder Standard](media-services-mes-presets-overview.md) sont basées. rubrique de Hello donne l’explication des éléments et leurs valeurs valides. schéma complet de Hello est publié à une date ultérieure.  

## <a name="Preset"></a> Présélection (élément racine)
Définit une valeur prédéfinie d’encodage.  

### <a name="elements"></a>Éléments
| Nom | Type | Description |
| --- | --- | --- |
| **Encodage** |[Encodage](media-services-mes-schema.md#Encoding) |Élément racine, indique que les sources d’entrée hello toobe encodé. |
| **Sorties** |[Sorties](media-services-mes-schema.md#Output) |Collection de fichiers de sortie souhaités. |

### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **Version**<br/><br/> Requis |**xs:decimal** |version de présélection Hello. Hello restrictions suivantes s’appliquent : xs:fractionDigits valeur = « 1 » et xs:minInclusive value = « 1 » par exemple, **version = « 1.0 »**. |

## <a name="Encoding"></a> Encodage
Contient une séquence de hello suivant d’éléments.  

### <a name="elements"></a>Éléments
| Nom | Type | Description |
| --- | --- | --- |
| **H264Video** |[H264Video](media-services-mes-schema.md#H264Video) |Paramètres d’encodage vidéo H.264. |
| **AACAudio** |[AACAudio](media-services-mes-schema.md#AACAudio) |Paramètres d’encodage audio AAC. |
| **BmpImage** |[BmpImage](media-services-mes-schema.md#BmpImage) |Paramètres de l’image Bmp. |
| **PngImage** |[PngImage](media-services-mes-schema.md#PngImage) |Paramètres de l’image Png. |
| **JpgImage** |[JpgImage](media-services-mes-schema.md#JpgImage) |Paramètres de l’image Jpg. |

## <a name="H264Video"></a> H264Video
### <a name="elements"></a>Éléments
| Nom | Type | Description |
| --- | --- | --- |
| **TwoPass**<br/><br/> minOccurs="0" |**xs:boolean** |Actuellement, seul l’encodage en une étape est pris en charge. |
| **KeyFrameInterval**<br/><br/> minOccurs="0"<br/><br/> **default="00:00:02"** |**xs:time** |Détermine hello fixée l’espacement entre les frames IDR en unités de secondes. Également appelée durée de GOP tooas hello. Consultez **SceneChangeDetection** (ci-dessous) pour contrôler si hello encodeur peut s’écarter cette valeur. |
| **SceneChangeDetection**<br/><br/> minOccurs="0"<br/><br/> default=”false” |**xs:boolean** |Si set tootrue, les tentatives d’encodeur toodetect scène modifier dans la vidéo de hello et insère un cadre IDR. |
| **Complexité**<br/><br/> minOccurs="0"<br/><br/> default="Balanced" |**xs:string** |Contrôles hello compromis encoder la qualité de vitesse et de la vidéo. Peut être une des valeurs suivantes de hello : **vitesse**, **équilibré**, ou **qualité**<br/><br/> Par défaut : **Équilibré** |
| **SyncMode**<br/><br/> minOccurs="0" | |Cette fonctionnalité sera présentée dans les versions à venir. |
| **H264Layers**<br/><br/> minOccurs="0" |[H264Layers](media-services-mes-schema.md#H264Layers) |Collection de couches vidéo de sortie. |

### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **Condition** |**xs:string** | Lors de l’entrée de hello n’affiche aucune vidéo, vous pouvez choisir tooforce hello encodeur tooinsert une piste vidéo monochrome. toodo qui, à Condition d’utilisent = « InsertBlackIfNoVideoBottomLayerOnly » (tooinsert une vidéo avec uniquement le débit de la plus basse hello) ou une Condition = « InsertBlackIfNoVideo » (tooinsert une vidéo à tous les débits binaires de sortie). Pour plus d’informations, consultez [cette rubrique](media-services-advanced-encoding-with-mes.md#no_video) .|

## <a name="H264Layers"></a> H264Layers

Par défaut, si vous envoyez un encodeur toohello d’entrée qui contient uniquement des données audio et aucune vidéo, hello élément multimédia de sortie contiennent les fichiers avec des données audio uniquement. Certains lecteurs ne pourront peut-être toohandle ce flux de sortie. Vous pouvez utiliser de hello H264Video **InsertBlackIfNoVideo** attribut tooforce hello encodeur tooadd une sortie toohello de piste vidéo dans ce scénario. Pour plus d’informations, consultez [cette rubrique](media-services-advanced-encoding-with-mes.md#no_video) .
              
### <a name="elements"></a>Éléments
| Nom | Type | Description |
| --- | --- | --- |
| **H264Layer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[H264Layer](media-services-mes-schema.md#H264Layer) |Collection de couches H264. |

## <a name="H264Layer"></a> H264Layer
> [!NOTE]
> Limites vidéos sont basées sur les valeurs hello décrites dans hello [H264 niveaux](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Levels) table.  
> 
> 

### <a name="elements"></a>Éléments
| Nom | Type | Description |
| --- | --- | --- |
| **Profil**<br/><br/> minOccurs="0"<br/><br/> default=”Auto” |**xs:string** |Peut être de l’un des éléments suivants de hello **xs : String** valeurs : **automatique**, **base**, **principal**, **haute**. |
| **Niveau**<br/><br/> minOccurs="0"<br/><br/> default=”Auto” |**xs:string** | |
| **Bitrate**<br/><br/> minOccurs="0" |**xs:int** |vitesse de transmission Hello utilisé pour cette couche vidéo, spécifiée en Kbits/s. |
| **MaxBitrate**<br/><br/> minOccurs="0" |**xs:int** |Hello vitesse de transmission maximale utilisée pour cette couche vidéo, spécifiée en Kbits/s. |
| **BufferWindow**<br/><br/> minOccurs="0"<br/><br/> default="00:00:05" |**xs:time** |Longueur du tampon de vidéo hello. |
| **Largeur**<br/><br/> minOccurs="0" |**xs:int** |Largeur de hello sortie image vidéo, en pixels.<br/><br/> Notez qu’actuellement vous devez spécifier la largeur et la hauteur. avez besoin de nombres pairs de toobe Hello largeur et hauteur. |
| **Hauteur**<br/><br/> minOccurs="0" |**xs:int** |Hauteur de hello sortie image vidéo, en pixels.<br/><br/> Notez qu’actuellement vous devez spécifier la largeur et la hauteur. avez besoin de nombres pairs de toobe Hello largeur et hauteur.|
| **BFrames**<br/><br/> minOccurs="0" |**xs:int** |Nombre de trames B entre les trames de référence. |
| **ReferenceFrames**<br/><br/> minOccurs="0"<br/><br/> default=”3” |**xs:int** |Nombre de trames de référence dans un GOP. |
| **EntropyMode**<br/><br/> minOccurs="0"<br/><br/> default=”Cabac” |**xs:string** |Peut être une des valeurs suivantes de hello : **Cabac** et **Cavlc**. |
| **FrameRate**<br/><br/> minOccurs="0" |nombre rationnel |Détermine la fréquence d’images hello de sortie hello vidéo. Utilisez la valeur par défaut « 0/1 » toolet Bonjour encodeur utilisez Bonjour même fréquence d’images d’en tant qu’entrée de hello vidéo. Les valeurs autorisées sont toobe attendu courantes des fréquences d’images vidéo, comme indiqué ci-dessous. Cependant, toute valeur rationnelle est autorisée. Par exemple, 1/1 correspondrait à 1 i/s et serait valide.<br/><br/> - 12/1  (12 i/s)<br/><br/> - 15/1 (15 i/s)<br/><br/> - 24/1 (24 i/s)<br/><br/> - 24000/1001 (23,976 i/s)<br/><br/> - 25/1 (25 i/s)<br/><br/>  - 30/1 (30 i/s)<br/><br/> - 30000/1001 (29,97 i/s) <br/> <br/>**Remarque** si vous créez un paramètre prédéfini pour l’encodage de plusieurs débits, toutes les couches de hello présélection **doit** utilisation hello même valeur de fréquence d’images.|
| **AdaptiveBFrame**<br/><br/> minOccurs="0" |**xs:boolean** |Copie depuis l’encodeur multimédia Azure |
| **Tranches**<br/><br/> minOccurs="0"<br/><br/> default="0" |**xs:int** |Détermine le nombre de tranches dans lequel une trame est divisée. Nous vous recommandons d'utiliser la valeur par défaut. |

## <a name="AACAudio"></a> AACAudio
 Contient une séquence de hello suivant des éléments et des groupes.  

 Pour plus d’informations sur AAC, consultez [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding).  

### <a name="elements"></a>Éléments
| Nom | Type | Description |
| --- | --- | --- |
| **Profil**<br/><br/> minOccurs="0 "<br/><br/> default="AACLC" |**xs:string** |Peut être une des valeurs suivantes de hello : **AACLC**, **HEAACV1**, ou **HEAACV2**. |

### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **Condition** |**xs:string** |tooforce hello encodeur tooproduce un élément multimédia contenant une piste audio en mode silencieux lors de l’entrée ne contient aucune donnée audio, spécifier la valeur de « InsertSilenceIfNoAudio » hello.<br/><br/> Par défaut, si vous envoyez un encodeur toohello d’entrée qui contient uniquement, audio et vidéo aucun, hello élément multimédia de sortie contient des fichiers qui contiennent des données vidéo uniquement. Certains lecteurs ne pourront peut-être toohandle ce flux de sortie. Vous pouvez utiliser cette tooadd d’encodeur de paramètre tooforce hello une sortie toohello de piste audio en mode silencieux dans ce scénario. |

### <a name="groups"></a>Groupes
| Référence | Description |
| --- | --- |
| [AudioGroup](media-services-mes-schema.md#AudioGroup)<br/><br/> minOccurs="0" |Consultez la description de [AudioGroup](media-services-mes-schema.md#AudioGroup) tooknow hello nombre approprié de canaux, taux d’échantillonnage et le taux de bits qui peut être défini pour chaque profil. |

## <a name="AudioGroup"></a> AudioGroup
Pour plus d’informations sur les valeurs qui sont valides pour chaque profil, consultez la table « Détails du codec Audio » hello qui suit.  

### <a name="elements"></a>Éléments
| Nom | Type | Description |
| --- | --- | --- |
| **Canaux**<br/><br/> minOccurs="0" |**xs:int** |nombre de Hello de canaux audio encodés. les options valides sont Hello suivantes : 1, 2, 5, 6 et 8.<br/><br/> Par défaut  : 2. |
| **SamplingRate**<br/><br/> minOccurs="0" |**xs:int** |taux d’échantillonnage audio Hello, spécifiée en Hz. |
| **Bitrate**<br/><br/> minOccurs="0" |**xs:int** |vitesse de transmission Hello utilisé lors de l’encodage audio de hello, spécifié en Kbits/s. |

### <a name="audio-codec-details"></a>Détails du codec audio
Codec audio|Détails  
-----------------|---  
**AACLC**|1:<br/><br/> - 11025 : 8 &lt;= bitrate &lt; 16<br/><br/> - 12000 : 8 &lt;= bitrate &lt; 16<br/><br/> - 16000 : 8 &lt;= bitrate &lt;32<br/><br/>- 22050 : 24 &lt;= bitrate &lt; 32<br/><br/> - 24000 : 24 &lt;= bitrate &lt; 32<br/><br/> - 32000 : 32 &lt;= bitrate &lt;= 192<br/><br/> - 44100 : 56 &lt;= bitrate &lt;= 288<br/><br/> - 48000 : 56 &lt;= bitrate &lt;= 288<br/><br/> - 88200 : 128 &lt;= bitrate &lt;= 288<br/><br/> - 96000 : 128 &lt;= bitrate &lt;= 288<br/><br/> 2 :<br/><br/> - 11025 : 16 &lt;= bitrate &lt; 24<br/><br/> - 12000 : 16 &lt;= bitrate &lt; 24<br/><br/> - 16000 : 16 &lt;= bitrate &lt; 40<br/><br/> - 22050 : 32 &lt;= bitrate &lt; 40<br/><br/> - 24000 : 32 &lt;= bitrate &lt; 40<br/><br/> - 32000 :  40 &lt;= bitrate &lt;= 384<br/><br/> - 44100 : 96 &lt;= bitrate &lt;= 576<br/><br/> - 48000 : 96 &lt;= bitrate &lt;= 576<br/><br/> - 88200 : 256 &lt;= bitrate &lt;= 576<br/><br/> - 96000 : 256 &lt;= bitrate &lt;= 576<br/><br/> 5/6:<br/><br/> - 32000 : 160 &lt;= bitrate &lt;= 896<br/><br/> - 44100 : 240 &lt;= bitrate &lt;= 1024<br/><br/> - 48000 : 240 &lt;= bitrate &lt;= 1024<br/><br/> - 88200 : 640 &lt;= bitrate &lt;= 1024<br/><br/> - 96000 : 640 &lt;= bitrate &lt;= 1024<br/><br/> 8:<br/><br/> - 32000 : 224 &lt;= bitrate &lt;= 1024<br/><br/> - 44100 : 384 &lt;= bitrate &lt;= 1024<br/><br/> - 48000 : 384 &lt;= bitrate &lt;= 1024<br/><br/> - 88200 : 896 &lt;= bitrate &lt;= 1024<br/><br/> - 96000 : 896 &lt;= bitrate &lt;= 1024  
**HEAACV1**|1:<br/><br/> - 22050 : bitrate = 8<br/><br/> - 24000 : 8 &lt;= bitrate &lt;= 10<br/><br/> - 32000 : 12 &lt;= bitrate &lt;= 64<br/><br/> - 44100 : 20 &lt;= bitrate &lt;= 64<br/><br/> - 48000 : 20 &lt;= bitrate &lt;= 64<br/><br/> - 88200 : bitrate = 64<br/><br/> 2 :<br/><br/> - 32000 : 16 &lt;= bitrate &lt;= 128<br/><br/> - 44100 : 16 &lt;= bitrate &lt;= 128<br/><br/> - 48000 : 16 &lt;= bitrate &lt;= 128<br/><br/> - 88200 : 96 &lt;= bitrate &lt;= 128<br/><br/> - 96000 : 96 &lt;= bitrate &lt;= 128<br/><br/> 5/6:<br/><br/> - 32000 : 64 &lt;= bitrate &lt;= 320<br/><br/> - 44100 : 64 &lt;= bitrate &lt;= 320<br/><br/> - 48000 : 64 &lt;= bitrate &lt;= 320<br/><br/> - 88200 : 256 &lt;= bitrate &lt;= 320<br/><br/> - 96000 : 256 &lt;= bitrate &lt;= 320<br/><br/> 8:<br/><br/> - 32000 : 96 &lt;= bitrate &lt;= 448<br/><br/> - 44100 : 96 &lt;= bitrate &lt;= 448<br/><br/> - 48000 : 96 &lt;= bitrate &lt;= 448<br/><br/> - 88200 : 384 &lt;= bitrate &lt;= 448<br/><br/> - 96000 : 384 &lt;= bitrate &lt;= 448  
**HEAACV2**|2 :<br/><br/> - 22050 : 8 &lt;= bitrate &lt;= 10<br/><br/> - 24000 : 8 &lt;= bitrate &lt;= 10<br/><br/> - 32000 : 12 &lt;= bitrate &lt;= 64<br/><br/> - 44100 : 20 &lt;= bitrate &lt;= 64<br/><br/> - 48000 : 20 &lt;= bitrate &lt;= 64<br/><br/> - 88200 : 64 &lt;= bitrate &lt;= 64  
  

## <a name="Clip"></a> Séquence
### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **StartTime** |**xs:duration** |Spécifie l’heure de début hello d’une présentation. valeur de Hello de StartTime doit toomatch hello des horodateurs absolu de la vidéo d’entrée de hello. Par exemple, si hello du premier frame de la vidéo d’entrée de hello a un horodateur de 12:00:10.000, StartTime doit être au moins 12:00:10.000 ou supérieur. |
| **Durée** |**xs:duration** |Spécifie la durée hello d’une présentation (par exemple, l’apparence d’une superposition vidéo de hello). |

## <a name="Output"></a> Sortie
### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **FileName** |**xs:string** |nom Hello hello du fichier de sortie.<br/><br/> Vous pouvez utiliser les macros décrits dans hello suivant des noms de fichiers de sortie table toobuild hello. Par exemple :<br/><br/> **"Outputs": [      {       "FileName": "{Basename}*{Resolution}*{Bitrate}.mp4",       "Format": {         "Type": "MP4Format"       }     }   ]** |

### <a name="macros"></a>Macros
| Macro | Description |
| --- | --- |
| **{Basename}** |Si vous effectuez le codage de la demande (VOD), hello {Basename} est hello les 32 premiers caractères de la propriété de AssetFile.Name hello du fichier primaire de hello dans l’élément multimédia d’entrée de hello.<br/><br/> Si la ressource en entrée hello est une archive en direct, puis hello {Basename} est dérivée des attributs de trackName hello dans le manifeste de serveur hello. Si vous soumettez un travail d’un sous-élément à l’aide de hello TopBitrate, comme dans : « < VideoStream\>TopBitrate < / VideoStream\>», fichier de sortie hello contient vidéo, puis hello {Basename} est hello les 32 premiers caractères de trackName hello Hello couche de vidéo avec un débit binaire plus élevé de hello.<br/><br/> Si à la place vous soumettez un travail d’un sous-élément à l’aide de toutes les vitesses de transmission hello d’entrée, tels que « < VideoStream\>* < / VideoStream\>», fichier de sortie hello contient vidéo, puis {Basename} est hello tout d’abord de 32 caractères de trackName hello de couche de vidéo Hello correspondante. |
| **{Codec}** |Mappe trop « H264 » pour la vidéo et « AAC » pour l’audio. |
| **{Bitrate}** |Hello vidéo débit cible si fichier de sortie hello contient vidéo et audio ou vitesse de transmission audio cible si le fichier de sortie hello contient uniquement des données audio. valeur de Hello utilisée est à débit binaire hello en Kbits/s. |
| **{Channel}** |Nombre de canaux audio si le fichier de hello contient des données audio. |
| **{Width}** |Largeur de hello vidéo, en pixels, dans le fichier de sortie hello, si les fichiers hello contient la vidéo. |
| **{Height}** |Hauteur de hello vidéo, en pixels, dans le fichier de sortie hello, si les fichiers hello contient la vidéo. |
| **{Extension}** |Hérite de hello propriété « Type » pour le fichier de sortie hello. nom de fichier de sortie Hello aura une extension qui fait partie de : « mp4 », « ts », « jpg », « png » ou « bmp ». |
| **{Index}** |Obligatoire pour la miniature. Ne doit être présent qu’une seule fois. |

## <a name="Video"></a> Vidéo (le type complexe hérite de Codec)
### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **Start** |**xs:string** | |
| **Étape** |**xs:string** | |
| **Plage** |**xs:string** | |
| **PreserveResolutionAfterRotation** |**xs:boolean** |Pour une explication détaillée, consultez hello suivant la section : [PreserveResolutionAfterRotation](media-services-mes-schema.md#PreserveResolutionAfterRotation) |

### <a name="PreserveResolutionAfterRotation"></a> PreserveResolutionAfterRotation
Il est recommandé d’indicateur de PreserveResolutionAfterRotation toouse hello en association avec des valeurs de résolution exprimés en termes de pourcentage (largeur = « 100 % », Height = « 100 % »).  

Par défaut, hello encoder les paramètres de résolution (largeur, hauteur) Bonjour Media Encoder Standard (MES) prédéfinis sont ciblées sur les vidéos avec rotation de 0 degrés. Par exemple, si votre vidéo d’entrée est 1280 x 720 avec zéro degré de rotation, puis paramètres prédéfinis hello Assurez-vous que sortie de hello dispose hello même résolution. Voir l’image ci-dessous.  

![MESRoation1](./media/media-services-shemas/media-services-mes-roation1.png) 

Toutefois, cela signifie que si la vidéo d’entrée de hello a été capturée avec rotation de zéro (par exemple). un smartphone ou tablette détenus verticalement), puis MES par défaut s’appliqueront hello coder la résolution d’entrée vidéo toohello de paramètres (largeur, hauteur), puis compenser rotation de hello. Par exemple, voir l’image de hello ci-dessous. Hello présélection utilise la largeur = « 100 % », Height = « 100 % », MES interprète comme nécessitant hello sortie toobe 1280 pixels de largeur et 720 pixels de hauteur. Après rotation vidéo de hello, il puis réduit hello image toofit dans cette fenêtre, entraînant des zones de toopillar-box sur hello gauche et droite.  

![MESRoation2](./media/media-services-shemas/media-services-mes-roation2.png) 

Si hello ci-dessus n’est pas un comportement de hello souhaité, vous pouvez rendre utiliser Hello PreserveResolutionAfterRotation indicateur et définir trop « true » (valeur par défaut est « false »). Par conséquent, si votre prédéfini a une largeur = « 100 % », hauteur = « 100 % » et PreserveResolutionAfterRotation défini trop « true », une vidéo d’entrée qui est 1280 pixels de large et 720 pixels en hauteur avec une rotation de 90 degrés génère une sortie avec zéro degré de rotation, mais 720 pixels de larges et 1280 pixels de hauteur. Voir l’image de hello ci-dessous.  

![MESRoation3](./media/media-services-shemas/media-services-mes-roation3.png) 

## <a name="FormatGroup"></a> FormatGroup (groupe)
### <a name="elements"></a>Éléments
| Nom | Type | Description |
| --- | --- | --- |
| **BmpFormat** |**BmpFormat** | |
| **PngFormat** |**PngFormat** | |
| **JpgFormat** |**JpgFormat** | |

## <a name="BmpLayer"></a> BmpLayer
### <a name="element"></a>Élément
| Nom | Type | Description |
| --- | --- | --- |
| **Largeur**<br/><br/> minOccurs="0" |**xs:int** | |
| **Hauteur**<br/><br/> minOccurs="0" |**xs:int** | |

### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="PngLayer"></a> PngLayer
### <a name="element"></a>Élément
| Nom | Type | Description |
| --- | --- | --- |
| **Largeur**<br/><br/> minOccurs="0" |**xs:int** | |
| **Hauteur**<br/><br/> minOccurs="0" |**xs:int** | |

### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="JpgLayer"></a> JpgLayer
### <a name="element"></a>Élément
| Nom | Type | Description |
| --- | --- | --- |
| **Largeur**<br/><br/> minOccurs="0" |**xs:int** | |
| **Hauteur**<br/><br/> minOccurs="0" |**xs:int** | |
| **Qualité**<br/><br/> minOccurs="0" |**xs:int** |Valeurs valides : 1 (moins bonne) - 100 (meilleure) |

### <a name="attributes"></a>Attributs
| Nom | Type | Description |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="PngLayers"></a> PngLayers
### <a name="elements"></a>Éléments
| Nom | Type | Description |
| --- | --- | --- |
| **PngLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[PngLayer](media-services-mes-schema.md#PngLayer) | |

## <a name="BmpLayers"></a> BmpLayers
### <a name="elements"></a>Éléments
| Nom | Type | Description |
| --- | --- | --- |
| **BmpLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[BmpLayer](media-services-mes-schema.md#BmpLayer) | |

## <a name="JpgLayers"></a> JpgLayers
### <a name="elements"></a>Éléments
| Nom | Type | Description |
| --- | --- | --- |
| **JpgLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[JpgLayer](media-services-mes-schema.md#JpgLayer) | |

## <a name="BmpImage"></a> BmpImage (le type complexe hérite de Video)
### <a name="elements"></a>Éléments
| Nom | Type | Description |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Couches PNG |

## <a name="JpgImage"></a> JpgImage (le type complexe hérite de Video)
### <a name="elements"></a>Éléments
| Nom | Type | Description |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Couches PNG |

## <a name="PngImage"></a> PngImage (le type complexe hérite de Video)
### <a name="elements"></a>Éléments
| Nom | Type | Description |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Couches PNG |

## <a name="examples"></a>Exemples
Pour voir des exemples de présélections XML qui sont générées conformément à ce schéma, consultez [Présélections de tâches pour MES (Media Encoder Standard)](media-services-mes-presets-overview.md).

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

