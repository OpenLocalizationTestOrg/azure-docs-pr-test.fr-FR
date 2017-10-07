---
title: "aaaGet démarré à la livraison de demande (VOD) à l’aide de hello portail Azure | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes hello d’implémentation d’un service de diffusion de contenu vidéo à la demande (VoD) base avec l’application Azure Media Services (AMS) à l’aide de hello portail Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a>Prise en main la diffusion de contenu sur demande à l’aide de hello portail Azure
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Ce didacticiel vous guide tout au long des étapes hello d’implémentation d’un service de diffusion de contenu vidéo à la demande (VoD) base avec l’application Azure Media Services (AMS) à l’aide de hello portail Azure.

## <a name="prerequisites"></a>Composants requis
Hello Voici didacticiel de hello toocomplete requis :

* Un compte Azure. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Un compte Media Services. toocreate un compte Media Services, consultez [comment tooCreate un compte Media Services](media-services-portal-create-account.md).

Ce didacticiel inclut hello tâches suivantes :

1. Démarrer un point de terminaison de streaming.
2. Télécharger un fichier vidéo.
3. Encoder le fichier de source de hello en un ensemble de fichiers MP4 à débit adaptatif.
4. Publier les actifs hello et get de diffusion en continu et URL de téléchargement progressif.  
5. Lire votre contenu.

## <a name="start-streaming-endpoints"></a>Démarrer les points de terminaison de streaming 

Lorsque vous travaillez avec un des scénarios les plus courants de hello est diffusion vidéo via à débit adaptatif de diffusion en continu Azure Media Services. Media Services propose un empaquetage dynamique, ce qui vous permet de toodeliver votre vitesse de transmission adaptative MP4 encodés le contenu de diffusion en continu des formats pris en charge par Media Services (MPEG DASH, HLS, Smooth Streaming) juste-à-temps, sans que vous ayez toostore préconçue versions de chacune de ces formats de diffusion en continu.

>[!NOTE]
>Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état. 

toostart hello du point de terminaison de diffusion en continu, hello suivant :

1. Connectez-vous à l’adresse hello [portail Azure](https://portal.azure.com/).
2. Dans la fenêtre des paramètres hello, cliquez sur les points de terminaison de diffusion en continu. 
3. Cliquez sur le point de terminaison de diffusion en continu de la valeur par défaut hello. 

    fenêtre de détails par défaut du point de terminaison de diffusion en continu Hello s’affiche.

4. Cliquez sur l’icône Démarrer hello.
5. Cliquez sur toosave de bouton hello enregistrer vos modifications.

## <a name="upload-files"></a>Charger des fichiers
toostream vidéos à l’aide d’Azure Media Services, vous devez les vidéos de source tooupload hello, les encoder en plusieurs vitesses de transmission et publier les résultats hello. première étape de Hello est décrite dans cette section. 

1. Bonjour **paramètre** fenêtre, cliquez sur **actifs**.
   
    ![Charger des fichiers](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. Cliquez sur hello **télécharger** bouton.
   
    Hello **télécharger un élément multimédia vidéo** fenêtre s’affiche.
   
   > [!NOTE]
   > Il n’existe aucune limite de taille de fichier.
   > 
   > 
3. Parcourir vidéo toohello souhaité sur votre ordinateur, sélectionnez-le, puis appuyez sur OK.  
   
    téléchargement de Hello démarre et vous pouvez voir la progression hello sous le nom de fichier hello.  

Une fois le téléchargement de hello terminé, vous voyez hello un nouveau composant répertorié dans hello **actifs** fenêtre. 

## <a name="encode-assets"></a>Encoder des éléments multimédias

Lorsque vous travaillez avec un des scénarios les plus courants de hello transmet les clients tooyour de diffusion en continu à débit adaptatif Azure Media Services. Media Services prend en charge hello suivant des technologies de diffusion en continu de fichiers à débit adaptatif : HTTP Live Streaming (HLS), la diffusion en continu lisse, MPEG DASH. tooprepare vos vidéos pour de diffusion en continu à débit adaptatif, vous devez tooencode votre source vidéo dans des fichiers de débits. Vous devez utiliser hello **Media Encoder Standard** encodeur tooencode vos vidéos.  

Media Services fournit également un empaquetage dynamique, ce qui vous permet de toodeliver votre MP4s débits Bonjour suivant les formats de diffusion en continu : MPEG DASH, HLS, Smooth Streaming, sans que vous ayez toorepackage dans ces formats de diffusion en continu. Avec l’empaquetage dynamique, vous devez uniquement toostore et payer pour les fichiers hello dans un seul format de stockage et de Media Services génère et sert de réponse appropriée de hello en fonction des demandes d’un client.

tootake parti de l’empaquetage dynamique, vous devez tooencode votre fichier source en un ensemble de fichiers MP4 à plusieurs débits (étapes de codage hello sont décrites plus loin dans cette section).

### <a name="toouse-hello-portal-tooencode"></a>tooencode de portail hello toouse
Cette section décrit les étapes à suivre tooencode votre contenu avec Media Encoder Standard hello.

1. Bonjour **paramètres** fenêtre, sélectionnez **actifs**.  
2. Bonjour **actifs** fenêtre, asset hello select que vous aimeriez tooencode.
3. Hello de presse **Encode** bouton.
4. Bonjour **encoder un élément multimédia** fenêtre, processeur de « Media Encoder Standard » hello select et une présélection. Pour plus d’informations sur les présélections, consultez les articles [Utilisation d’Azure Media Encoder Standard pour générer automatiquement une échelle des vitesses de transmission](media-services-autogen-bitrate-ladder-with-mes.md) et [Présélections de travaux pour MES (Media Encoder Standard)](media-services-mes-presets-overview.md). Si vous envisagez toocontrol quelle valeur prédéfinie d’encodage est utilisée, gardez cela à l’esprit : il est important de tooselect hello prédéfini qui convient le mieux pour votre vidéo d’entrée. Par exemple, si vous connaissez votre vidéo d’entrée d’une résolution de 1920 x 1080 pixels, vous pouvez utiliser hello « H264 plusieurs débits binaires 1080p » prédéfini. Si vous disposez d’une vidéo basse résolution (640 x 360), il est préférable de ne pas utiliser la présélection « H264 – Vitesse de transmission multiple – 1 080 pixels ».
   
   Pour faciliter la gestion, vous avez une option de modification de nom hello de ressource en sortie hello et nom hello du travail de hello.
   
   ![Encoder des éléments multimédias](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. Appuyez sur **Créer**.

### <a name="monitor-encoding-job-progress"></a>Suivi de la progression de la tâche d’encodage
progression de hello toomonitor Hello encodage de travail, cliquez sur **paramètres** (en hello haut hello), puis sélectionnez **travaux**.

![Tâches](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a>Publication de contenu
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

> [!NOTE]
> Si vous avez utilisé les localisateurs toocreate portail hello avant mars 2015, les localisateurs avec une date d’expiration de deux ans ont été créés.  
> 
> 

tooupdate une date d’expiration sur un localisateur, utilisez [reste](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) ou [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API. Lorsque vous mettez à jour date d’expiration de hello d’un localisateur SAS, hello URL change.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello toopublish portail un élément multimédia
toouse hello toopublish portail un élément multimédia, hello suivant :

1. Sélectionnez **Paramètres** > **Éléments multimédias**.
2. Sélectionnez asset hello que vous souhaitez toopublish.
3. Cliquez sur hello **publier** bouton.
4. Sélectionnez le type de localisateur hello.
5. Cliquez sur **Ajouter**.
   
    ![Publier](./media/media-services-portal-vod-get-started/media-services-publish1.png)

Hello URL est ajouté à la liste des toohello **URL de publication**.

## <a name="play-content-from-hello-portal"></a>Lire le contenu à partir du portail de hello
portail Azure Hello fournit un lecteur de contenu que vous pouvez utiliser tootest votre vidéo.

Vidéo de hello souhaité, puis cliquez sur hello **lire** bouton.

![Publier](./media/media-services-portal-vod-get-started/media-services-play.png)

Certaines considérations s’appliquent :

* toobegin de diffusion en continu, démarrage en cours d’exécution hello **par défaut** point de terminaison de diffusion en continu.
* Vérifiez que hello vidéo a été publié.
* Cela **Media player** est lu à partir du point de terminaison de diffusion en continu de la valeur par défaut hello. Si vous souhaitez tooplay à partir d’un élément non défini par défaut diffusion en continu de point de terminaison, cliquez sur l’URL toocopy hello et utilisez un autre lecteur. par exemple, le [lecteur Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

## <a name="next-steps"></a>Étapes suivantes
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

