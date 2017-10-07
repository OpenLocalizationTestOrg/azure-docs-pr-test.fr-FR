---
title: "aaaMicrosoft Azure Media Services scénarios et la disponibilité des fonctionnalités entre centres de données | Documents Microsoft"
description: "Cette rubrique offre une vue d’ensemble des scénarios Microsoft Azure Media Services et de la disponibilité des fonctionnalités et services dans les centres de données."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 3dbab6998ed5da738baf8f1e2fb096dfba336e19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a>Scénarios et disponibilité des fonctionnalités Media Services dans les centres de données

Microsoft Azure Media Services (AMS) vous permet de télécharger des toosecurely, stocker, encoder et empaqueter le contenu vidéo ou audio pour la demande et live diffusion en continu remise toovarious les clients (par exemple, TV, PC et appareils mobiles).

AMS fonctionne dans plusieurs centres de données Bonjour. Ces centres de données sont regroupés dans des régions toogeographic, ce qui vous donne une grande souplesse dans le choix de l’emplacement toobuild vos applications. Vous pouvez passer en revue hello [la liste des régions et leurs emplacements](https://azure.microsoft.com/regions/). 

Cette rubrique décrit les scénarios courants pour distribuer votre contenu [en direct](#live_scenarios) ou [à la demande](#vod_scenarios). rubrique de Hello fournit également des détails sur la disponibilité des services et les fonctionnalités multimédias centres de données.

## <a name="overview"></a>Vue d'ensemble

### <a name="prerequisites"></a>Composants requis

toostart à l’aide d’Azure Media Services, vous devez disposer de hello :

* Un compte Azure. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com).
* Un compte Azure Media Services. Pour plus d’informations, consultez [Créer un compte](media-services-portal-create-account.md).
* Hello, point de terminaison à partir de laquelle vous souhaitez toostream contenu de diffusion en continu a toobe Bonjour **en cours d’exécution** état.

    Lorsque votre compte AMS est créé, un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de diffusion en continu de point de terminaison de diffusion en continu a toobe Bonjour **en cours d’exécution** état.

### <a name="commonly-used-objects-when-developing-against-hello-ams-odata-model"></a>Objets couramment utilisés lors du développement avec hello modèle AMS OData

Hello image suivante montre certains des objets de hello couramment utilisé lors du développement avec le modèle de Media Services OData hello.

Cliquez sur tooview d’image hello il plein écran.  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

Vous pouvez afficher hello ensemble modèle [ici](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-hello-clear-non-encrypted"></a>Protéger le contenu dans le stockage et la remise diffusion multimédia en continu dans hello Effacer (non chiffré)

![Flux de travail VOD](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. Chargez un fichier multimédia de haute qualité dans une ressource.

    Il est recommandé de tooapply chiffrement option tooyour élément multimédia de stockage dans l’ordre tooprotect votre contenu au cours de téléchargement et while au repos dans le stockage.
2. Encoder l’ensemble de tooa de fichiers MP4 à débit adaptatif.

    Il est recommandé de sortie tooapply stockage chiffrement option toohello actif dans l’ordre tooprotect votre contenu au repos.
3. Configurez la stratégie de remise de ressources (utilisée par l’empaquetage dynamique).

    Si votre ressource est stockée sous forme chiffrée, vous **devez** configurer une stratégie de remise de ressources.
4. Publier les actifs hello en créant un localisateur OnDemand.
5. Diffusez le contenu publié.

Pour plus d’informations sur la disponibilité des centres de données, consultez hello [disponibilité](#availability) section.

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a>Protéger le contenu stocké et diffuser du contenu multimédia chiffré dynamiquement en continu

![Protéger avec PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. Chargez un fichier multimédia de haute qualité dans une ressource. Appliquer la ressource de stockage chiffrement option toohello.
2. Encoder l’ensemble de tooa de fichiers MP4 à débit adaptatif. Appliquer la ressource en sortie toohello stockage chiffrement option.
3. Créer la clé de chiffrement de contenu pour l’élément hello toobe chiffré dynamiquement pendant la lecture.
4. Configurez la stratégie d’autorisation de clé de contenu.
5. Configurez la stratégie de remise de ressources (utilisée par l’empaquetage dynamique et le chiffrement dynamique).
6. Publier les actifs hello en créant un localisateur OnDemand.
7. Diffusez le contenu publié.

Pour plus d’informations sur la disponibilité des centres de données, consultez hello [disponibilité](#availability) section.

## <a name="use-media-analytics-tooderive-actionable-insights-from-your-videos"></a>Utilisez les informations exploitables de tooderive Analytique de support à partir de vos vidéos

Support Analytique est une collection de composants de la reconnaissance vocale et de la vision qui le rendent plus facile pour les organisations et les entreprises tooderive d’informations exploitables à partir de leurs fichiers vidéos. Pour plus d’informations, consultez [Vue d’ensemble d’Azure Media Analytics](media-services-analytics-overview.md).

1. Chargez un fichier multimédia de haute qualité dans une ressource.
2. Traiter vos vidéos avec l’un des services de support Analytique hello décrites dans hello [vue d’ensemble du support Analytique](media-services-analytics-overview.md) section.
3. Les processeurs multimédias Media Analytics créent des fichiers MP4 ou JSON. Si un processeur multimédia produit un fichier MP4, vous pouvez télécharger progressivement les fichier hello. Si un processeur multimédia produit un fichier JSON, vous pouvez télécharger le fichier de hello de hello stockage d’objets blob Azure.

Pour plus d’informations sur la disponibilité des centres de données, consultez hello [disponibilité](#availability) section.

## <a name="deliver-progressive-download"></a>Remettre le téléchargement progressif

1. Chargez un fichier multimédia de haute qualité dans une ressource.
2. Encoder un fichier MP4 unique de tooa.
3. Publier les actifs hello en créant un localisateur OnDemand ou SAS.

    Si vous utilisez localisateur SAS, hello est téléchargé à partir hello stockage d’objets blob Azure. Dans ce cas, vous n’avez pas besoin de toohave de diffusion en continu des points de terminaison dans l’état démarré.
4. Téléchargez le contenu de manière progressive.

## <a id="live_scenarios"></a>Diffusion d’événements en streaming en direct 

1. Ingérer du contenu en direct à l’aide de différents protocoles de streaming en direct (par exemple RTMP ou Smooth Streaming)
2. Encoder votre flux en flux à débit adaptatif (facultatif)
3. Afficher un aperçu de votre flux en direct
4. Fournir du contenu hello via des protocoles de diffusion en continu courants (par exemple, MPEG DASH, Smooth Streaming, HLS) directement les clients tooyour ou tooa réseau de distribution de contenu (CDN) pour une distribution ultérieure.

    -ou-

    Enregistrement et le magasin de contenu hello ingéré dans l’ordre toobe transmis en continu ultérieur (vidéo à la demande).

Lors de la diffusion en continu, vous pouvez choisir un des éléments suivants de hello achemine :

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Utilisation des canaux recevant un flux dynamique à débit binaire multiple provenant d’encodeurs locaux (méthode directe)

Hello diagramme suivant montre hello de plateforme de hello AMS des composants principaux impliqués dans hello **pass-through** flux de travail.

![Flux de travail live](./media/scenarios-and-availability/media-services-live-streaming-current.png)

Pour plus d’informations, consultez [Utilisation des canaux recevant un flux dynamique à débit binaire multiple provenant d’encodeurs locaux](media-services-live-streaming-with-onprem-encoders.md).

### <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Utilisation de canaux qui sont activés tooperform dynamique encodage avec Azure Media Services

Hello diagramme suivant montre hello principales parties de plateforme de AMS hello impliqués dans le flux de travail de diffusion en continu Live où un canal est activé tooperform dynamique encodage avec Media Services.

![Flux de travail live](./media/scenarios-and-availability/media-services-live-streaming-new.png)

Pour plus d’informations, consultez [utilisation de canaux est à activé tooPerform Live encodage avec Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

Pour plus d’informations sur la disponibilité des centres de données, consultez hello [disponibilité](#availability) section.

## <a name="consuming-content"></a>Utilisation de contenu

Azure Media Services fournit des outils hello vous devez toocreate riche, les applications de lecteur client dynamiques pour la plupart des plateformes, y compris : iOS, appareils, les appareils Android, Windows, Windows Phone, Xbox et décodeurs boîtes. Hello rubrique suivante fournit des liens tooSDKs et des infrastructures de lecteur que vous pouvez utiliser toodevelop vos propres applications clientes qui peuvent consommer de diffusion multimédia en continu à partir des Services de support. Pour plus d’informations, consultez [Développement d’applications de lecteur vidéo](media-services-develop-video-players.md).

## <a name="enabling-azure-cdn"></a>Activation du CDN Azure

Media Services prend en charge l’intégration avec le CDN d’Azure. Pour plus d’informations sur la façon de tooenable CDN Azure, consultez [comment tooManage points de terminaison de diffusion en continu dans un compte Media Services](media-services-portal-manage-streaming-endpoints.md).

## <a id="scaling"></a>Scalabilité d’un compte Media Services

Les clients AMS peuvent mettre à l’échelle les points de terminaison de streaming, le traitement multimédia et le stockage dans leurs comptes AMS.

* En fonction de leurs besoins, les clients Media Services peuvent choisir un point de terminaison de streaming **Standard** ou **Premium**. Le point de terminaison de streaming **Standard** convient à la plupart des charges de travail de streaming. Il inclut hello mêmes fonctionnalités comme un **Premium** diffusion en continu de bande passante sortante de points de terminaison et les échelles automatiquement. 

    Les points de terminaison de streaming **Premium** sont conçus pour les charges de travail avancées et fournissent une capacité de bande passante dédiée et scalable. Les clients disposant d’un point de terminaison de streaming **Premium** ont par défaut une unité de streaming. point de terminaison de diffusion en continu de Hello peut être monté en ajoutant SUs. Chaque appel à SU fournit l’application de toohello de capacité de la bande passante supplémentaire. Pour plus d’informations sur la mise à l’échelle **Premium** points de terminaison de diffusion en continu, consultez hello [mise à l’échelle des points de terminaison de diffusion en continu](media-services-portal-scale-streaming-endpoints.md) rubrique.

* Un compte Media Services est associé à un Type d’unité réservée, qui détermine la vitesse de hello avec lequel votre média, les tâches de traitement est traités. Vous pouvez choisir parmi les éléments suivants de hello réservé de types d’unités : **S1**, **S2**, ou **S3**. Par exemple, les hello même travail d’encodage s’exécute plus rapidement lorsque vous utilisez hello **S2** type d’unité réservée comparer toohello **S1** type.

    En outre toospecifying hello réservé type d’unité, vous pouvez spécifier tooprovision votre compte avec **unités réservées** (RUs). nombre de Hello de configuré RUs détermine nombre hello de tâches multimédia qui peuvent être traitées simultanément dans un compte donné.

    >[!NOTE]
    >Les unités réservées fonctionnent pour la mise en parallèle de tout le traitement multimédia, notamment les travaux d’indexation qui utilisent Azure Media Indexer. Toutefois, contrairement à l’encodage, l’indexation des travaux n’est pas plus rapide avec des unités réservées plus rapides.

    Pour plus d’informations, consultez [Mise à l’échelle du traitement multimédia](media-services-portal-scale-media-processing.md).
* Vous pouvez également faire évoluer votre compte Media Services en ajoutant tooit des comptes de stockage. Chaque compte de stockage est limité too500 to. tooexpand votre stockage au-delà des limites de hello par défaut, vous pouvez choisir tooattach plusieurs comptes tooa unique Media Services compte de stockage. Pour plus d’informations, consultez [Gérer les comptes de stockage](meda-services-managing-multiple-storage-accounts.md).

##<a id="availability"></a> Disponibilité des fonctionnalités Media Services dans les centres de données

Cette section présente des informations sur la disponibilité des fonctionnalités Media Services dans les centres de données.

### <a name="ams-accounts"></a>Comptes AMS

#### <a name="availability"></a>Disponibilité

Vous pouvez créer des comptes de service de média Bonjour suivant régions : Europe du Nord, Europe de l’ouest, ouest des États-Unis, est des États-Unis, Asie du Sud-est, Asie orientale, occidental, oriental, sud du Brésil, Inde-ouest, l’Inde Sud et Inde centrale. 

### <a name="streaming-endpoints"></a>Points de terminaison de streaming 

En fonction de leurs besoins, les clients Media Services peuvent choisir un point de terminaison de streaming **Standard** ou **Premium**. Pour plus d’informations, consultez hello [mise à l’échelle](#scaling) section.

#### <a name="availability"></a>Disponibilité

|Nom|État|Centres de données
|---|---|---|
|Standard|GA|Tout|
|Premium|GA|Tout|

### <a name="live-encoding"></a>Live Encoding

#### <a name="availability"></a>Availability

Disponible dans tous les centres de données, à l’exception des régions suivantes : Allemagne, Sud du Brésil, Inde-Ouest, Inde-Sud et Inde-Centre. 

### <a name="encoding-media-processors"></a>Processeurs multimédia d’encodage

AMS offre deux encodeurs à la demande : **Media Encoder Standard** et **Media Encoder Premium Workflow**. Pour plus d’informations, consultez [Vue d’ensemble et comparaison d’encodeurs multimédia à la demande Azure](media-services-encode-asset.md). 

#### <a name="availability"></a>Availability

|Nom du processeur multimédia|État|Centres de données
|---|---|---|
|Media Encoder Standard|GA|Tout|
|Media Encoder Premium Workflow|GA|Tout sauf la Chine|

### <a name="analytics-media-processors"></a>Processeurs multimédias Analytics

Support Analytique est une collection de composants de la reconnaissance vocale et de la vision qui rend plus facile pour les organisations et les entreprises tooderive d’informations exploitables à partir de leurs fichiers vidéos. Pour plus d’informations, consultez [Vue d’ensemble d’Azure Media Analytics](media-services-analytics-overview.md).

#### <a name="availability"></a>Availability

|Nom du processeur multimédia|État|Centres de données
|---|---|---|
|Détecteur de visage Azure Media|VERSION PRÉLIMINAIRE|Tout|
|Azure Media Hyperlapse|VERSION PRÉLIMINAIRE|Tout|
|Azure Media Indexer|GA|Tout|
|Détecteur de mouvement Azure Media|VERSION PRÉLIMINAIRE|Tout|
|Azure Media OCR|VERSION PRÉLIMINAIRE|Tout|
|Azure Media Redactor|VERSION PRÉLIMINAIRE|Tout|
|Azure Media Stabilizer|VERSION PRÉLIMINAIRE|Tout|
|Miniatures vidéo Azure Media|VERSION PRÉLIMINAIRE|Tout|
|Azure Media Indexer 2|VERSION PRÉLIMINAIRE|Tout sauf la région de Chine et du gouvernement fédéral|

### <a name="protection"></a>Protection

Microsoft Azure Media Services permet de vous toosecure votre média à partir de l’heure hello qu'il quitte votre ordinateur via le stockage, le traitement et la remise. Pour plus d’informations, consultez [Protection du contenu AMS](media-services-content-protection-overview.md).

#### <a name="availability"></a>Availability

|Chiffrement|État|Centres de données|
|---|---|---| 
|Storage|GA|Tout|
|Clés AES-128|GA|Tout|
|Fairplay|GA|Tout|
|PlayReady|GA|Tout|
|Widevine|GA|Tous, sauf les régions Allemagne, Gouvernement fédéral et Chine.

### <a name="reserved-units-rus"></a>Unités réservées

nombre Hello d’unités réservées configurées détermine le nombre hello de tâches multimédia qui peuvent être traitées simultanément dans un compte donné. 

Pour plus d’informations, consultez hello [mise à l’échelle](#scaling) section.

#### <a name="availability"></a>Disponibilité

Disponible dans tous les centres de données.

### <a name="reserved-unit-ru-type"></a>Type d’unité réservée

Un compte Media Services est associé à un type d’unité réservée, qui détermine la vitesse de hello avec lequel votre média, les tâches de traitement est traités. Vous pouvez choisir parmi les éléments suivants de hello réservé de types d’unités : S1, S2 ou S3.

Pour plus d’informations, consultez hello [mise à l’échelle](#scaling) section.

#### <a name="availability"></a>Disponibilité

|Nom du type d’unité réservée|État|Centres de données
|---|---|---|
|S1|GA|Tout|
|S2|GA|Tous, à l’exception des régions Sud du Brésil et Inde-Ouest|
|S3|GA|Tous, à l’exception de la région Inde-Ouest|

## <a name="next-steps"></a>Étapes suivantes

Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

