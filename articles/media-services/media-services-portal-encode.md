---
title: "aaaEncode un élément multimédia à l’aide de Media Encoder Standard avec hello portail Azure | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes hello de codage d’un élément multimédia à l’aide de Media Encoder Standard avec hello portail Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a>Encoder un élément multimédia à l’aide de Media Encoder Standard avec hello portail Azure
> [!NOTE]
> toocomplete ce didacticiel, vous avez besoin d’un compte Azure. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Lorsque vous travaillez avec un des scénarios les plus courants de hello transmet les clients tooyour de diffusion en continu à débit adaptatif Azure Media Services. Media Services prend en charge hello suivant des technologies de diffusion en continu de fichiers à débit adaptatif : HTTP Live Streaming (HLS), la diffusion en continu lisse, MPEG DASH. tooprepare vos vidéos pour de diffusion en continu à débit adaptatif, vous devez tooencode votre source vidéo dans des fichiers de débits. Vous devez utiliser hello **Media Encoder Standard** encodeur tooencode vos vidéos.  

Media Services fournit également un empaquetage dynamique qui vous permet de toodeliver votre MP4s débits Bonjour suivant les formats de diffusion en continu : MPEG DASH, HLS, Smooth Streaming, sans que vous ayez toore-package dans ces formats de diffusion en continu. Avec l’empaquetage dynamique vous devez uniquement toostore et payer pour les fichiers hello dans un seul format de stockage et les Services de support pour la génération et fournit hello de réponse appropriée en fonction des demandes d’un client.

tootake parti de l’empaquetage dynamique, vous devez tooencode votre fichier source en un ensemble de fichiers MP4 à plusieurs débits (étapes de codage hello sont décrites plus loin dans cette section).

support tooscale du traitement, consultez [cela](media-services-portal-scale-media-processing.md) rubrique.

## <a name="encode-with-hello-azure-portal"></a>Encoder avec hello portail Azure
Cette section décrit les étapes à suivre tooencode votre contenu avec Media Encoder Standard hello.

1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.
2. Bonjour **paramètres** fenêtre, sélectionnez **actifs**.  
3. Bonjour **actifs** fenêtre, asset hello select que vous aimeriez tooencode.
4. Hello de presse **Encode** bouton.
5. Bonjour **encoder un élément multimédia** fenêtre, processeur de « Media Encoder Standard » hello select et une présélection. Pour plus d’informations sur les présélections, consultez les articles [Utilisation d’Azure Media Encoder Standard pour générer automatiquement une échelle des vitesses de transmission](media-services-autogen-bitrate-ladder-with-mes.md) et [Présélections de travaux pour MES (Media Encoder Standard)](media-services-mes-presets-overview.md). Si vous envisagez toocontrol quelle valeur prédéfinie d’encodage est utilisée, gardez cela à l’esprit : il est important de tooselect hello prédéfini qui convient le mieux pour votre vidéo d’entrée. Par exemple, si vous connaissez votre vidéo d’entrée d’une résolution de 1920 x 1080 pixels, vous pouvez utiliser hello « H264 plusieurs débits binaires 1080p » prédéfini. Si vous disposez d’une vidéo basse résolution (640 x 360), il est préférable de ne pas utiliser la présélection « H264 – Vitesse de transmission multiple – 1 080 pixels ».
   
   Pour faciliter la gestion, vous avez une option de modification de nom hello de ressource en sortie hello et nom hello du travail de hello.
   
   ![Encoder des éléments multimédias](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. Appuyez sur **Créer**.

## <a name="next-step"></a>Étape suivante
Vous pouvez surveiller la progression de la tâche encodage avec hello portail Azure, comme décrit dans [cela](media-services-portal-check-job-progress.md) l’article.  

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

