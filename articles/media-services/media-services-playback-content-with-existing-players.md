---
title: aaaUse lecteurs tooplayback votre contenu existant - Azure | Documents Microsoft
description: "Cette rubrique répertorie les lecteurs existants que vous pouvez utiliser tooplayback votre contenu."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 54817345a19a9d3b18f1e7b352c3342043a569b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="playing-your-content-with-existing-players"></a>Lecture de votre contenu à l’aide des lecteurs existants
Azure Media Services prend en charge de nombreux formats de streaming populaires, tels que Smooth Streaming, le streaming HTTP et MPEG-Dash. Cette rubrique vous oriente tooexisting les lecteurs que vous pouvez utiliser tootest votre flux de données.

### <a name="hello-azure-portal-media-services-content-player"></a>lecteur de contenu Hello portail Azure Media Services
Hello **Azure** portail fournit un lecteur de contenu que vous pouvez utiliser tootest votre vidéo.

Cliquez sur hello souhaité vidéo (qu’elle [publié](media-services-portal-publish.md)) et cliquez sur hello **lire** bouton bas hello du portail de hello.

Certaines considérations s’appliquent :

* Hello **lecteur de contenu MEDIA SERVICES** est lu à partir du point de terminaison de diffusion en continu de la valeur par défaut hello. Si vous souhaitez tooplay à partir d’un point de terminaison de diffusion en continu par défaut, utilisez un autre lecteur. Par exemple, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a>Azure Media Player
Utilisez [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tooplayback votre contenu (clair ou non) dans un des hello suivant formats :

* Smooth Streaming
* MPEG DASH
* HLS
* MP4 progressif

### <a name="flash-player"></a>Flash Player
#### <a name="aes-encrypted-with-token"></a>Chiffrement AES avec jeton
[http://aestoken.azurewebsites.net](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a>Lecteurs Silverlight
#### <a name="monitoring"></a>Surveillance
[http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a>PlayReady avec jeton
[http://sltoken.azurewebsites.net](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a>Lecteurs DASH
[http://dashplayer.azurewebsites.net](http://dashplayer.azurewebsites.net)

[http://dashif.org](http://dashif.org)

### <a name="other"></a>Autres
tootest URL HLS vous pouvez également utiliser :

* **Safari** sur un appareil iOS ou
* **3ivx HLS Player** sous Windows.

## <a name="developing-video-players"></a>Développement de lecteurs vidéo
Pour plus d’informations sur comment toodevelop vos propres lecteurs, consultez [développement des lecteurs vidéo](media-services-develop-video-players.md)

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
