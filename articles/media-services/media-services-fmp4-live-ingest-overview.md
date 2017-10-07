---
title: "spécification de réception aaaAzure Media Services MP4 fragmenté live | Documents Microsoft"
description: "Cette spécification décrit le protocole de hello et format pour fragmentés basée sur des fichiers MP4 en diffusion en continu ingestion pour Azure Media Services. Vous pouvez utiliser des événements en direct toostream Azure Media Services et diffuser le contenu en temps réel en utilisant Azure comme plateforme de cloud hello. Ce document explique également les pratiques recommandées pour créer des mécanismes d’ingestion en direct extrêmement redondants et robustes."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 43fac263-a5ea-44af-8dd5-cc88e423b4de
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 0c191f8d6c5a595621feaba0e571fb984b666f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-fragmented-mp4-live-ingest-specification"></a>Spécification d’ingestion en direct au format MP4 fragmenté Azure Media Services
Cette spécification décrit le protocole de hello et format pour fragmentés basée sur des fichiers MP4 en diffusion en continu ingestion pour Azure Media Services. Media Services fournit un service de diffusion en continu live que les clients peuvent utiliser des événements en direct toostream et diffuser le contenu en temps réel en utilisant Azure comme plateforme de cloud hello. Ce document explique également les pratiques recommandées pour créer des mécanismes d’ingestion en direct extrêmement redondants et robustes.

## <a name="1-conformance-notation"></a>1. Notation de conformité
Hello mots clés « doit », « ne doit pas, » « Requis », « Devra », « ne devra pas, » « Devrait », « Ne doivent pas », « Recommandé », « Peut » et « OPTIONAL » dans ce document sont toobe interprété comme elles sont décrites dans la RFC 2119.

## <a name="2-service-diagram"></a>2. Diagramme du service
Hello diagramme suivant montre architecture de haut niveau hello Hello dynamique de diffusion en continu de service dans les Services de support :

1. Un encodeur en direct push toochannels de flux live qui sont créés et configurés via hello Azure Media Services SDK.
2. Canaux, les programmes et les points de terminaison de diffusion en continu tous les hello diffusion en continu de fonctionnalités, notamment la réception, la mise en forme, du handle de Media Services de cloud computing magnétoscope numérique, sécurité, l’évolutivité et la redondance.
3. Le cas échéant, les clients peuvent choisir toodeploy une couche d’Azure Content Delivery Network entre hello de diffusion en continu de point de terminaison et les points de terminaison clients hello.
4. Flux de points de terminaison de client à partir de hello point de terminaison de diffusion en continu à l’aide de protocoles de diffusion en continu adaptative de HTTP. Parmi les exemples citons Microsoft Smooth Streaming, Dynamic Adaptive Streaming sur HTTP (DASH ou MPEG-DASH) et Apple HTTP Live Streaming (HLS).

![Flux d’ingestion][image1]

## <a name="3-bitstream-format--iso-14496-12-fragmented-mp4"></a>3. Format de flux binaire – MP4 fragmenté ISO 14496-12
Hello format de transmission pour la diffusion en continu de réception décrites dans ce document est basé sur [ISO-14496-12]. Pour obtenir une explication détaillée du format MP4 fragmenté et des extensions de fichiers vidéo à la demande et d’ingestion de streaming en direct, consultez [[MS-SSTR]](http://msdn.microsoft.com/library/ff469518.aspx).

### <a name="live-ingest-format-definitions"></a>Définitions de format de réception en temps réel
Hello listée ci-dessous format spécial définitions qui s’appliquent toolive de réception dans Azure Media Services :

1. Hello **ftyp**, **zone de manifeste de serveur Live**, et **moov** zones doivent être envoyés avec chaque demande (HTTP POST). Ces zones doivent être envoyés au début de hello du flux de hello et n’importe quel moment encodeur de hello doit se reconnecter tooresume flux de réception. Pour plus d’informations, consultez la section 6 dans [1].
2. La section 3.3.2 dans [1] définit une zone facultative appelée **StreamManifestBox** pour l’ingestion en direct. En raison de la logique de routage toohello d’équilibrage de charge Azure hello, à l’aide de cette zone est déconseillée. boîte de Hello ne doit pas être présent lors de la réception dans Media Services. Si cette zone est présente, Media Services l’ignore en mode silencieux.
3. Hello **TrackFragmentExtendedHeaderBox** boîte définie dans 3.2.3.2 dans [1] doit être présent pour chaque fragment.
4. La version 2 de hello **TrackFragmentExtendedHeaderBox** case doit être utilisé toogenerate des segments de supports ayant des URL identiques dans plusieurs centres de données. champ de l’index Hello fragment est requise pour le basculement entre centres de données basée sur les index de diffusion en continu formats de tels que Apple HLS et MPEG-DASH basés sur un index. basculement entre centres de données de tooenable, hello fragment l’index doit être synchronisé entre plusieurs encodeurs et être augmenté de 1 pour chaque fragment multimédia successives, voire entre les redémarrages de l’encodeur ou d’échecs.
5. Section 3.3.6 dans [1] définit une zone appelée **MovieFragmentRandomAccessBox** (**mfra**) qui peut être envoyé à la fin hello de canal toohello de réception dynamique tooindicate fin de flux (fin du support). Échéance toohello réception logique de Media Services, à l’aide de la fin du support est déconseillée et hello **mfra** boîte de réception dynamique ne doit pas être envoyée. Si elle l’est, Media Services l’ignore en mode silencieux. état de hello tooreset Hello de point de réception, nous vous recommandons d’utiliser [canal réinitialisé](https://docs.microsoft.com/rest/api/media/operations/channel#reset_channels). Nous vous recommandons également d’utiliser [programme arrêter](https://msdn.microsoft.com/library/azure/dn783463.aspx#stop_programs) tooend une présentation et un flux de données.
6. durée du fragment Hello MP4 doit être constante, taille de hello tooreduce des manifestes de client hello. Une durée de fragment MP4 constante améliore également l’heuristique du téléchargement client à l’aide de hello de balises de répétitions. durée de Hello peut-être fluctuer toocompensate pour des fréquences d’images de type non entier.
7. durée du fragment Hello MP4 doit être comprise entre environ 2 et 6 secondes.
8. Les horodatages et index du fragment MP4 (**TrackFragmentExtendedHeaderBox** `fragment_ absolute_ time` et `fragment_index`) DOIVENT normalement arriver dans l’ordre croissant. Bien que Media Services est résilient tooduplicate fragments, il a limité les fragments de tooreorder possibilité selon la chronologie du média toohello.

## <a name="4-protocol-format--http"></a>4. Format de protocole – HTTP
ISO fragmenté basée sur des fichiers MP4 en temps réel de réception pour Media Services utilise une longue HTTP POST demande tootransmit encodé media données standard qui sont empaquetées dans un service de toohello de format MP4 fragmenté. Chaque requête HTTP POST envoie un fragmenté MP4 flux binaire (« stream »), à partir des zones d’en-tête à compter de hello (**ftyp**, **zone de manifeste de serveur Live**, et **moov** zones) et en continuant avec une séquence de fragments (**moof** et **mdat** boîtes). Syntaxe d’URL pour la requête HTTP POST de hello, consultez la section 9.2 in [1]. Un exemple Hello poster une URL est : 

    http://customer.channel.mediaservices.windows.net/ingest.isml/streams(720p)

### <a name="requirements"></a>Configuration requise
Voici hello exigences détaillées :

1. Hello encodeur doit démarrer hello de diffusion en envoyant une demande HTTP POST avec vide « corps » (longueur de contenu nulle) à l’aide de hello même URL de réception. Cela permet d’encoder de hello rapidement détecter si le point de terminaison de réception dynamique hello est valide et s’il n’y aucune authentification ou autres conditions requises. Par le protocole HTTP, les serveur hello ne peut pas renvoyer une réponse HTTP jusqu'à ce que hello entière, y compris le corps de publication hello, la demande. Raison de la nature hello longue d’un événement en direct, sans cette étape, l’encodeur de hello peut-être pas en mesure de toodetect toute erreur jusqu'à ce qu’il termine l’envoi de toutes les données hello.
2. encodeur de Hello doit gérer les erreurs ou les demandes d’authentification en raison de (1). Si (1) réussit avec une réponse 200, continuez.
3. encodeur de Hello doit commencer une nouvelle demande HTTP POST avec flux de fichiers MP4 hello fragmenté. charge utile de Hello doit commencer par les zones d’en-tête hello, suivis par fragments. Notez que hello **ftyp**, **zone de manifeste de serveur Live**, et **moov** cases (dans cet ordre) doivent être envoyés avec chaque demande, même si l’encodeur de hello doit se reconnecter car hello demande précédente a été interrompue fin toohello préalable du flux de hello. 
4. encodeur de Hello doit utiliser pour le téléchargement de codage de transfert mémorisé en bloc, car il est impossible toopredict hello contenu longueur totale de hello dynamique des événements.
5. Lors de l’événement de hello est, après l’envoi du dernier fragment de hello, encodeur de hello doit se terminer normalement le codage de séquence de message (la plupart des piles de client HTTP gérer automatiquement) de transfert hello mémorisé en bloc. encodeur de Hello doit attendre le code de réponse finale hello service tooreturn hello, puis se ferme les connexions hello. 
6. encodeur Hello ne doit pas utiliser hello `Events()` substantif comme décrit dans 9.2 [1] pour l’ingestion en direct dans Media Services.
7. Si de requête HTTP POST hello se termine ou heures out avec un TCP erreur toohello préalable de fin de flux de données hello, hello encodeur doit émettre une nouvelle demande POST à l’aide d’une nouvelle connexion et suivez hello exigences précédentes. En outre, encodeur de hello doit renvoyer hello des fragments MP4 deux précédentes pour chaque piste de flux de données hello et reprendre sans introduire une discontinuité dans la chronologie du média hello. Renvoi des deux derniers fragments MP4 pour chaque piste hello garantit qu’il n’existe aucune perte de données. En d’autres termes, si un flux de données contient un audio et une piste vidéo, Échec de la demande POST en cours de hello, encodeur de hello doit se reconnecter et renvoyer hello dernière deux fragments de la piste audio de hello, qui ont été envoyées précédemment avec succès, et hello deux derniers fragments pour piste vidéo de Hello, qui ont été précédemment envoyé, tooensure qu’il n’existe aucune perte de données. encodeur de Hello doit conserver une mémoire tampon de « avant » de fragments de média, il renvoie lorsqu’il se reconnecte.

## <a name="5-timescale"></a>5. Échelle de temps
[[MS-SSTR] ](https://msdn.microsoft.com/library/ff469518.aspx) décrit hello de l’utilisation de l’échelle de temps pour **SmoothStreamingMedia** (Section 2.2.2.1), **StreamElement** (Section 2.2.2.3), **StreamFragmentElement**(Section 2.2.2.6), et **LiveSMIL** (Section 2.2.7.3.1). Si la valeur d’échelle de temps hello n’est pas présent, valeur par défaut de hello utilisée est 10 000 000 (10 MHz). Bien que la spécification de format de diffusion en continu de hello ne bloque pas l’utilisation d’autres valeurs de l’échelle de temps, la plupart des implémentations d’encodeur utilisent cette valeur par défaut toogenerate valeur (10 MHz) de diffusion en continu lisse les données de réception. Échéance toohello [mise en package dynamique Azure Media](media-services-dynamic-packaging-overview.md) fonctionnalité, nous recommandons d’utiliser une échelle de temps 90 KHz des flux vidéo et 44,1 KHz KHz 48.1 pour les flux audio. Si les valeurs de l’échelle de temps différents sont utilisés pour différents flux, l’échelle de temps hello au niveau du flux de données doit être envoyé. Pour plus d’informations, consultez [[MS-SSTR]](https://msdn.microsoft.com/library/ff469518.aspx).     

## <a name="6-definition-of-stream"></a>6. Définition de « stream »
Flux de données est hello unité de base de l’opération de réception dynamique pour composer des présentations, la gestion des scénarios de redondance et de basculement de diffusion en continu. Stream se définit comme un seul flux binaire MP4 fragmenté pouvant contenir une piste unique ou plusieurs pistes. Une présentation en direct peut contenir un ou plusieurs flux, selon la configuration de hello des encodeurs en temps réel hello. Hello suivant exemples illustre diverses options de l’utilisation de flux toocompose une présentation en direct.

**Exemple :** 

Un client souhaite toocreate une présentation de diffusion en continu en direct qui inclut hello suivant les vitesses de transmission audio/vidéo :

Vidéo : 3000 Kbits/s, 1500 Kbits/s, 750 Kbits/s

Audio : 128 Kbits/s

### <a name="option-1-all-tracks-in-one-stream"></a>Option 1 : toutes les pistes dans un seul flux
Dans cette option, un encodeur unique génère toutes les pistes audio/vidéo et les regroupe dans un flux binaire MP4 fragmenté. Hello fragmenté MP4 flux binaire est ensuite envoyé via une connexion HTTP POST. Dans cet exemple, il existe un seul flux pour cette présentation en direct.

![Flux : une piste][image2]

### <a name="option-2-each-track-in-a-separate-stream"></a>Option 2 : chaque piste dans un flux distinct
Dans cette option, encodeur de hello place d’une piste dans chaque flux binaire fragment MP4 et tous les flux hello publie ensuite sur les connexions HTTP distinctes. Cette option est réalisable avec un seul encodeur ou plusieurs. réception dynamique de Hello voit cette présentation dynamique comme composé de quatre flux.

![Flux : pistes distinctes][image3]

### <a name="option-3-bundle-audio-track-with-hello-lowest-bitrate-video-track-into-one-stream"></a>Option 3 : Regrouper une piste audio avec piste vidéo hello plus bas débit binaire dans un flux de données
Dans cette option, le client de hello choisit une piste audio de hello toobundle avec piste vidéo de la plus faible vitesse de transmission hello dans un flux binaire d’un fragment MP4, et laissez hello autres deux pistes vidéos en tant que flux distincts. 

![Flux : pistes audio et vidéo][image4]

### <a name="summary"></a>Résumé
Cela ne constitue pas la liste exhaustive de toutes les options d’ingestion possibles pour cet exemple. En fait, tous les regroupements de pistes dans des flux sont pris en charge par l’ingestion en direct. Les clients et fournisseurs d'encodeurs peuvent choisir leurs propres implémentations selon la complexité d'ingénierie, la capacité de l'encodeur et les questions de redondance et de basculement. Toutefois, dans la plupart des cas, il est uniquement une piste audio pour hello ensemble dynamique de la présentation. Par conséquent, ses tooensure important hello santé Hello réception du flux qui contient la piste audio de hello. Cette considération souvent des résultats en plaçant la piste audio de hello dans son propre flux de données (comme dans l’Option 2) ou il regroupement avec piste vidéo de la plus faible vitesse de transmission hello (comme dans l’Option 3). En outre, pour une meilleure redondance et la tolérance de panne, envoi hello même piste audio dans deux flux différents (Option 2 avec pistes audio redondant) ou regroupement piste audio hello avec au moins deux des pistes vidéo de la plus faible vitesse de transmission hello (Option 3 avec contenu audio à au moins deux flux vidéos) est fortement recommandée pour direct de réception dans Media Services.

## <a name="7-service-failover"></a>7. Basculement du service
Compte tenu de la nature de hello de diffusion en continu, prise en charge du basculement de bon est essentielle pour garantir la disponibilité de hello du service de hello. Media Services est conçue toohandle différents types d’échecs, notamment des erreurs réseau, les erreurs de serveur et les problèmes de stockage. Lorsqu’il est utilisé conjointement avec la logique de basculement approprié hello encodeur en temps réel côté, clients peuvent obtenir un service de diffusion en continu live hautement fiable du cloud de hello.

Dans cette section, nous abordons les scénarios de basculement du service. Dans ce cas, hello défaillance intervient quelque part dans le service de hello, et il se traduit par une erreur réseau. Voici quelques recommandations pour l’implémentation d’encodeur hello pour gérer le basculement du service :

1. Utiliser un délai d’attente de 10 secondes pour établir la connexion TCP de hello. Si une connexion de hello tooestablish tentative prend plue de 10 secondes, hello opération d’abandon, puis réessayez. 
2. Utiliser un délai d’expiration court pour l’envoi des blocs de message de demande hello HTTP. Si la durée de fragment MP4 hello cible est N secondes, utiliser un délai d’attente d’envoi entre N et 2 N secondes ; par exemple, si la durée de fragment MP4 hello est de 6 secondes, utiliser un délai de 6 secondes too12. Si un délai d’attente se produit, réinitialisation hello connexion, ouvrir une nouvelle connexion et reprendre le flux de données de réception sur une nouvelle connexion hello. 
3. Mettre à jour un tampon propagée qui comporte des deux derniers fragments hello pour chaque piste qui ont été correctement et complètement toohello service envoyés.  Si hello requête HTTP POST pour un flux de données est arrêtée ou arrive à expiration fin toohello préalable du flux de hello, ouvrir une nouvelle connexion et commencer une autre demande HTTP POST, renvoyer des en-têtes de flux hello, renvoyer des fragments de deux derniers pour chaque piste hello et reprendre des flux hello sans introduire une discontinuité dans la chronologie du média hello. Cela réduit les risques de hello de perte de données.
4. Nous vous recommandons de cet encodeur hello ne pas limiter le nombre de hello de nouvelles tentatives tooestablish une connexion ou reprendre après une erreur TCP de diffusion en continu.
5. Après une erreur TCP :
  
    a. Hello en cours de connexion doit être fermée, et une nouvelle connexion doit être créée pour une nouvelle demande HTTP POST.

    b. Hello nouvelle HTTP POST URL doit être identique à celle de l’URL de la publication initiale de hello hello.
  
    c. Hello nouvelle HTTP POST doit inclure les en-têtes de flux de données (**ftyp**, **zone de manifeste de serveur Live**, et **moov** cases) qui sont des en-têtes de flux de données identiques toohello Bonjour initiale POST.
  
    d. fragments de deux derniers Hello envoyés pour chaque piste doivent être renvoyées et de diffusion en continu doit reprendre sans introduire une discontinuité dans la chronologie du média hello. Hello horodateurs de fragments MP4 doit augmenter en permanence, même sur les requêtes HTTP POST.
6. encodeur de Hello doit s’arrêter de requête HTTP POST hello si les données ne sont pas envoyées à un rythme adapté à la durée de fragment MP4 hello.  Une requête HTTP POST qui n’envoie pas de données peut empêcher le déconnecter rapidement les encodeur hello dans les cas de hello d’une mise à jour de service de Media Services. Pour cette raison, hello HTTP POST pour éparses assure le suivi (un signal publicitaire) doit être courte, fin d’exécution dès que le fragment d’éparses hello est envoyé.

## <a name="8-encoder-failover"></a>8. Basculement de l’encodeur
Basculement de l’encodeur est hello second type de scénario de basculement qui doit toobe traité pour la diffusion en continu en direct de bout en bout. Dans ce scénario, condition d’erreur hello se produit côté d’encodeur hello. 

![Basculement de l’encodeur][image5]

Hello suivant attentes s’appliquent à partir du point de terminaison de réception dynamique hello lors de l’encodeur basculement se produit :

1. Une nouvelle instance de l’encodeur doit être créée toocontinue de diffusion en continu, comme illustré dans le diagramme hello (flux de vidéo avec ligne en pointillés à 3000k).
2. Hello Nouvel encodeur doit utiliser hello même demande des URL pour HTTP POST comme hello Échec de l’instance.
3. Hello POST demande du nouvel encodeur doit inclure hello même fragmenté zones d’en-tête MP4 comme hello instance ayant échoué.
4. Nouvel encodeur de Hello doit être synchronisé correctement avec tous les autres des encodeurs en cours d’exécution pour la même présentation live toogenerate hello synchronisés exemples audio/vidéo avec les limites des fragments alignés.
5. nouveau flux de données Hello doit être sémantiquement équivalente avec flux de données hello précédente et interchangeables à des niveaux d’en-tête et à fragment hello.
6. Nouvel encodeur de Hello essayez toominimize une perte de données. Hello `fragment_absolute_time` et `fragment_index` du support de fragments doivent augmenter à partir du point hello où encodeur de hello dernier arrêt. Hello `fragment_absolute_time` et `fragment_index` doit augmenter de façon continue, mais elle est autorisée toointroduce une discontinuité, si nécessaire. Media Services ignore les fragments qu’il a déjà reçu et traité, il est mieux tooerr côté hello du renvoi de fragments à toointroduce des discontinuités dans la chronologie du média hello. 

## <a name="9-encoder-redundancy"></a>9. Redondance de l’encodeur
Les événements que plus grande disponibilité de la demande et la qualité d’expérience, nous avons recommandé d’utiliser les encodeurs redondants actif-actif tooachieve un basculement transparent sans perte de données en direct pour certaines critiques.

![Redondance de l’encodeur][image6]

Comme illustré dans ce diagramme, deux groupes d’encodeurs push simultanément deux copies de chaque flux de données dans le service live hello. Cette configuration est prise en charge, car Media Services peut filtrer les fragments en double en fonction de l’ID du flux et de l’horodatage des fragments. Hello qui en résulte des flux live et archive est une copie unique de tous les flux hello agrégation possibles de hello meilleures de deux sources différentes hello. Par exemple, dans un cas extrême hypothétique, tant qu’il existe un encodeur (il ne dispose pas toobe hello même) en cours d’exécution à un moment donné dans le temps pour chaque flux, hello qui résulte des flux live à partir du service de hello est continue sans perte de données. 

exigences de Hello pour ce scénario sont même hello presque comme des spécifications hello dans les cas de « Basculement de l’encodeur » hello, avec l’exception de hello hello deuxième ensemble d’encodeurs s’exécutent au hello même moment que hello encodeurs principales.

## <a name="10-service-redundancy"></a>10. Redondance du service
Parfois destinés à redondance élevée, vous devez avoir les sinistres régionaux toohandle de sauvegarde entre régions. Développement de topologie de « Redondance encodeur » hello, clients peuvent choisir toohave un déploiement de service redondant dans une région différente est connectée avec hello deuxième ensemble d’encodeurs. Les clients peuvent également travailler avec un toodeploy de fournisseur un gestionnaire de trafic Global devant hello deux déploiements tooseamlessly itinéraire client trafic du service de réseau de livraison de contenu. configuration requise de Hello pour les encodeurs hello est identique hello cas de « Redondance encodeur » hello. Hello seule exception est que hello deuxième ensemble d’encodeurs besoins toobe pointé live tooa autre point de terminaison de réception. Hello diagramme suivant illustre cette configuration :

![Redondance du service][image7]

## <a name="11-special-types-of-ingestion-formats"></a>11. Types spéciaux de formats d’ingestion
Cette section traite des types particuliers de formats de réception dynamique toohandle conçu des scénarios spécifiques.

### <a name="sparse-track"></a>Piste partiellement allouée
Lors de la remise d’une présentation de diffusion en continu en direct avec une expérience client riche, souvent qu’il est nécessaire tootransmit synchronisés à la fois les événements ou signale en intrabande avec les données de support principal hello. L’insertion de publicités dynamiques en direct en est un exemple. Ce type de signalisation d'événement diffère de la diffusion audio/vidéo en continu standard en raison de sa nature partiellement allouée. En d’autres termes, hello signalisation données généralement ne pas se produisent en continu et l’intervalle de salutation peut être toopredict dur. concept de Hello de piste partiellement a été conçue tooingest et les données de signalisation de diffusion en intrabande.

Hello étapes suivantes sont une implémentation recommandée pour la réception de piste partiellement :

1. Créez un flux binaire MP4 fragmenté distinct qui contient uniquement des pistes partiellement allouées, sans pistes audio/vidéo.
2. Bonjour **zone de manifeste de serveur Live** tel que défini dans la Section 6 de [1], utilisez hello *parentTrackName* toospecify hello nom suivi du parent hello. Pour plus d’informations, consultez la section 4.2.1.2.1.2 dans [1].
3. Bonjour **zone de manifeste de serveur Live**, **manifestOutput** doit être défini trop**true**.
4. Compte tenu de nature éparses hello Hello signalisation d’événement, nous vous recommandons suivant de hello :
   
    a. Au début de hello d’événement en direct hello, encodeur de hello envoie les zones d’en-tête initiale hello toohello service, ce qui permet de piste partiellement hello service tooregister hello manifeste hello du client.
   
    b. encodeur de Hello doit s’arrêter de requête HTTP POST hello lorsque les données ne sont pas envoyées. Une publication HTTP longue qui n’envoient pas de données peut empêcher le déconnecter rapidement les encodeur hello dans les cas de hello d’un redémarrage du serveur ou de mise à jour de service de Media Services. Dans ces cas, serveur multimédia de hello est temporairement bloqué dans une opération de réception sur le socket de hello.
   
    c. Au moment de hello lorsque signalant des données n’est pas disponible, les encodeur hello doivent fermer de requête HTTP POST hello. Lors de la demande POST de hello est actif, les encoder hello doit envoyer des données.

    d. Lors de l’envoi des fragments éparses, encodeur de hello peut définir un en-tête content-length explicit, s’il est disponible.

    e. Lors de l’envoi de fragments éparses à une nouvelle connexion, encodeur de hello doit commencer à envoyer à partir des zones d’en-tête hello, suivies de fragments de nouveau hello. Il s’agit de cas dans lequel le basculement se produit entre ces et connexion éparses hello est établie tooa nouveau serveur qui n’a pas été trouvé avant de piste partiellement hello.

    f. fragment de piste partiellement Hello devient disponible toohello client lors hello correspondant parent suivi fragment qui a une valeur supérieure ou égale timestamp disponible toohello client. Par exemple, si le fragment d’éparses hello a un horodateur de t = 1000, il est probable qu’une fois que le client de hello voit horodatage 1000 du fragment « vidéo » (en supposant que nom de la piste hello parent est « vidéo ») ou version ultérieure, il peut télécharger hello fragment éparses t = 1000. Notez que ce signal réel hello peut être utilisé pour une autre position dans la chronologie de présentation hello pour son objectif désigné. Dans cet exemple, il s’agit de possibles qui hello éparse fragment de t = 1000 a une charge utile XML, ce qui concerne l’insertion d’une publicité dans une position qui est de quelques secondes plus tard.

    g. charge utile de Hello de piste partiellement fragments peut être dans différents formats (par exemple, XML, texte ou binaire), selon le scénario de hello.

### <a name="redundant-audio-track"></a>Piste audio redondante
Dans un HTTP adaptative en continu scénario classique (par exemple, la diffusion en continu lisse ou tiret), il existe souvent qu’une piste audio dans l’ensemble de la présentation hello. Contrairement aux pistes vidéo, qui ont plusieurs niveaux de qualité pour hello toochoose de client à partir de conditions d’erreur, piste audio de hello peut être un point de défaillance unique si hello ingestion du flux hello qui contient la piste audio de hello est interrompue. 

toosolve ce problème, Media Services prend en charge live ingestion des pistes audio redondant. Hello est que hello même piste audio peut être envoyé plusieurs fois dans les différents flux. Bien que hello service inscrit uniquement piste audio de hello qu’une seule fois dans le manifeste du client hello, il peut utiliser des pistes audio redondant en tant que les sauvegardes pour récupérer les fragments audio si piste audio principale de hello présente des problèmes. tooingest des pistes audio redondant, encodeur de hello doit :

1. Créez hello piste audio même dans plusieurs fragments MP4 bitstreams. pistes redondant Hello doivent être sémantiquement équivalentes, par hello même fragment horodateurs et sont interchangeables à l’en-tête de hello et niveaux de fragment.
2. Vérifiez l’entrée « audio » hello Bonjour Live Server manifeste (Section 6 dans [1]) est hello même pour les pistes audio redondants.

Hello suivant l’implémentation est recommandée pour les pistes audio redondant :

1. Envoyez chaque piste audio unique dans un flux toute seule. En outre, envoyer un flux de données redondante pour chacun de ces flux de la piste audio, où les flux deuxième hello différent hello tout d’abord uniquement par un identificateur hello Bonjour poster une URL HTTP : {protocole}  :// {adresse serveur} / {path}/Streams({identifier}) de point de publication.
2. Utiliser des flux distincts toosend hello deux le plus bas vidéo débits binaires. Chacun de ces flux DOIT également contenir une copie de chaque piste audio unique. Par exemple, quand plusieurs langues sont prises en charge, ces flux DOIVENT contenir des pistes audio pour chaque langue.
3. Utiliser un serveur distinct (encodeur) instances tooencode et envoyer des flux de données redondantes hello mentionné dans (1) et (2). 

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[image1]: ./media/media-services-fmp4-live-ingest-overview/media-services-image1.png
[image2]: ./media/media-services-fmp4-live-ingest-overview/media-services-image2.png
[image3]: ./media/media-services-fmp4-live-ingest-overview/media-services-image3.png
[image4]: ./media/media-services-fmp4-live-ingest-overview/media-services-image4.png
[image5]: ./media/media-services-fmp4-live-ingest-overview/media-services-image5.png
[image6]: ./media/media-services-fmp4-live-ingest-overview/media-services-image6.png
[image7]: ./media/media-services-fmp4-live-ingest-overview/media-services-image7.png
