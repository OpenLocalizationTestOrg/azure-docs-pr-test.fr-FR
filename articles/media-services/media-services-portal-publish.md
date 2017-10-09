---
title: "AAA » publier du contenu avec hello portail Azure | Documents Microsoft »"
description: "Ce didacticiel vous guide tout au long des étapes hello de publication de votre contenu avec hello portail Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a>Publier du contenu avec hello portail Azure
> [!div class="op_single_selector"]
> * [Portail](media-services-portal-publish.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
> [!NOTE]
> toocomplete ce didacticiel, vous avez besoin d’un compte Azure. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

tooprovide votre utilisateur avec une URL qui peut être utilisé toostream ou télécharger votre contenu, vous tout d’abord besoin trop « publier » votre élément multimédia en créant un localisateur. Les localisateurs offrent toofiles accès contenues dans l’élément multimédia de hello. Media Services prend en charge deux types de localisateurs : 

* Diffusion en continu les localisateurs (OnDemandOrigin), utilisés pour la diffusion adaptative en continu (par exemple, toostream MPEG DASH, HLS ou Smooth Streaming). toocreate un localisateur de diffusion en continu votre élément multimédia doit contenir un fichier .ism. 
* les localisateurs progressifs (SAS), utilisés pour la diffusion de vidéo par téléchargement progressif.

Une URL de diffusion en continu a hello suivant le format et vous pouvez l’utiliser de ressources de diffusion en continu lisse tooplay.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

ajouter des toobuild une URL de diffusion en continu de TLS (format = m3u8-aapl) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

ajouter des toobuild une URL de diffusion en continu de MPEG DASH (format = mpd-heure-csf) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

Une URL SAS a hello suivant le format.

    {blob container name}/{asset name}/{file name}/{SAS signature}

Pour plus d’informations, consultez [Fournir du contenu (vue d’ensemble)](media-services-deliver-content-overview.md).

> [!NOTE]
> Si vous avez utilisé les localisateurs toocreate portail hello avant mars 2015, les localisateurs avec une date d’expiration de deux ans ont été créés.  
> 
> 

tooupdate une date d’expiration sur un localisateur, utilisez [reste](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) ou [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API. Notez que lorsque vous mettez à jour date d’expiration de hello d’un localisateur SAS, hello URL change.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello toopublish portail un élément multimédia
toouse hello toopublish portail un élément multimédia, hello suivant :

1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.
2. Sélectionnez **Paramètres** > **Éléments multimédias**.
3. Sélectionnez asset hello que vous souhaitez toopublish.
4. Cliquez sur hello **publier** bouton.
5. Sélectionnez le type de localisateur hello.
6. Cliquez sur **Ajouter**.
   
    ![Publier](./media/media-services-portal-vod-get-started/media-services-publish1.png)

URL de Hello sera ajouté toohello la liste des **URL de publication**.

## <a name="play-content-from-hello-portal"></a>Lire le contenu à partir du portail de hello
portail Azure Hello fournit un lecteur de contenu que vous pouvez utiliser tootest votre vidéo.

Vidéo de hello souhaité, puis cliquez sur hello **lire** bouton.

![Publier](./media/media-services-portal-vod-get-started/media-services-play.png)

Certaines considérations s’appliquent :

* Vérifiez que hello vidéo a été publié.
* Cela **Media player** est lu à partir du point de terminaison de diffusion en continu de la valeur par défaut hello. Si vous souhaitez tooplay à partir d’un élément non défini par défaut diffusion en continu de point de terminaison, cliquez sur l’URL toocopy hello et utilisez un autre lecteur. par exemple, le [lecteur Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
* Bonjour à partir de laquelle vous diffusiez en continu un point de terminaison de diffusion en continu doit s’exécuter.  

## <a name="next-steps"></a>Étapes suivantes
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

