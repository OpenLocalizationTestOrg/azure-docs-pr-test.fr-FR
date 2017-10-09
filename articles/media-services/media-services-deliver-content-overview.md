---
title: toocustomers de contenu aaaDelivering | Documents Microsoft
description: "Cette rubrique donne une vue d’ensemble de ce qu’implique la distribution de votre contenu avec Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 89ede54a-6a9c-4814-9858-dcfbb5f4fed5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 0570bd62d9d42633df0132f9449b357e2abb4086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deliver-content-toocustomers"></a>Fournir du contenu toocustomers
Lorsque vous êtes remettre votre toocustomers de contenu de diffusion en continu ou de vidéo à la demande, votre objectif est toodeliver pour les appareils toovarious vidéo de haute qualité dans des conditions réseau différents.

tooachieve cet objectif, vous pouvez :

* Encoder votre flux vidéo de flux tooa plusieurs débits (débit adaptatif). La qualité et les conditions du réseau sont ainsi prises en charge.
* Utiliser Microsoft Azure Media Services [empaquetage dynamique](media-services-dynamic-packaging-overview.md) toodynamically créer un nouveau package votre flux de données dans différents protocoles. La diffusion en continu sur différents appareils est ainsi prise en charge. Media Services prend en charge la remise de hello suivant des technologies de diffusion en continu de fichiers à débit adaptatif : HTTP Live Streaming (HLS), la diffusion en continu lisse et MPEG-DASH.

>[!NOTE]
>Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état. 

Cet article offre une vue d’ensemble sur des concepts importants de la distribution de contenu.

toocheck des problèmes connus, consultez [problèmes connus](media-services-deliver-content-overview.md#known-issues).

## <a name="dynamic-packaging"></a>l’empaquetage dynamique
Avec l’empaquetage dynamique de hello que Media Services fournit, que vous pouvez livrer votre contenu à débit adaptatif MP4 ou Smooth Streaming encodés de diffusion en continu des formats pris en charge par Media Services (MPEG-DASH, HLS, Smooth Streaming) sans avoir toore-package dans Ces formats de diffusion en continu. Nous vous recommandons de distribuer votre contenu avec l’empaquetage dynamique.

tootake parti de l’empaquetage dynamique, vous devez tooencode votre fichier mezzanine (source) dans un ensemble de fichiers MP4 à débit adaptatif ou des fichiers de diffusion en continu lisse à débit adaptatif.

Avec l’empaquetage dynamique, vous stockez et payez les fichiers hello dans le format de stockage unique. Media Services crée et fournit la réponse appropriée de hello en fonction de vos demandes.

L’empaquetage dynamique est disponible pour les points de terminaison de streaming Standard et Premium. 

Pour plus d’informations, consultez [Empaquetage dynamique](media-services-dynamic-packaging-overview.md).

## <a name="filters-and-dynamic-manifests"></a>Filtres et manifestes dynamiques
Vous pouvez définir des filtres pour vos éléments multimédias avec Media Services. Ces filtres sont des règles côté serveur à vos clients de faire lire une section spécifique d’une vidéo ou spécifier un sous-ensemble de formats audio et vidéo capable de gérer les périphériques de votre client (au lieu de tous les formats de hello qui sont associés à des actifs de hello ). Ce filtrage s’effectue via *manifestes dynamiques* qui sont créés lorsque votre client demande toostream une vidéo basée sur l’un ou plusieurs filtres spécifiés.

Pour plus d’informations, consultez [Filtres et manifestes dynamiques](media-services-dynamic-manifest-overview.md).

## <a name="locators"></a>Localisateurs
tooprovide votre utilisateur avec une URL qui peut être utilisé toostream ou télécharger votre contenu, vous devez toopublish votre élément multimédia en créant un localisateur. Un localisateur fournit un hello de tooaccess de point d’entrée des fichiers contenus dans un élément multimédia. Media Services prend en charge deux types de localisateurs :

* Localisateurs OnDemandOrigin. Ceux-ci sont utilisés toostream media (par exemple, MPEG-DASH, HLS ou Smooth Streaming) ou téléchargement progressivement les fichiers.
* Localisateurs d’URL de signature d’accès partagé (SAP). Il s’agit d’ordinateur local du tooyour fichiers media toodownload utilisé.

Un *stratégie d’accès* est utilisé toodefine autorisations hello (par exemple, lecture, écriture et liste) et la durée pour laquelle un client a accès pour un composant particulier. Notez qu’autorisation de liste de hello (AccessPermissions.List) ne doit pas être utilisée pour la création d’un localisateur OrDemandOrigin.

Les localisateurs ont une date d’expiration. Hello portail Azure définit une date d’expiration à 100 ans Bonjour futures de localisateurs.

> [!NOTE]
> Si vous avez utilisé les localisateurs toocreate portail Azure hello avant mars 2015, les localisateurs ont été définies tooexpire après deux ans.
> 
> 

tooupdate une date d’expiration sur un localisateur, utilisez [reste](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) ou [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API. Notez que lorsque vous mettez à jour date d’expiration de hello d’un localisateur SAS, hello URL change.

Les localisateurs ne sont pas conçus toomanage le contrôle d’accès par utilisateur. Vous pouvez accorder des droits tooindividual utilisateurs accès différent à l’aide de solutions de gestion des droits numériques (DRM). Pour plus d’informations, consultez la page [Sécurisation des médias](http://msdn.microsoft.com/library/azure/dn282272.aspx).

Lorsque vous créez un localisateur, il peut y avoir un délai de 30 secondes en raison du processus de stockage et de propagation toorequired dans le stockage Azure.

## <a name="adaptive-streaming"></a>Diffusion en continu adaptative
Technologies de débit adaptatif permettent aux applications de lecteur vidéo toodetermine des conditions réseau et sélectionner à partir de plusieurs débits binaires. Lors de la communication réseau se dégrade, client de hello permet un débit binaire inférieur pour lecture puisse continuer avec la qualité vidéo moindre. Comme l’amélioration des conditions réseau, client de hello peut basculer tooa le débit plus élevé avec une meilleure qualité vidéo. Azure Media Services prend en charge hello suivant des technologies de débit adaptatif : HTTP Live Streaming (HLS), la diffusion en continu lisse et MPEG-DASH.

tooprovide des utilisateurs avec des URL de diffusion en continu, vous devez créer un localisateur OnDemandOrigin. Création de hello donne localisateur vous hello asset toohello chemin d’accès de base qui contient le contenu de hello souhaité toostream. Toutefois, toostream en mesure de toobe ce contenu, vous devez toomodify ce chemin d’accès supplémentaire. tooconstruct une URL complète toohello fichier manifeste de diffusion en continu, vous devez concaténer de chemin d’accès du localisateur hello valeur et hello manifeste (nom_fichier.ISM) nom du fichier. Puis ajoutez **de manifeste** et un chemin d’accès du localisateur de toohello format approprié (si nécessaire).

> [!NOTE]
> Vous pouvez aussi diffuser votre contenu via une connexion SSL. toodo, assurez-vous que votre Démarrer URL de diffusion en continu avec HTTPS. Notez qu’actuellement AMS ne prend pas en charge SSL avec les domaines personnalisés.  
> 


Vous pouvez uniquement diffuser via le protocole SSL si hello point de terminaison à partir duquel vous distribuez votre contenu de diffusion en continu a été créé après le 10 septembre 2014. Si votre URL de diffusion en continu est basés sur hello créés après le 10 septembre 2014, des points de terminaison de diffusion en continu hello URL contient « streaming.mediaservices.windows.net ». URL de diffusion en continu qui contiennent « origin.mediaservices.windows.net » (hello ancien format) ne prennent pas en charge SSL. Si votre URL est dans un ancien format de hello et que vous souhaitez toostream en mesure de toobe via le protocole SSL, créez un nouveau point de terminaison de diffusion en continu. URL de l’utilisation selon hello new toostream de point de terminaison de diffusion en continu votre contenu via le protocole SSL.

## <a name="streaming-url-formats"></a>Formats d’URL de diffusion en continu :
### <a name="mpeg-dash-format"></a>Format MPEG-DASH
{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)

### <a name="apple-http-live-streaming-hls-v4-format"></a>Format Apple HTTP Live Streaming (HLS) V4
{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)

### <a name="apple-http-live-streaming-hls-v3-format"></a>Format Apple HTTP Live Streaming (HLS) V3
{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)

### <a name="apple-http-live-streaming-hls-format-with-audio-only-filter"></a>Format Apple HTTP Live Streaming (HLS) avec filtre audio uniquement
Par défaut, les pistes audio uniquement sont inclus dans hello que TLS de manifeste. Cette condition est nécessaire pour qu’Apple Store certifie les réseaux cellulaires. Dans ce cas, si un client n’a pas suffisamment de bande passante ou est connecté via une connexion de 2G, lecture bascule tooaudio uniquement. Cela permet de tookeep le contenu de diffusion en continu sans mise en mémoire tampon, mais rien ne s’affiche. Dans certains scénarios, la mise en mémoire tampon du lecteur est préférable à une diffusion audio uniquement. Si vous souhaitez piste audio uniquement du hello tooremove, ajoutez **audio uniquement = false** toohello URL.

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3,audio-only=false)

Pour plus d’informations, consultez [Prise en charge la composition du manifeste dynamique et fonctionnalités supplémentaires de sortie HLS](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/).

### <a name="smooth-streaming-format"></a>Format Smooth Streaming
{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest

Exemple :

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest

### <a id="fmp4_v20"></a>Manifeste Smooth Streaming 2.0 (manifeste hérité)
Par défaut, le format de manifeste Smooth Streaming contient la balise de répétition hello (r-tag). Toutefois, certains lecteurs ne gèrent pas la balise hello. Clients avec ces lecteurs peuvent utiliser un format qui désactive la balise hello :

{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=fmp4-v20)

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=fmp4-v20)

## <a name="progressive-download"></a>Téléchargement progressif
Avec le téléchargement progressif, vous pouvez commencer la lecture du contenu multimédia avant que l’intégralité du fichier hello a été téléchargé. Vous ne pouvez pas télécharger progressivement des fichiers .ism* (.ismv, .isma, .ismt ou .ismc).

tooprogressively téléchargent du contenu, utilisez hello OnDemandOrigin type localisateur. Hello exemple suivant montre les URL hello basé sur hello type OnDemandOrigin de localisateur :

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

Vous devez déchiffrer tous les éléments chiffrés de stockage que vous souhaitez toostream à partir du service d’origine hello pour le téléchargement progressif.

## <a name="download"></a>Télécharger
toodownload votre appareil client tooa de contenu, vous devez créer un localisateur SAS. Hello SAS localisateur vous donne accès au conteneur de stockage Azure toohello où se trouve votre fichier. URL de téléchargement toobuild hello, vous avez le nom de fichier tooembed hello entre l’hôte de hello et la signature SAS.

Hello exemple suivant montre les URL de hello qui est basé sur le localisateur SAS de hello :

    https://test001.blob.core.windows.net/asset-ca7a4c3f-9eb5-4fd8-a898-459cb17761bd/BigBuckBunny.mp4?sv=2012-02-12&se=2014-05-03T01%3A23%3A50Z&sr=c&si=7c093e7c-7dab-45b4-beb4-2bfdff764bb5&sig=msEHP90c6JHXEOtTyIWqD7xio91GtVg0UIzjdpFscHk%3D

Hello suivant considérations s’appliquent :

* Vous devez déchiffrer tous les éléments chiffrés de stockage que vous souhaitez toostream à partir du service d’origine hello pour le téléchargement progressif.
* Si le téléchargement n’est pas terminé au bout de 12 heures, il échoue.

## <a name="streaming-endpoints"></a>Points de terminaison de streaming

Un point de terminaison de diffusion en continu représente un service de diffusion en continu qui peut fournir du contenu directement tooa client lecteur application ou tooa réseau content delivery network (CDN) pour plus de distribution. flux sortant de Hello à partir d’un service de point de terminaison de diffusion en continu peut être un flux en direct ou une ressource vidéo à la demande dans votre compte Media Services. Il existe deux types de points de terminaison de streaming : **Standard** et **Premium**. Pour plus d’informations, consultez [Vue d’ensemble des points de terminaison de streaming](media-services-streaming-endpoints-overview.md).

>[!NOTE]
>Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état. 

## <a name="known-issues"></a>Problèmes connus
### <a name="changes-toosmooth-streaming-manifest-version"></a>Version du manifeste de diffusion en continu tooSmooth modifications
Avant que le hello version de juillet 2016 service--lorsque le manifeste des biens produits par l’encodeur de support Standard, Workflow d’encodeur multimédia Premium ou hello Azure Media Encoder antérieures ont été transmis à l’aide d’empaquetage dynamique--hello Smooth Streaming retourné serait conforme tooversion 2.0. Dans la version 2.0, les durées de fragment hello n’utilisent pas les balises hello soi-disant repeat (« r »). Par exemple :

<?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" n="0" />
            <c d="2000" />
            <c d="2000" />
            <c d="2000" />
        </StreamIndex>
    </SmoothStreamingMedia>

Dans la version de juillet 2016 de service de hello, manifeste de diffusion en continu lisse hello généré est conforme à tooversion 2.2, avec des durées de fragment à l’aide de balises de répétitions. Par exemple :

    <?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" r="4" />
        </StreamIndex>
    </SmoothStreamingMedia>

Certaines des clients hérités de diffusion en continu lisse hello n’acceptent pas les balises de répétition hello et ne pourra pas de manifeste de hello tooload. toomitigate ce problème, vous pouvez utiliser le paramètre de format de manifeste hérité hello **(format = fmp4-v20)** ou mettre à jour votre version plus récente toohello du client, qui prend en charge les balises de répétitions. Pour plus d’informations, consultez [Smooth Streaming 2.0](media-services-deliver-content-overview.md#fmp4_v20).

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Rubriques connexes
[Mettre à jour les localisateurs de Media Services après le déploiement des clés de stockage](media-services-roll-storage-access-keys.md)

