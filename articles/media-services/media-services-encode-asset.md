---
title: "aaaOverview et comparaison d’Azure sur demande les encodeurs media | Documents Microsoft"
description: "Cette rubrique donne une vue d’ensemble des encodeurs multimédia à la demande Azure et les compare."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a>Vue d’ensemble et comparaison d’encodeurs multimédia à la demande Azure
## <a name="encoding-overview"></a>Vue d’ensemble de l’encodage
Azure Media Services propose plusieurs options pour l’encodage de hello de support dans le cloud de hello.

Lorsque vous démarrez avec Media Services, il est différence de hello toounderstand important entre les codecs et formats de fichier.
Les codecs sont des logiciels de hello qui implémente les algorithmes de compression/décompression hello tandis que les formats de fichier sont des conteneurs qui contiennent la vidéo de hello compressé.

Media Services fournit l’empaquetage dynamique qui vous permet de toodeliver votre vitesse de transmission adaptative MP4 ou Smooth Streaming encodé contenu de diffusion en continu des formats pris en charge par Media Services (MPEG DASH, HLS, Smooth Streaming) sans que vous ayez toore-package dans ces formats de diffusion en continu.

>[!NOTE]
>Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état. avantage tootake de [empaquetage dynamique](media-services-dynamic-packaging-overview.md), toodo, hello éléments suivants sont nécessaires :
>
>En outre, encoder votre fichier source dans un ensemble de fichiers MP4 ou de fichiers de diffusion en continu lisse à débit adaptatif (les étapes de codage hello sont décrites plus loin dans ce didacticiel).

Media Services prend en charge suivantes d’hello sur les encodeurs à la demande qui sont décrites dans cet article :

* [Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Media Encoder Premium Workflow](media-services-encode-asset.md#media-encoder-premium-workflow)

Cet article donne une vue d’ensemble de la demande des encodeurs de support et fournit des liens tooarticles qui fournissent des informations plus détaillées. rubrique de Hello compare également les encodeurs hello.

>[!NOTE]
>Par défaut, chaque compte Media Services peut avoir une tâche d’encodage active à la fois. Vous pouvez réserver les unités d’encodage qui vous permettent de toohave s’exécutant simultanément, un pour chaque unité d’encodage réservée que vous achetez plusieurs tâches d’encodage. Pour plus d’informations, consultez [Mise à l’échelle des unités d’encodage](media-services-scale-media-processing-overview.md).

## <a name="media-encoder-standard"></a>Media Encoder Standard
### <a name="how-toouse"></a>Comment toouse
[Comment tooencode avec Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a>Formats
[Formats et codecs](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a>Présélections
Encodeur de support Standard est configuré d’à l’aide d’une des présélections d’encodeur hello décrites [ici](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Métadonnées d’entrée et de sortie
Hello encodeurs des métadonnées d’entrée sont décrit [ici](media-services-input-metadata-schema.md).

Hello encodeurs sortie métadonnées décrit [ici](media-services-output-metadata-schema.md).

### <a name="generate-thumbnails"></a>Génération de miniatures
Pour plus d’informations, consultez [comment miniatures toogenerate à l’aide de Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).

### <a name="trim-videos-clipping"></a>Découpage de vidéos (extrait)
Pour plus d’informations, consultez [comment vidéos tootrim à l’aide de Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).

### <a name="create-overlays"></a>Création de superpositions
Pour plus d’informations, consultez [comment superpositions toocreate à l’aide de Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).

### <a name="see-also"></a>Voir aussi
[blog de Media Services Hello](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a>Media Encoder Premium Workflow
### <a name="overview"></a>Vue d'ensemble
[Présentation de l’encodage Premium dans Azure Media Services](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a>Comment toouse
Media Encoder Premium Workflow se configure à l’aide de flux de travail complexes. Fichiers de flux de travail peut être créés et mis à jour avec hello [le Concepteur de flux de travail](media-services-workflow-designer.md) outil.

[Comment tooUse Premium encodage dans Azure Media Services](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a>Problèmes connus
Si votre vidéo d’entrée ne contient pas de sous-titrage, hello de sortie Qu'actif contient toujours un fichier TTML vide.


## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Articles connexes
* [Exécution de tâches d’encodage avancées via la personnalisation des présélections Media Encoder Standard](media-services-custom-mes-presets-with-dotnet.md)
* [Quotas et limitations](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
