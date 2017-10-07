---
title: concepts de Media Services aaaAzure | Documents Microsoft
description: "Cette rubrique fournit une vue d'ensemble des concepts liés à Azure Media Services"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: dcefc8bc-e2ea-4b38-a643-9010f4436fb5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: juliako
ms.openlocfilehash: 0a45deff32336dfcf778552f720c1ea21927951b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-concepts"></a>Concepts Azure Media Services
Cette rubrique donne une vue d’ensemble des concepts de Media Services hello plus importants.

## <a id="assets"></a>Éléments multimédias et stockage
### <a name="assets"></a>Éléments multimédias
Un [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) contient des fichiers numériques (y compris la vidéo, audio, images, collections de miniatures, pistes de texte et sous-titres) et hello métadonnées concernant ces fichiers. Une fois les fichiers numériques hello sont téléchargés dans un élément multimédia, ils peuvent être utilisés dans l’encodage et de flux de travail de diffusion en continu de hello Media Services.

Un élément multimédia est mappé tooa conteneur d’objets blob dans le compte de stockage Azure hello et fichiers hello asset de hello sont stockés en tant qu’objets BLOB de blocs dans le conteneur. Les objets blob de pages ne sont pas pris en charge par Azure Media Services.

Lorsque vous décidez quels tooupload de contenu multimédia et le magasin dans un élément multimédia, hello suivant considérations s’appliquent :

* Un élément multimédia doit contenir une seule et unique instance de contenu multimédia. Par exemple, une seule version d’un épisode d’une série TV, d’un film ou d’une publicité.
* Un élément multimédia ne doit pas contenir plusieurs rendus ou versions d’un fichier audiovisuel. Un exemple d’une utilisation incorrecte d’un élément multimédia essaient toostore plusieurs épisode TV, de publication ou de plusieurs angles de caméra à partir d’une même production à l’intérieur d’un élément multimédia. Le stockage de plusieurs rendus ou un fichier audiovisuel dans un élément multimédia, vous risquez de soumission des travaux d’encodage, diffusion en continu et la sécurisation de remise hello d’actif hello plus loin dans le flux de travail hello.  

### <a name="asset-file"></a>Fichier d’élément multimédia
Un [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) représente un fichier vidéo ou audio réel stocké dans un conteneur d’objets blob. Un fichier d’élément multimédia est toujours associé à un élément multimédia et un élément multimédia peut contenir un ou plusieurs fichiers tâche d’encodeur Media Services Hello échoue si un objet de fichier actif n’est pas associé à un fichier numérique dans un conteneur d’objets blob.

Hello **AssetFile** instance et le fichier multimédia lui-même de hello sont deux objets distincts. instance AssetFile de Hello contient des métadonnées sur le fichier du média hello, tandis que le fichier du média hello contient le contenu du média réel hello.

Vous ne devez pas essayer contenu hello de toochange de conteneurs d’objets blob qui ont été générés par Media Services sans utiliser les API de Media Services.

### <a name="asset-encryption-options"></a>Options de chiffrement d’élément multimédia
En fonction de type hello de contenu que vous souhaitez tooupload, store et remettre, Media Services propose différentes options de chiffrement que vous pouvez sélectionner.

>[!NOTE]
>Aucun chiffrement n’est utilisé. Il s’agit de valeur par défaut de hello. Quand vous utilisez cette option, votre contenu n'est pas protégé pendant le transit ou le repos dans le stockage.

Si vous envisagez de toodeliver un fichier MP4 à l’aide d’un téléchargement progressif, utilisez cette tooupload option votre contenu.

**StorageEncrypted** : utilisez cette option tooencrypt votre contenu en clair localement avec le chiffrement AES 256 bits, puis le télécharger tooAzure Storage où il est stocké et chiffré au repos. Les éléments multimédias protégés par chiffrement de stockage sont automatiquement déchiffrés et placés dans un tooencoding préalable de système de fichiers chiffrés et éventuellement RE-chiffrée toouploading préalable comme un nouvel élément multimédia de sortie. Hello est principalement utilisé pour le chiffrement de stockage lorsque vous souhaitez toosecure vos fichiers multimédias d’entrée de haute qualité avec un chiffrement renforcé au reste sur le disque. 

Dans l’ordre toodeliver un élément multimédia chiffré de stockage, vous devez configurer la stratégie de remise de hello actif afin que Media Services sache comment vous souhaitez que toodeliver votre contenu. Avant que votre élément multimédia peut être transmis en continu, hello de diffusion en continu flux et chiffrement de stockage de serveur supprime hello votre contenu à l’aide de hello spécifié de stratégie de remise (par exemple, AES, PlayReady ou aucun chiffrement). 

**CommonEncryptionProtected** -Utilisez cette option si vous souhaitez tooencrypt (ou téléchargement déjà chiffré) avec le chiffrement commun ou PlayReady DRM (par exemple, diffusion en continu lisse protégée par DRM PlayReady).

**EnvelopeEncryptionProtected** – Utilisez cette option si vous voulez tooprotect (ou téléchargement déjà protégé) HTTP Live Streaming (HLS) chiffré avec Advanced Encryption Standard (AES). Si vous téléchargez du contenu HLS déjà chiffré avec AES, il doit avoir été chiffré par Transform Manager.

### <a name="access-policy"></a>Stratégie d’accès
Un [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy) définit les autorisations (lecture, écriture et liste) et la durée de ressource de tooan d’accès. Général, vous passez un localisateur de tooa objet AccessPolicy qui serait alors les fichiers de hello tooaccess utilisé contenus dans un élément multimédia.

>[!NOTE]
>Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy). Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies). Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .

### <a name="blob-container"></a>Conteneur d’objets blob
Un conteneur d’objets blob regroupe un ensemble d’objets blob. Les conteneurs d’objets blob sont utilisés dans Media Services comme points de limite de contrôle d’accès et comme localisateurs de signature d’accès partagé (SAS, Shared Access Signature) sur les éléments multimédias. Un compte de stockage Azure peut contenir un nombre illimité de conteneurs d’objets blob. Un conteneur peut stocker un nombre illimité d’objets blob.

>[!NOTE]
> Vous ne devez pas essayer contenu hello de toochange de conteneurs d’objets blob qui ont été générés par Media Services sans utiliser les API de Media Services.
> 
> 

### <a id="locators"></a>Localisateurs
[Recherche](https://docs.microsoft.com/rest/api/media/operations/locator)s offrent un hello de tooaccess de point d’entrée de fichiers contenus dans un élément multimédia. Une stratégie d’accès est utilisé toodefine hello autorisations et la durée pendant laquelle un client a tooa d’accès donné asset. Localisateurs peuvent avoir une relation à plusieurs tooone avec une stratégie d’accès, telles que différents localisateurs peuvent fournir différentes heures de démarrage et les clients toodifferent de types de connexion lorsque vous utilisez tous les hello même autorisation et les paramètres de durée ; Toutefois, en raison d’une restriction de stratégie d’accès partagé définie par les services de stockage Azure, vous ne peut pas avoir plus de cinq localisateurs uniques associés à un élément multimédia donné à la fois. 

Media Services prend en charge deux types de localisateurs : les localisateurs OnDemandOrigin, utilisés toostream media (par exemple, MPEG DASH, HLS ou Smooth Streaming) ou télécharger progressivement les médias et les localisateurs d’URL SAS tooupload utilisé ou téléchargement media de signalement fichiers to\from stockage Azure. 

>[!NOTE]
>autorisation de liste Hello (AccessPermissions.List) ne doit pas être utilisée lors de la création d’un localisateur OnDemandOrigin. 

### <a name="storage-account"></a>Compte de stockage
Tous les accès tooAzure stockage s’effectue via un compte de stockage. Un compte Media Services peut être associé à un ou plusieurs comptes de stockage. Un compte peut contenir un nombre illimité de conteneurs, tant que la taille totale ne dépasse pas 500 To par compte de stockage.  Media Services fournit des outils tooallow au niveau du Kit de développement logiciel vous toomanage plusieurs comptes de stockage et de charge équilibrent la distribution hello de vos éléments multimédias pendant le téléchargement des comptes toothese en fonction de distribution mesurée ou aléatoire. Pour plus d’informations, consultez la page [Utilisation d’Azure Storage](https://msdn.microsoft.com/library/azure/dn767951.aspx). 

## <a name="jobs-and-tasks"></a>Travaux et tâches
A [travail](https://https://docs.microsoft.com/rest/api/media/operations/job) est généralement utilisé tooprocess (par exemple, l’index ou encoder) une présentation audio ou vidéo. Si vous traitez plusieurs vidéos, créez un travail pour chaque toobe vidéo encodée.

Un travail contient des métadonnées sur toobe de traitement de hello effectuée. Chaque travail contient une ou plusieurs [tâche](https://docs.microsoft.com/rest/api/media/operations/task)s qui spécifient une tâche de traitement atomique, ses éléments multimédias d’entrée, ses éléments multimédias de sortie, un processeur multimédia et ses paramètres associés. Tâches au sein d’un travail peuvent être chaînés ensemble, où hello élément multimédia de sortie d’une tâche est donné comme hello d’entrée de la tâche suivante asset toohello. De cette façon, un travail peut contenir tout traitement hello nécessaire pour une présentation multimédia.

## <a id="encoding"></a>Encodage
Azure Media Services propose plusieurs options pour l’encodage de hello de support dans le cloud de hello.

Lorsque vous démarrez avec Media Services, il est différence de hello toounderstand important entre les codecs et formats de fichier.
Les codecs sont des logiciels de hello qui implémente les algorithmes de compression/décompression hello tandis que les formats de fichier sont des conteneurs qui contiennent la vidéo de hello compressé.

Media Services fournit l’empaquetage dynamique qui vous permet de toodeliver votre vitesse de transmission adaptative MP4 ou Smooth Streaming encodé contenu de diffusion en continu des formats pris en charge par Media Services (MPEG DASH, HLS, Smooth Streaming) sans que vous ayez toore-package dans ces formats de diffusion en continu.

avantage tootake de [empaquetage dynamique](media-services-dynamic-packaging-overview.md), vous devez tooencode votre fichier mezzanine (source) dans un ensemble de fichiers MP4 ou de fichiers de diffusion en continu lisse à débit adaptatif et que vous avez au moins une terminaison de diffusion en continu de standard ou premium dans l’état démarré.

Media Services prend en charge hello suivant encodeurs à la demande qui sont décrites dans cet article :

* [Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Media Encoder Premium Workflow](media-services-encode-asset.md#media-encoder-premium-workflow)

Pour plus d’informations sur les encodeurs pris en charge, consultez la page [Encodeurs](media-services-encode-asset.md).

## <a name="live-streaming"></a>Vidéo en flux continu
Dans Azure Media Services, un canal représente un pipeline de traitement du contenu de diffusion en direct. Un canal reçoit des flux d’entrée en direct de l’une des deux manières suivantes :

* Un encodeur dynamique local envoie plusieurs débits RTMP ou le canal de toohello Smooth Streaming (MP4 fragmenté). Vous pouvez utiliser hello suivant encodeurs en temps réel qui produisent plusieurs débits binaires de la diffusion en continu lisse : MediaExcel Ateme, imaginez, Envivio, Cisco et Communications élémentaire. Hello suivants encodeurs en temps réel de sortie RTMP : les encodeurs Adobe Flash Live encodeur Telestream Wirecast, Teradek, Haivision et Tricaster. Hello flux ingérés passent par les canaux sans aucun autre le transcodage et l’encodage. Lorsqu’il est demandé, Media Services diffuse hello flux toocustomers.
* Un flux à débit binaire unique (dans un des hello suivant formats : RTP (MPEG-TS)), RTMP ou Smooth Streaming (MP4 fragmenté)) est envoyé de canal toohello est activé tooperform dynamique encodage avec Media Services. Hello canal effectue ensuite l’encodage dynamique de hello entrant à débit binaire unique flux tooa débits (adaptatif) flux vidéo. Lorsqu’il est demandé, Media Services diffuse hello flux toocustomers.

### <a name="channel"></a>Canal
Dans Media Services, les [canaux](https://docs.microsoft.com/rest/api/media/operations/channel)sont responsables du traitement du contenu de vidéo en flux continu. Un canal fournit un point de terminaison d’entrée (URL de réception) que vous fournissez ensuite tooa TRANSCODEUR en temps réel. canal de Hello reçoit des flux d’entrée live d’hello TRANSCODEUR en temps réel et la rend disponible pour la diffusion en continu via un ou plusieurs Streamingendpoint. Les canaux fournissent également un aperçu point de terminaison (URL d’aperçu) que vous utilisez toopreview et validez votre flux de données avant de poursuivre le traitement et de remise.

Vous pouvez obtenir hello réception URL et l’URL d’aperçu hello lorsque vous créez le canal de hello. tooget ces URL, le canal de hello n’a pas toobe en état de hello a démarré. Lorsque vous êtes prêt toostart transmettre des données à partir d’un TRANSCODEUR en temps réel à un canal de hello, hello doit être démarré. Une fois que hello TRANSCODEUR en temps réel démarre la réception de données, vous pouvez afficher un aperçu de votre flux de données.

Chaque compte Media Services peut contenir plusieurs canaux, plusieurs programmes et plusieurs StreamingEndpoints. Selon les besoins de la bande passante et la sécurité des hello, les services StreamingEndpoint peuvent être dédié tooone canaux ou plus. N’importe quel StreamingEndpoint peut assurer l’extraction à partir de n’importe quel canal.

### <a name="program-event"></a>Programme (événement)
A [programme (événement)](https://docs.microsoft.com/rest/api/media/operations/program) vous permet de la publication toocontrol hello et stockage des segments dans un flux en direct. Les canaux gèrent les programmes (événements). Hello relation de canal et le programme est un support similaire tootraditional où un canal possède un flux constant de contenu et un programme est événements étendue toosome a expiré sur le canal.
Vous pouvez spécifier le nombre de hello d’heures que vous voulez tooretain hello enregistrée contenu pour le programme de hello en définissant un hello **ArchiveWindowLength** propriété. Cette valeur peut être définie à partir d’un minimum de 5 minutes tooa 25 heures maximum.

ArchiveWindowLength détermine également hello durée maximale pendant laquelle les clients peuvent effectuer des recherches dans le temps à partir de la position de diffusion en continu hello actuel. Programmes peuvent s’exécuter sur la durée spécifiée hello, mais le contenu qui se trouve derrière la longueur de la fenêtre hello est ignoré en permanence. La valeur de cette propriété détermine également la durée pendant laquelle hello client manifestes peuvent atteindre.

Chaque programme (événement) est associé à un élément multimédia. programme de hello toopublish vous devez créer un localisateur pour hello associés actif. Ce localisateur activera toobuild une URL de diffusion en continu que vous pouvez fournir tooyour clients.

Un canal prend en charge jusqu'à toothree qui s’exécutent simultanément des programmes, vous pouvez créer plusieurs archives de hello même flux entrant. Cela vous permet de toopublish et archivage de différentes parties d’un événement en fonction des besoins. Par exemple, vos exigences d’entreprise est tooarchive 6 heures d’un programme, mais toobroadcast uniquement les 10 dernières minutes. tooaccomplish, vous devez toocreate deux des programmes qui s’exécutent simultanément. Un programme a la valeur tooarchive d’événement de hello les 6 heures, mais les programme hello ne sont pas publié. Hello autre programme est ensemble tooarchive pendant 10 minutes et ce programme est publié.

Pour plus d'informations, consultez les pages suivantes :

* [Utilisation de canaux est à activé tooPerform Live encodage avec Azure Media Services](media-services-manage-live-encoder-enabled-channels.md)
* [Utilisation des canaux recevant un flux dynamique à débit binaire multiple provenant d’encodeurs locaux](media-services-live-streaming-with-onprem-encoders.md)
* [Quotas et limitations](media-services-quotas-and-limitations.md)

## <a name="protecting-content"></a>Protection du contenu
### <a name="dynamic-encryption"></a>Chiffrement dynamique
Azure Media Services permet de vous toosecure votre média à partir de l’heure hello qu'il quitte votre ordinateur via le stockage, le traitement et la remise. Media Services vous permet de toodeliver votre contenu chiffré dynamiquement avec la norme AES (Advanced Encryption) (à l’aide de clés de chiffrement 128 bits) et le chiffrement commun (CENC) à l’aide de PlayReady et/ou Widevine DRM. Media Services fournit également un service de distribution de clés AES et les clients tooauthorized de licences PlayReady.

Actuellement, vous pouvez chiffrer hello suivant les formats de diffusion en continu : TLS, MPEG DASH et diffusion en continu lisse. Vous ne pouvez pas chiffrer les téléchargements progressifs.

Si vous souhaitez un élément multimédia pour tooencrypt de Media Services, vous devez tooassociate une clé de chiffrement (CommonEncryption ou EnvelopeEncryption) avec votre élément multimédia et également configurer les stratégies d’autorisation pour la clé de hello.

Si vous voulez toostream un élément multimédia chiffré de stockage, vous devez configurer la stratégie de remise de hello actif dans l’ordre toospecify comment vous souhaitez que toodeliver votre élément multimédia.

Lorsqu’un flux de données est demandée par un lecteur, Media Services utilise hello spécifié toodynamically clé chiffrer votre contenu à l’aide d’un chiffrement d’enveloppe (avec AES) ou un chiffrement commun (avec PlayReady ou Widevine). flux de données toodecrypt hello, le lecteur hello demande clé de hello de service de distribution de clés hello. toodecide soit ou non d’utilisateur de hello autorisé clé de hello tooget, hello évalue les stratégies d’autorisation hello que vous avez spécifié pour la clé de hello.

### <a name="token-restriction"></a>Restriction à jeton
Hello contenu clé peut avoir une ou plusieurs restrictions d’autorisation : ouverte, restriction de jeton ou restrictions d’adresse IP. stratégie de restriction token Hello doit être accompagné d’un jeton émis par un Service (jeton de sécurité). Media Services prend en charge les jetons dans les formats de jetons SWT (Simple Web Tokens) hello et JSON Web Token (JWT). Media Services ne fournit pas de services de jeton sécurisé. Vous pouvez créer un STS personnalisé ou tirer parti des jetons de tooissue Microsoft Azure ACS. Hello STS doit être configuré toocreate un jeton signé avec hello spécifié clé et émettre les revendications que vous avez spécifié dans la configuration de restriction token hello. les revendications Hello Media Services, service de distribution de clés renvoie hello demandé hello et clé (ou licence) client toohello si hello jeton est valide dans hello jeton correspondent à celles configurées pour la clé de hello (ou licence).

Lorsque vous configurez la stratégie de restriction token hello, vous devez spécifier la clé de vérification principale hello, l’émetteur et paramètres de l’audience. clé de vérification principale Hello contient hello clé que le jeton de hello a été signé avec, l’émetteur est hello sécurisé STS qui émet le jeton de hello. audience Hello (parfois appelé étendue) décrit l’intention de hello du jeton de hello ou autorise l’accès au jeton de hello ressource hello. Hello service de distribution de clés de Media Services valide que ces valeurs dans le jeton de hello correspondent aux valeurs hello modèle de hello.

Pour plus d’informations, consultez hello suivant des articles :

[Vue d’ensemble de la protection du contenu](media-services-content-protection-overview.md)
[Protéger avec AES-128](media-services-protect-with-aes128.md)
[ Protéger par DRM](media-services-protect-with-drm.md)

## <a name="delivering"></a>Remise
### <a id="dynamic_packaging"></a>Empaquetage dynamique
Lorsque vous travaillez avec Media Services, il est recommandé tooencode vos fichiers mezzanine en un MP4 à débit adaptatif définie et puis convertir hello toohello format souhaité à l’aide de hello [empaquetage dynamique](media-services-dynamic-packaging-overview.md).

### <a name="streaming-endpoint"></a>point de terminaison de diffusion en continu
Un StreamingEndpoint représente un service de diffusion en continu qui peut fournir du contenu directement de l’application de lecteur tooa client ou tooa réseau de distribution de contenu (CDN) pour une distribution ultérieure (Azure Media Services fournit désormais l’intégration du CDN Azure hello.) hello flux sortant à partir d’un service de point de terminaison de diffusion en continu peut être un flux en direct ou à la demande à un élément multimédia vidéo dans votre compte Media Services. Les clients de Media Services choisir soit un **Standard** diffusion en continu de point de terminaison ou une ou plusieurs **Premium** points de terminaison, en fonction des besoins de tootheir de diffusion en continu. Le point de terminaison de streaming standard convient à la plupart des charges de travail de diffusion en continu. 

Le point de terminaison de streaming standard convient à la plupart des charges de travail de diffusion en continu. Points de terminaison standard de diffusion en continu offrent hello flexibilité toodeliver votre contenu toovirtually chaque appareil via l’empaquetage dynamique dans Smooth Streaming de HLS et MPEG-DASH, ainsi que le chiffrement dynamique de Microsoft PlayReady, Google Widevine, Apple Fairplay et AES128.  Ils également mettre à l’échelle à partir de très petits toovery large public avec des milliers d’utilisateurs simultanés via l’intégration d’Azure CDN. Si vous avez une charge de travail avancée ou vos exigences de capacité de diffusion en continu ne tiennent pas toostandard cibles de débit de point de terminaison de diffusion en continu ou que vous souhaitiez capacité hello toocontrol hello StreamingEndpoint toohandle croissante de bande passante service a besoin, il est recommandé unités d’échelle tooallocate (également appelé premium unités de diffusion en continu).

Il est recommandé de mise en package dynamique toouse et/ou le chiffrement dynamique.

>[!NOTE]
>Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état. 

Pour plus d’informations, consultez [cette rubrique](media-services-portal-manage-streaming-endpoints.md) .

Par défaut, vous pouvez avoir des points de terminaison de diffusion en continu too2 dans votre compte Media Services. toorequest une limite plus élevée, consultez [Quotas et limitations](media-services-quotas-and-limitations.md).

Vous êtes facturé uniquement lorsque votre StreamingEndpoint est en cours d’exécution.

### <a name="asset-delivery-policy"></a>Stratégie de remise d’élément multimédia
Une des hello étapes Bonjour Media Services consiste à configurer des flux de travail de diffusion de contenu [des stratégies de remise pour les ressources ](https://docs.microsoft.com/rest/api/media/operations/assetdeliverypolicy)que vous souhaitez toobe transmis en continu. stratégie de livraison des actifs Hello indique comment vous souhaitez pour votre toobe asset remis à Media Services : dans le protocole de diffusion en continu doit votre élément multimédia dynamiquement packagé (par exemple, MPEG DASH, HLS, Smooth Streaming ou tous), vous souhaitez toodynamically ou non chiffrer votre élément multimédia et comment (enveloppe ou chiffrement commun).

Si vous avez une ressource chiffrée de stockage, avant que votre élément multimédia peut être transmis en continu, hello de diffusion en continu flux et chiffrement de stockage de serveur supprime hello votre contenu à l’aide de hello spécifié de stratégie de remise. Par exemple, toodeliver votre élément multimédia chiffré avec la clé de chiffrement Advanced Encryption Standard (AES), tooDynamicEnvelopeEncryption de type de stratégie de hello ensemble. chiffrement de stockage tooremove et asset hello de flux Bonjour clair, la valeur tooNoDynamicEncryption de type hello stratégie.

### <a name="progressive-download"></a>Téléchargement progressif
Le téléchargement progressif vous permet de toostart lecture du contenu multimédia avant que l’intégralité du fichier hello a été téléchargé. Seul un fichier MP4 peut être téléchargé progressivement.

>[!NOTE]
>Vous devez déchiffrer des éléments multimédias chiffrés si vous souhaitez qu’ils toobe disponible pour le téléchargement progressif.

URL de téléchargement progressif aux utilisateurs tooprovide, vous devez d’abord créer un localisateur OnDemandOrigin. Création de localisateur hello, donne hello de base asset toohello de chemin d’accès. Vous devez ensuite le nom de hello tooappend de fichier MP4. Par exemple :

http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

### <a name="streaming-urls"></a>URL de diffusion
Diffusion en continu votre contenu tooclients. tooprovide des utilisateurs avec des URL de diffusion en continu, vous devez créer un localisateur OnDemandOrigin. Création de localisateur hello, donne hello de base asset toohello chemin d’accès qui contient le contenu hello toostream. Toutefois, toostream en mesure de toobe ce contenu, vous devez toomodify ce chemin d’accès supplémentaire. tooconstruct une URL complète toohello fichier manifeste de diffusion en continu, vous devez concaténer de chemin d’accès du localisateur hello valeur et hello manifeste (nom_fichier.ISM) nom du fichier. Ensuite, ajoutez /Manifest et un chemin d’accès du localisateur de toohello format approprié (si nécessaire).

Vous pouvez aussi diffuser votre contenu via une connexion SSL. toodo, assurez-vous que votre Démarrer URL de diffusion en continu avec HTTPS. Actuellement, AMS ne prend pas en charge SSL avec les domaines personnalisés.  

>[!NOTE]
>Vous pouvez uniquement diffuser via le protocole SSL si hello point de terminaison à partir duquel vous distribuez votre contenu de diffusion en continu a été créé après le 10 septembre 2014. Si votre URL de diffusion en continu est basés sur hello de diffusion en continu des points de terminaison créés après le 10 septembre, hello URL contient « streaming.mediaservices.windows.net » (hello nouveau format). URL de diffusion en continu qui contiennent « origin.mediaservices.windows.net » (hello ancien format) ne prennent pas en charge SSL. Si votre URL est dans un ancien format de hello et que vous souhaitez toostream en mesure de toobe via le protocole SSL, créez un nouveau point de terminaison de diffusion en continu. Utilisez des URL créés en fonction de hello new de diffusion en continu toostream de point de terminaison votre contenu via le protocole SSL.

Hello suivant liste décrit les différents formats de diffusion en continu et fournit des exemples :

* Smooth Streaming

{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest

* MPEG DASH

{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)

* Apple HTTP Live Streaming (HLS) V4

{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)

* Apple HTTP Live Streaming (HLS) V3

{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

