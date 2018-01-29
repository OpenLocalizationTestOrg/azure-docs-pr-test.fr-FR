---
title: "Encoder un actif multimédia à l’aide de Media Encoder Standard dans le portail Azure | Microsoft Docs"
description: "Ce didacticiel fournit les étapes à suivre pour l’encodage d’un actif multimédia à l’aide de Media Encoder Standard dans le portail Azure."
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
ms.openlocfilehash: ae5f4fd391cbf62b41d1a65f1d8107cefe3a5df3
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="encode-an-asset-by-using-media-encoder-standard-in-the-azure-portal"></a>Encoder un actif multimédia à l’aide de Media Encoder Standard dans le portail Azure

> [!NOTE]
> Pour suivre ce didacticiel, vous avez besoin d'un compte Azure. Pour plus d’informations, consultez la page [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Parmi les scénarios Azure Media Services les plus courants figure l’offre d’une technologie de streaming à débit adaptatif à vos clients. Media Services prend en charge les technologies de streaming à débit adaptatif suivantes : Apple HTTP Live Streaming (HLS), Microsoft Smooth Streaming et Dynamic Adaptive Streaming sur HTTP (DASH, aussi appelé MPEG-DASH). Pour préparer vos vidéos au streaming à débit adaptatif, vous devez encoder votre vidéo source sous la forme de fichiers multidébits. Vous pouvez utiliser Azure Media Encoder Standard pour encoder vos vidéos.  

Media Services fournit l’empaquetage dynamique. Avec l’empaquetage dynamique, vous pouvez distribuer vos fichiers MP4 multidébits dans TLS, Smooth Streaming et MPEG-DASH, sans qu’un nouvel empaquetage soit nécessaire. L’empaquetage dynamique vous permet de stocker et de payer les fichiers dans un format de stockage unique. Media Services crée et fournit la réponse appropriée à la demande du client.

Pour tirer parti de l’empaquetage dynamique, vous devez encoder votre fichier source en un ensemble de fichiers MP4 multidébits. Les étapes d’encodage sont présentées plus loin dans cet article.

Pour savoir comment mettre à l’échelle le traitement multimédia, consultez [Mettre à l’échelle le traitement multimédia](media-services-portal-scale-media-processing.md).

## <a name="encode-in-the-azure-portal"></a>Encoder dans le portail Azure

Pour encoder votre contenu à l’aide de Media Encoder Standard :

1. Dans le [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.
2. Sélectionnez **Paramètres** > **Éléments multimédias**. Sélectionnez l’actif multimédia que vous souhaitez encoder.
3. Cliquez sur le bouton **Encoder**.
4. Dans la fenêtre **Encoder un élément multimédia**, sélectionnez le processeur **Media Encoder Standard**, puis choisissez une présélection. Pour plus d’informations sur les présélections, consultez les articles [Générer automatiquement une échelle de vitesses de transmission](media-services-autogen-bitrate-ladder-with-mes.md) et [Présélections de tâches pour Media Encoder Standard](media-services-mes-presets-overview.md). Il est important de choisir la présélection qui correspond à votre vidéo d’entrée. Par exemple, si vous savez que votre vidéo d’entrée a une résolution de 1 920 x 1 080 pixels, vous pouvez utiliser la présélection **H264 multidébit 1 080 pixels**. Si vous disposez d’une basse résolution vidéo (640 x 360), n’utilisez pas la présélection **H264 multidébit 1 080 pixels**.
   
   Pour vous aider à gérer vos ressources, vous pouvez modifier le nom de l’actif de sortie et le nom de la tâche.
   
   ![Encoder des éléments multimédias](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. Sélectionnez **Créer**.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Étapes suivantes
* [Surveiller la progression du travail d’encodage](media-services-portal-check-job-progress.md) dans le portail Azure  

