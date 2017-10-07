---
title: aaaFilters et des manifestes dynamiques | Documents Microsoft
description: "Cette rubrique décrit comment toocreate filtre votre client peut utiliser les toostream des sections spécifiques d’un flux. Media Services crée les manifestes dynamique tooarchive cette diffusion sélective."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: ff102765-8cee-4c08-a6da-b603db9e2054
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 9527a011438c11da07a363d701ea736414412ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="filters-and-dynamic-manifests"></a>Filtres et manifestes dynamiques
À compter de version 2.11, Media Services vous permet toodefine des filtres pour vos ressources. Ces filtres sont des règles côté serveur qui permettent à vos clients toochoose toodo opérations : lecture uniquement une section d’une vidéo (au lieu de hello vidéo complètes), ou spécifiez uniquement un sous-ensemble de formats audio et vidéo que les appareils de votre client peuvent traiter () au lieu de tous les formats de hello qui sont associés les actifs hello). Ce filtrage de vos ressources est archivé via **manifeste dynamique**s qui sont créées lors de toostream de demande de votre client une vidéo en fonction de filtres spécifiées.

Cette rubrique traite des scénarios courants dans lesquels l’utilisation de filtres serait tootopics tooyour très avantageux clients et des liens qui montrent comment toocreate filtres par programmation (actuellement, vous pouvez créer des filtres avec l’API REST uniquement).

## <a name="overview"></a>Vue d'ensemble
Lors de la remise de votre contenu toocustomers (diffusion en continu les événements en direct ou vidéo à la demande) votre objectif est toodeliver une unité de toovarious vidéo haute qualité dans des conditions réseau différents. tooachieve cet objectif hello suivant :

* encoder votre flux toomulti à plusieurs débits ([à débit adaptatif](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) des flux vidéo (cela s’occupe des conditions réseau et de qualité) et 
* utiliser les Services de support [empaquetage dynamique](media-services-dynamic-packaging-overview.md) toodynamically package nouveau votre flux de données dans les différents protocoles (cela s’occupe de la diffusion en continu sur différents appareils). Media Services prend en charge la remise de hello suivant des technologies de diffusion en continu de fichiers à débit adaptatif : HTTP Live Streaming (HLS), la diffusion en continu lisse et MPEG DASH. 

### <a name="manifest-files"></a>Fichiers manifeste
Lorsque vous encodez un élément multimédia à débit adaptatif diffusion en continu, un **manifeste** (sélection) fichier est créé (fichier de hello est basée sur XML ou texte). Hello **manifeste** fichier inclut la diffusion en continu des métadonnées telles que : effectuer le suivi de type (audio, vidéo ou du texte), d’effectuer le suivi de nom, heure de début et de fin, la vitesse de transmission (qualités), langues de suivi, fenêtre de présentation (une fenêtre glissante de durée fixe), vidéo codec (FourCC). Il indique également le fragment suivant de hello lecteur tooretrieve hello en fournissant des informations sur hello suivant lisible fragments vidéo disponibles et leur emplacement. Fragments (ou segments) sont hello réel « blocs » d’un contenu vidéo.

Voici un exemple de fichier manifeste : 

    <?xml version="1.0" encoding="UTF-8"?>    
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="330187755" TimeScale="10000000">

    <StreamIndex Chunks="17" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="8">
    <QualityLevel Index="0" Bitrate="5860941" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931300016E360000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="1" Bitrate="4602724" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931100011EDC00002CD29FF8C7076850A45800000000168E9093525" />
    <QualityLevel Index="2" Bitrate="3319311" FourCC="H264" MaxWidth="1280" MaxHeight="720" CodecPrivateData="000000016764001FAC2CA5014016EC054808080A00000300020000030064C0800067C28000103667F8C7076850A4580000000168E9093525" />
    <QualityLevel Index="3" Bitrate="2195119" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C1000044AA0000ABA9FE31C1DA14291600000000168E9093525" />
    <QualityLevel Index="4" Bitrate="1469881" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C04000B71A0000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="5" Bitrate="978815" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C08001E8480004C4B7F8C7076850A45800000000168E9093525" />
    <QualityLevel Index="6" Bitrate="638374" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C080013D60000C65DFE31C1DA1429160000000168E9093525" />
    <QualityLevel Index="7" Bitrate="388851" FourCC="H264" MaxWidth="320" MaxHeight="180" CodecPrivateData="000000016764000DAC2CA505067E7C054830303200000300020000030064C040030D40003D093F8C7076850A45800000000168E9093525" />

    <c t="0" d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="9600000"/>
    </StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_128kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_128kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="125658" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_56kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_56kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="53655" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>

    </SmoothStreamingMedia>

### <a name="dynamic-manifests"></a>Manifestes dynamiques
Il n’y [scénarios](media-services-dynamic-manifest-overview.md#scenarios) lorsque votre client a besoin de davantage de flexibilité que ce qui est décrit dans le fichier manifeste de l’actif hello par défaut. Par exemple :

* Spécifiques au périphérique : fournir une seule hello spécifiée et/ou de formats spécifiée des pistes de langue sont pris en charge par le périphérique hello tooplayback utilisé hello (« filtrage associé ») du contenu. 
* Réduire tooshow de manifeste hello un clip sous-chemin d’un événement en direct (« filtrage de découpage secondaire »).
* Début de hello découpage d’une vidéo (« ajustement d’une vidéo »).
* Ajustez la fenêtre de présentation (DVR) dans l’ordre tooprovide une longueur limitée de la fenêtre du magnétoscope numérique hello dans le lecteur hello (« fenêtre Présentation ajustement »).

tooachieve cette souplesse, les offres de Services de support **manifestes dynamique** basé sur prédéfinis [filtres](media-services-dynamic-manifest-overview.md#filters).  Une fois que vous définissez des filtres de hello, vos clients pourraient utiliser toostream un format spécifique ou des clips secondaire de votre vidéo. Ils spécifiez filtres Bonjour URL de diffusion en continu. Filtres peut être appliqué tooadaptive à débit binaire protocoles pris en charge par [empaquetage dynamique](media-services-dynamic-packaging-overview.md): TLS, MPEG-DASH et diffusion en continu lisse. Par exemple :

URL MPEG DASH avec filtre

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf,filter=MyLocalFilter)

URL Smooth Streaming avec filtre

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyLocalFilter)


Pour plus d’informations sur la façon toodeliver votre contenu et génération de diffusion en continu d’URL, consultez [vue d’ensemble du contenu de diffusion](media-services-deliver-content-overview.md).

> [!NOTE]
> Notez que manifestes dynamique ne pas modifier l’élément multimédia de hello et hello manifeste par défaut pour cet élément multimédia. Votre client peut choisir de toorequest un flux de données avec ou sans filtres. 
> 
> 

### <a id="filters"></a>Filtres
Il existe deux types de filtres d'éléments multimédias : 

* Filtres globaux (peut être actif appliqué tooany Bonjour compte Azure Media Services, ont une durée de vie du compte de hello) et 
* Filtres locaux (peut uniquement être asset tooan appliqué par le hello filtre a été associé lors de la création, ont une durée de vie de l’élément multimédia de hello). 

Types de filtres globaux et locaux ont exactement hello les mêmes propriétés. Hello principale différence hello deux est pour les scénarios de quel type d’un serveur de fichiers est plus adapté. Filtres globaux conviennent généralement pour les profils d’appareils (filtrage associé) dans laquelle les filtres locaux peuvent être utilisé tootrim une ressource spécifique.

## <a id="scenarios"></a>Scénarios courants
Comme mentionné avant, lors de la remettre à votre contenu toocustomers (diffusion en continu les événements en direct ou vidéo à la demande) votre objectif est toodeliver une vidéo haute qualité appareils toovarious sous différentes conditions de réseau. De plus, vous pouvez avoir d'autres impératifs impliquant le filtrage de vos éléments multimédias et l'utilisation de **manifestes dynamiques**. Hello les sections suivantes donne une brève présentation des différents scénarios de filtrage.

* Spécifiez uniquement un sous-ensemble de formats audio et vidéo capable de gérer certains appareils (au lieu de tous les formats hello qui sont associés à des actifs de hello). 
* Lire uniquement une section d’une vidéo (au lieu de hello vidéo complètes).
* Ajustement de la fenêtre de présentation DVR.

## <a name="rendition-filtering"></a>Filtrage de rendu
Vous pouvez choisir tooencode vos profils de toomultiple codage asset (ligne de base H.264, H.264 haute, AACL, AACH, Dolby Digital Plus) et plusieurs vitesses de transmission de qualité. Toutefois, tous les appareils client ne prennent pas en charge tous les profils et débits binaires de tous vos éléments multimédias. Par exemple, les anciens appareils Android prennent uniquement en charge H.264 Baseline+AACL. Envoi des appareils tooa débits binaires plus élevée qui ne peut pas obtenir les avantages de hello, gaspille de calcul de la bande passante et de périphérique. Ce périphérique doit décoder tous hello donné plus d’informations, tooscale uniquement il vers le bas pour l’affichage.

Avec un manifeste dynamique, vous pouvez créer des profils d’appareils tels que mobile, de la console, HD/SD, etc. et inclure hello pistes et des qualités de laquelle vous souhaitez toobe une partie de chaque profil.

![Exemple de filtrage de rendu][renditions2]

Bonjour l’exemple suivant, un encodeur a été utilisé tooencode un élément mezzanine en sept formats vidéos ISO MP4s (à partir de 180p too1080p). Hello ressource encodée peut être dynamiquement empaqueté dans n’importe quel Hello suite de protocoles de diffusion en continu : MPEG DASH, Smooth Streaming et HLS.  Haut hello du diagramme de hello, hello TLS manifeste pour un composant de hello sans filtre s’affiche (il contient tous les formats de sept).  Dans la partie inférieure gauche de hello, hello que TLS manifeste toowhich a été appliqué un filtre nommé « ott » s’affiche. filtre de « ott » Hello spécifie tooremove toutes les vitesses de transmission ci-dessous 1 Mbits/s, ce qui a entraîné hello bas deux niveaux de qualité qui est supprimés dans la réponse de hello.  Dans hello en bas à droite, hello TLS toowhich manifeste a été appliqué un filtre nommé « mobile » s’affiche. le filtre « mobile » Hello détermine les formats tooremove où hello résolution est supérieure à 720p, ce qui a entraîné dans deux formats 1080p hello, qui est supprimés.

![Filtrage de rendu][renditions1]

## <a name="removing-language-tracks"></a>Suppression des pistes de langue
Vos éléments multimédias peuvent inclure plusieurs langues audio telles que l'anglais, l'espagnol, le français, etc. En règle générale, les gestionnaires de hello du SDK du lecteur par défaut la sélection d’une piste audio et audio disponibles effectue le suivi par la sélection de l’utilisateur. Il est difficile à toodevelop ces kits de développement logiciel lecteur, elle nécessite des implémentations différentes sur les infrastructures de lecteur spécifique au périphérique. En outre, sur certaines plates-formes, les API de lecteur sont limités et n’incluent pas la fonctionnalité de sélection audio où les utilisateurs ne peuvent pas sélectionner ou modifier une piste audio hello par défaut. Avec des filtres actifs, vous pouvez contrôler le comportement de hello en créant des filtres qui incluent uniquement les langues audio souhaités.

![Filtrage des pistes de langue][language_filter]

## <a name="trimming-start-of-an-asset"></a>Découpage du début d'un élément multimédia
Dans la plupart des événements de diffusion en continu live, opérateurs exécuter des tests avant l’événement réel de hello. Par exemple, ils peuvent inclure une séquence comme suit avant de démarrer hello d’événement de hello : « Programme commencera bientôt ». Si l’archivage de programme de hello, test de hello et les données de séquence sont également archivées et seront incluses dans la présentation de hello. Toutefois, ces informations ne doivent pas être affichées toohello clients. Avec un manifeste dynamique, vous pouvez créer un filtre d’heure de début et supprimer les données de hello indésirables de manifeste de hello.

![Découpage du début][trim_filter]

## <a name="creating-sub-clips-views-from-a-live-archive"></a>Création de sous-clips (vues) à partir d'une archive en direct
De nombreux événements en direct ont une durée d'exécution longue et une archive en direct peut inclure plusieurs événements. Une fois que les chaînes de télévision hello événement dynamique se termine souhaitant toobreak des hello archive se trouvent dans la logique de programme de démarrage et arrêter des séquences. Publiez ensuite ces programmes virtuels séparément sans post traitement archive en direct de hello et ne créez ne pas de ressources distincts (qui bénéficieront pas de fragments de mise en cache existant hello Bonjour CDN). Parmi ces programmes virtuels (éléments de sous-menu) est trimestres hello de football ou de basket, tournées hello base-ball ou des événements individuels d’une après-midi du programme de jeux.

Avec un manifeste dynamique, vous pouvez créer des filtres à l’aide des heures de début et de fin et créer des vues virtuels par-dessus hello votre archive en direct. 

![Filtre de sous-clip][subclip_filter]

Élément multimédia filtré :

![Ski][skiing]

## <a name="adjusting-presentation-window-dvr"></a>Ajustement de la fenêtre de présentation (DVR)
Actuellement, Azure Media Services propose archive circulaire où la durée de hello peut être configurée entre 5 minutes - 25 heures. Le filtrage de manifeste, toocreate utilisé une fenêtre du magnétoscope numérique propagée peut être par-dessus hello archive hello, sans supprimer le média. Il existe de nombreux scénarios où les chaînes de télévision que tooprovide une fenêtre du magnétoscope numérique limitée qui accompagne hello live edge et à hello même temps maintenir une plus grande fenêtre d’archivage. Une chaîne peut données hello toouse qui est en dehors des clips de toohighlight fenêtre hello magnétoscope numérique, ou he\she pouvez tooprovide différentes fenêtres de magnétoscope numérique pour différents appareils. Par exemple, la plupart des appareils mobiles de hello ne gère pas big windows magnétoscope numérique (vous pouvez avoir une fenêtre du magnétoscope numérique 2 minutes pour les appareils mobiles et 1 heure pour les clients de bureau).

![Fenêtre DVR][dvr_filter]

## <a name="adjusting-livebackoff-live-position"></a>Ajustement de LiveBackoff (position en direct)
Le manifeste de filtrage peut être utilisé tooremove quelques secondes à partir de bord en direct de hello d’un programme en direct. Ainsi, les chaînes de télévision présentation de hello toowatch sur la composition d’aperçu hello point et créer des points d’insertion de publication avant de recevoir des visionneuses de hello flux hello (généralement sauvegardées-off en 30 secondes). Chaînes de télévision ensuite, pour ajouter ces infrastructures de client tootheir publications dans le temps pour les informations de hello tooreceived et processus avant d’opportunité de publication hello.

En outre toohello publication prend en charge, LiveBackoff peut être utilisé pour ajuster la position du téléchargement direct client afin que lorsque des clients dérive et atteint le bord de live hello toujours avoir fragments à partir du serveur au lieu d’obtenir des erreurs HTTP 404 ou 412.

![livebackoff_filter][livebackoff_filter]

## <a name="combining-multiple-rules-in-a-single-filter"></a>Combinaison de plusieurs règles dans un seul filtre
Vous pouvez combiner plusieurs règles de filtrage dans un filtre unique. Par exemple, vous pouvez définir une plage règle tooremove une séquence à réception d’une archive en direct et également filtrer les vitesses de transmission disponibles. Pour plusieurs fin hello de règles filtrage résultat est hello (intersection uniquement) de ces règles.

![plusieurs règles][multiple-rules]

## <a name="create-filters-programmatically"></a>Création de filtres par programme
Hello rubrique suivante décrit des entités Media Services toofilters connexes. rubrique de Hello montre également comment tooprogrammatically créer des filtres.  

[Créez des filtres avec les API REST](media-services-rest-dynamic-manifest.md).

## <a name="combining-multiple-filters-filter-composition"></a>Combinaison de plusieurs filtres (composition de filtre)
Vous pouvez également combiner plusieurs filtres dans une URL unique. 

Hello scénario suivant montre comment vous pouvez souhaiter toocombine filtres :

1. Vous devez toofilter de votre vidéos qualités pour des périphériques mobiles Android ou iPAD (dans les qualités de vidéo toolimit ordre). tooremove hello qualités indésirables, vous devez créer un filtre global qui n’est approprié pour les profils de l’appareil. Comme indiqué ci-dessus, les filtres globaux peuvent être utilisés pour tous vos actifs sous hello même support services compte sans aucune autre association. 
2. Vous souhaitez démarrer de hello tootrim et heure d’un élément multimédia de fin. tooachieve, vous créez un filtre local et définir l’heure de début et de fin hello. 
3. Vous souhaitez toocombine de ces filtres (sans combinaison vous devriez tooadd qualité filtrage toohello ajustement filtre qui sera difficile l’utilisation de filtres).

filtres de toocombine, vous devez tooset hello filtre noms toohello manifeste/sélection URL avec séparés par des points-virgules. Supposons que vous avez un filtre nommé *MyMobileDevice* qui filtre les qualités et que vous avez un autre nommé *MyStartTime* tooset spécifique à une heure de début. Vous pouvez les combiner comme suit :

    http://teststreaming.streaming.mediaservices.windows.net/3d56a4d-b71d-489b-854f-1d67c0596966/64ff1f89-b430-43f8-87dd-56c87b7bd9e2.ism/Manifest(filter=MyMobileDevice;MyStartTime)

Vous pouvez combiner des filtres de too3. 

Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) .

## <a name="know-issues-and-limitations"></a>Problèmes connus et limitations
* Le manifeste dynamique fonctionne dans les limites d'un groupe d'images (GOP) (images clés), par conséquent, le découpage est précis au niveau du GOP. 
* Vous pouvez utiliser le même nom de filtre pour les filtres locaux et globaux. Notez que le filtre local a une priorité plus élevée et remplace les filtres globaux.
* Si vous mettez à jour un filtre, peut prendre jusqu'à minutes too2 de règles de hello toorefresh de point de terminaison de diffusion en continu. Si le contenu hello a été traitée à l’aide de certains filtres (et mises en cache proxys et CDN caches), mise à jour de ces filtres peut entraîner des échecs de lecteur. Il est recommandé de cache de hello tooclear après la mise à jour de filtre de hello. Si cette option n'est pas possible, envisagez d'utiliser un filtre différent.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Voir aussi
[Fourniture de contenu tooCustomers vue d’ensemble](media-services-deliver-content-overview.md)

[renditions1]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter.png
[renditions2]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter2.png

[rendered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[timeline_trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[timeline_trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png

[multiple-rules]:./media/media-services-dynamic-manifest-overview/media-services-multiple-rules-filters.png

[subclip_filter]: ./media/media-services-dynamic-manifest-overview/media-services-subclips-filter.png
[trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png
[trim_filter]: ./media/media-services-dynamic-manifest-overview/media-services-trim-filter.png
[redered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[livebackoff_filter]: ./media/media-services-dynamic-manifest-overview/media-services-livebackoff-filter.png
[language_filter]: ./media/media-services-dynamic-manifest-overview/media-services-language-filter.png
[dvr_filter]: ./media/media-services-dynamic-manifest-overview/media-services-dvr-filter.png
[skiing]: ./media/media-services-dynamic-manifest-overview/media-services-skiing.png
