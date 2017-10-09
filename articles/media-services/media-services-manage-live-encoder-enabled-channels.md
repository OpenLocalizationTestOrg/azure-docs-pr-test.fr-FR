---
title: "aaaLive de diffusion en continu à l’aide de flux de débits Azure Media Services toocreate | Documents Microsoft"
description: "Cette rubrique explique comment tooset un canal qui reçoit un débit binaire unique live flux à partir d’un encodeur local et qu’il effectue ensuite les flux de vitesse de transmission de tooadaptive codage dynamique avec Media Services. Hello flux peut ensuite être remis tooclient les applications de lecture via un ou plusieurs points de diffusion en continu, à l’aide de hello suite de protocoles de diffusion en continu adaptatives : TLS, le contenu Smooth Streaming, MPEG DASH."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 30ce6556-b0ff-46d8-a15d-5f10e4c360e2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: a8bbdd1570cc9a11bfc2de7bb4ceb9006cc25534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams"></a>Diffusion en continu à l’aide de flux de débits toocreate Azure Media Services
## <a name="overview"></a>Vue d'ensemble
Dans Azure Media Services (AMS), un **canal** représente un pipeline de traitement du contenu vidéo en flux continu. Un **canal** reçoit des flux d’entrée live de l’une des deux manières suivantes :

* Un encodeur dynamique local envoie un flux unique à plusieurs débits canal toohello est activé tooperform live encodage avec Media Services dans un des hello suivant formats : RTP (MPEG-TS), RTMP ou Smooth Streaming (MP4 fragmenté). Hello canal effectue ensuite l’encodage dynamique de hello entrant à débit binaire unique flux tooa débits (adaptatif) flux vidéo. Lorsqu’il est demandé, Media Services diffuse hello flux toocustomers.
* Un encodeur dynamique local envoie plusieurs débits **RTMP** ou **Smooth Streaming** canal toohello (MP4 fragmenté) qui n’est pas activée tooperform dynamique encodage avec AMS. flux de données Hello ingéré passent par **canal**s sans traitement supplémentaire. Cette méthode est appelée **pass-through**. Vous pouvez utiliser hello suivant encodeurs en temps réel qui produisent plusieurs débits binaires de la diffusion en continu lisse : MediaExcel Ateme, imaginez, Envivio, Cisco et Communications élémentaire. Hello suivants encodeurs en temps réel de sortie RTMP : les encodeurs Adobe Flash Media en direct encodeur (FMLE), Telestream Wirecast, Haivision, Teradek et Tricaster.  Un encodeur en temps réel peut également envoyer un canal tooa du flux à débit binaire unique qui n’est pas activée pour l’encodage live, mais qui n’est pas recommandé. Lorsqu’il est demandé, Media Services diffuse hello flux toocustomers.
  
  > [!NOTE]
  > À l’aide d’une méthode directe d’est le moyen le plus économique hello toodo la diffusion en continu.
  > 
  > 

En commençant avec la version de hello 2.10 de Media Services, lorsque vous créez un canal, vous pouvez spécifier la façon dont vous souhaitez pour votre flux d’entrée du canal tooreceive hello et si vous souhaitez que pour hello canal tooperform live codage de votre flux de données. Deux options s'offrent à vous :

* **Aucun** : spécifiez cette valeur, si vous envisagez de toouse un encodeur dynamique local qui produira des flux de débits (un flux direct). Dans ce cas, les flux entrants hello transmis toohello de sortie sans encodage. Il s’agit de comportement hello d’une version antérieure too2.10 de canal.  Pour plus d’informations sur l’utilisation des canaux de ce type, consultez [Vidéo en flux continu avec des encodeurs locaux qui créent des flux à vitesses de transmission multiples](media-services-live-streaming-with-onprem-encoders.md).
* **Standard** – choisissez cette valeur, si vous envisagez de toouse Media Services tooencode votre flux de débits toomulti de flux en continu à débit binaire unique. N’oubliez pas qu’il existe un impact sur la facturation pour l’encodage dynamique et vous devez vous rappeler que sans toucher à un canal en direct de codage de hello état « Actif » occasionnent des frais de facturation.  Il est recommandé d’arrêter immédiatement vos canaux en cours d’exécution après votre événement de diffusion en continu en direct est tooavoid complète des frais supplémentaires de toutes les heures.

> [!NOTE]
> Cette rubrique décrit les attributs de canaux qui sont activés encodage dynamique tooperform (**Standard** type d’encodage). Pour plus d’informations sur l’utilisation des canaux qui ne sont pas activé l’encodage dynamique tooperform, consultez [la diffusion en continu en direct avec les encodeurs locaux qui créent des flux de débits](media-services-live-streaming-with-onprem-encoders.md).
> 
> Assurez-vous que tooreview hello [considérations](media-services-manage-live-encoder-enabled-channels.md#Considerations) section.
> 
> 

## <a name="billing-implications"></a>Implications de facturation
Un canal d’encodage live commence dès que l’état de transition trop « Running » via hello API de facturation.   Vous pouvez également afficher les état hello Bonjour portail Azure ou dans l’outil d’Azure Media Services Explorer hello (http://aka.ms/amse).

Hello tableau suivant montre comment mappent les États des canaux États toobilling Bonjour API et portail Azure. Notez que les États hello sont légèrement différentes entre hello API et UX de portail. Dès qu’un canal est en état hello « En cours d’exécution » via hello API ou dans hello « Prêt » ou « Streaming » Bonjour portail Azure, la facturation sera active.
Canal de hello toostop de facturation vous davantage, vous avez tooStop hello canal via les API de hello ou Bonjour portail Azure.
Vous êtes responsable de l’arrêt de vos canaux lorsque vous avez terminé avec le canal d’encodage live hello.  Échec toostop un canal d’encodage entraîne la facturation continue.

### <a id="states"></a>États de canal ainsi que leur mappage toohello en mode de facturation
état actuel de Hello d’un canal. Les valeurs possibles incluent :

* **Arrêté**. Il s’agit état initial de hello Hello canal après sa création (sauf si le démarrage automatique a été sélectionné dans le portail de hello.) Aucune facturation ne survient dans cet état. Dans cet état, les propriétés de canal hello peuvent être mis à jour, mais de diffusion en continu n’est pas autorisée.
* **Démarrage en cours**. Hello canal est en cours de démarrage. Aucune facturation ne survient dans cet état. Aucune mise à jour ni aucun streaming ne sont autorisés durant cet état. Si une erreur se produit, hello canal retourne toohello état arrêté.
* **Exécution en cours**. Hello canal est capable de traiter des flux live. Il facture désormais l'utilisation. Vous devez arrêter tooprevent de canal hello davantage de facturation. 
* **En cours d’arrêt**. Hello canal est en cours d’arrêt. Aucune facturation ne survient dans cet état de transition. Aucune mise à jour ou diffusion en continu n’est autorisée durant cet état.
* **Suppression en cours**. Hello canal est en cours de suppression. Aucune facturation ne survient dans cet état de transition. Aucune mise à jour ni aucun streaming ne sont autorisés durant cet état.

Hello tableau suivant montre comment canal indique le mode de facturation toohello mappage. 

| État du canal | Indicateurs de l’interface utilisateur du portail | Existe-t-il une facturation ? |
| --- | --- | --- |
| Démarrage en cours |Démarrage en cours |Aucun (état transitoire) |
| Exécution en cours |Prêt (pas de programmes en cours d’exécution)<br/>ou<br/>Diffusion en continu (au moins un programme en cours d'exécution) |OUI |
| En cours d’arrêt |En cours d’arrêt |Aucun (état transitoire) |
| Arrêté |Arrêté |Non |

### <a name="automatic-shut-off-for-unused-channels"></a>Fermeture automatique des canaux inutilisés
Depuis le 25 janvier 2016, Media Services a déployé une mise à jour qui ferme automatiquement un canal (avec encodage en temps réel activé) s’il reste non utilisé pendant une longue période. Cela s’applique tooChannels n’ayant aucun programme active, et qui n’ont pas reçu une contribution d’entrée de flux pour une période prolongée.

seuil de Hello pendant une période inutilisée nominalement est de 12 heures, mais il est sujet toochange.

## <a name="live-encoding-workflow"></a>Flux de travail d'encodage en temps réel
Hello diagramme suivant représente un flux de travail de diffusion en continu live où un canal reçoit un flux à débit binaire unique dans un des hello suivant protocoles : RTMP, diffusion en continu lisse ou RTP (MPEG-TS) ; Il encode ensuite des flux de débits tooa hello flux. 

![Flux de travail live][live-overview]

## <a id="scenario"></a>Scénario courant de diffusion dynamique en continu
Hello Voici les étapes générales nécessaires à la création d’applications de diffusion en continu dynamiques communes.

> [!NOTE]
> Actuellement, hello maximum recommandé de durée d’un événement en direct est de 8 heures. Si vous avez besoin d’un canal de toorun pour de longues périodes, contactez amslived Microsoft.com. N’oubliez pas qu’il existe un impact sur la facturation pour l’encodage dynamique et vous devez vous rappeler que sans toucher à un canal en direct de codage de hello état « Actif » occasionnent des frais de facturation toutes les heures.  Il est recommandé d’arrêter immédiatement vos canaux en cours d’exécution après votre événement de diffusion en continu en direct est tooavoid complète des frais supplémentaires de toutes les heures. 
> 
> 

1. Connecter un ordinateur de tooa caméra vidéo. Lancer et configurer un encodeur dynamique local qui peut afficher un **unique** flux à débit binaire de l’une des hello suite de protocoles : RTMP, diffusion en continu lisse ou RTP (MPEG-TS). 
   
    Cette étape peut également être effectuée après la création du canal.
2. Créez et démarrez un canal. 
3. URL de réception récupérer hello canal. 
   
    URL de réception Hello est utilisé par hello encodeur en temps réel toosend hello flux toohello canal.
4. Récupérer l’URL d’aperçu hello canal. 
   
    Utilisez cette tooverify URL que votre canal reçoit correctement les flux live hello.
5. Créez un programme. 
   
    Lors de l’aide de hello portail Azure, création d’un programme crée également un élément multimédia. 
   
    Lorsque vous utilisez le Kit de développement .NET ou REST vous devez toocreate un élément multimédia et toouse cette ressource lors de la création d’un programme. 
6. Publier asset hello associé hello du programme.   
   
    >[!NOTE]
    >Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. Hello, point de terminaison à partir de laquelle vous souhaitez toostream contenu de diffusion en continu a toobe Bonjour **en cours d’exécution** état. 
    
7. Démarrer le programme de hello lorsque vous êtes prêt toostart diffusion et l’archivage.
8. Si vous le souhaitez, encodeur en direct de hello peut être signalé toostart une publication. publication de Hello est insérée dans le flux de sortie hello.
9. Arrêter le programme de hello chaque fois que vous souhaitez toostop de diffusion en continu et l’archivage des événements de hello.
10. Supprimer le programme de hello (et éventuellement supprimer actif de hello).   

> [!NOTE]
> Il est très important pas tooforget tooStop un canal d’encodage Live. N’oubliez pas qu’il existe un horaire de l’impact de l’encodage dynamique de facturation et vous devez vous rappeler que sans toucher à un canal en direct de codage de hello état « Actif » occasionnent des frais de facturation.  Il est recommandé d’arrêter immédiatement vos canaux en cours d’exécution après votre événement de diffusion en continu en direct est tooavoid complète des frais supplémentaires de toutes les heures. 
> 
> 

## <a id="channel"></a>Configurations de l’entrée (réception) du canal
### <a id="Ingest_Protocols"></a>Protocole de streaming de réception
Si hello **Type d’encodeur** est défini trop**Standard**, les options valides sont :

* **RTP** (MPEG-TS) : flux de transport MPEG-2 via RTP.  
* **RTMP**
* **MP4 fragmenté** (Smooth Streaming) à débit binaire unique

#### <a name="rtp-mpeg-ts---mpeg-2-transport-stream-over-rtp"></a>RTP (MPEG-TS) : flux de transport MPEG-2 via RTP.
Cas d’utilisation classique : 

Professionnels chaînes de télévision fonctionnent généralement avec des encodeurs en temps réel local haut de gamme de fournisseurs comme toosend Technologies élémentaire, Ericsson, Ateme, Imagine ou Envivio un flux de données. Ils sont souvent utilisés conjointement avec un service informatique et des réseaux privés.

Considérations :

* utilisation de Hello d’un flux de transport de programme unique (SPTS) d’entrée est fortement recommandée. 
* Vous pouvez entrer des flux de données audio too8 à l’aide de MPEG-2 TS sur RTP. 
* les flux vidéo Hello doivent avoir un débit binaire moyen ci-dessous 15 Mbits/s
* Hello d’agrégation débit binaire moyen du flux de données audio hello doit être inférieure à 1 Mbit/s
* Suivantes sont hello codecs pris en charge :
  
  * Vidéo MPEG-2/H.262 
    
    * Profil Main (4:2:0)
    * Profil High (4:2:0, 4:2:2)
    * Profil 422 (4:2:0, 4:2:2)
  * Vidéo MPEG-4 AVC/H.264  
    
    * Profil Baseline, Main, High (8 bits 4:2:0)
    * Profil High 10 (10 bits 4:2:0)
    * Profil High 422 (10 bits 4:2:2)
  * Audio MPEG-2 AAC-LC 
    
    * Mono, stéréo, Surround (5.1, 7.1)
    * Format ADTS style MPEG-2
  * Dolby Digital (AC-3) Audio 
    
    * Mono, stéréo, Surround (5.1, 7.1)
  * Audio MPEG (couches II et III) 
    
    * Mono, stéréo
* Les encodeurs de diffusion recommandés sont les suivants :
  
  * Imagine Communications Selenio ENC 1
  * Imagine Communications Selenio ENC 2
  * Elemental Live

#### <a id="single_bitrate_RTMP"></a>RTMP à débit binaire unique
Considérations :

* les flux entrants Hello ne peut pas contenir plusieurs débits binaires vidéo
* les flux vidéo Hello doivent avoir un débit binaire moyen ci-dessous 15 Mbits/s
* les flux audio Hello doivent avoir un débit binaire moyen ci-dessous 1 Mbit/s
* Suivantes sont hello codecs pris en charge :
* Vidéo MPEG-4 AVC/H.264
* Profil Baseline, Main, High (8 bits 4:2:0)
* Profil High 10 (10 bits 4:2:0)
* Profil High 422 (10 bits 4:2:2)
* Audio MPEG-2 AAC-LC
* Mono, stéréo, Surround (5.1, 7.1)
* Fréquence d'échantillonnage 44,1 kHz
* Format ADTS style MPEG-2
* Les encodeurs recommandés sont les suivants :
* Telestream Wirecast
* Flash Media Live Encoder

#### <a name="single-bitrate-fragmented-mp4-smooth-streaming"></a>MP4 fragmenté (Smooth Streaming) à débit binaire unique
Cas d’utilisation classique :

Utiliser des encodeurs en temps réel sur site auprès de fournisseurs tels que des Technologies élémentaire, Ericsson, Ateme, flux d’entrée hello toosend Envivio sur hello ouvrir internet tooa à proximité du centre de données Azure.

Considérations :

Identique au flux [RTMP à débit binaire unique](media-services-manage-live-encoder-enabled-channels.md#single_bitrate_RTMP).

#### <a name="other-considerations"></a>Autres points à considérer
* Vous ne pouvez modifier le protocole d’entrée de hello lors hello canal ou ses programmes associés sont en cours d’exécution. Si vous avez besoin d’autres protocoles, vous devez créer des canaux distincts pour chaque protocole d’entrée.
* Résolution maximale de flux vidéo entrant de hello est 1920 x 1080 pixels et au maximum 60 champs/seconde si entrelacée, ou 30 images/seconde si progressif.

### <a name="ingest-urls-endpoints"></a>URL (points de terminaison) de réception
Un canal fournit un point de terminaison d’entrée (URL de réception) que vous spécifiez dans l’encodeur en temps réel de hello, afin de l’encodeur de hello pouvez pousser le flux tooyour canaux.

Vous pouvez obtenir hello URL de réception une fois que vous créez un canal. tooget ces URL, hello canal n’a pas toobe Bonjour **en cours d’exécution** état. Lorsque vous êtes prêt toostart transmettre des données à hello canal, il doit être Bonjour **en cours d’exécution** état. Une fois que le canal de hello démarre la réception de données, vous pouvez afficher un aperçu de votre flux de données via une URL d’aperçu hello.

Vous avez la possibilité de recevoir un flux dynamique au format MP4 fragmenté (Smooth Streaming) via une connexion SSL. tooingest via le protocole SSL, assurez-vous que tooupdate hello tooHTTPS de l’URL de réception. Notez qu’actuellement AMS ne prend pas en charge SSL avec les domaines personnalisés.  

### <a name="allowed-ip-addresses"></a>Adresses IP autorisées
Vous pouvez définir les adresses IP hello autorisées toopublish toothis vidéo channel. Les adresses IP autorisées peuvent être spécifiées en tant qu’adresses IP uniques (par exemple, '10.0.0.1'), une plage d’adresses IP utilisant une adresse IP et un masque de sous-réseau CIDR (par exemple, 10.0.0.1/22), ou une plage d’adresses IP utilisant une adresse IP et un masque de sous-réseau décimal séparé par des points (par exemple, '10.0.0.1(255.255.252.0)').

Si aucune adresse IP n’est spécifiée et qu’il n’existe pas de définition de règle, alors aucune adresse IP n’est autorisée. tooallow n’importe quelle adresse IP, créez une règle et définissez 0.0.0.0/0.

## <a name="channel-preview"></a>Aperçu du canal
### <a name="preview-urls"></a>URL d’aperçu
Les canaux fournissent un aperçu point de terminaison (URL d’aperçu) que vous utilisez toopreview et validez votre flux de données avant de poursuivre le traitement et de remise.

Vous pouvez obtenir les URL d’aperçu hello lorsque vous créez le canal de hello. tooget hello URL, le canal de hello n’a pas toobe Bonjour **en cours d’exécution** état.

Une fois que le canal de hello démarre la réception de données, vous pouvez afficher un aperçu de votre flux de données.

> [!NOTE]
> En flux d’aperçu hello ne peut plus être remis dans MP4 fragmenté (Smooth Streaming) de format, quelle que soit la hello spécifié type d’entrée. Vous pouvez utiliser hello [http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor) lecteur tootest hello contenu Smooth Streaming. Vous pouvez également utiliser un lecteur hébergé dans hello tooview portail Azure, votre flux de données.
> 
> 

### <a name="allowed-ip-addresses"></a>Adresses IP autorisées
Vous pouvez définir les adresses IP hello qui sont autorisés à point de terminaison tooconnect toohello aperçu. Si aucune adresse IP n’est spécifiée, alors toutes les adresses IP seront autorisées. Les adresses IP autorisées peuvent être spécifiées en tant qu’adresses IP uniques (par exemple, 10.0.0.1), une plage d’adresses IP utilisant une adresse IP et un masque de sous-réseau CIDR (par exemple, 10.0.0.1/22), ou une plage d’adresses IP utilisant une adresse IP et un masque de sous-réseau décimal séparé par des points (par exemple, 10.0.0.1[255.255.252.0]).

## <a name="live-encoding-settings"></a>Paramètres d’encodage en temps réel
Cette section décrit comment les paramètres hello pour l’encodeur en direct de hello dans hello canal peuvent être ajustée lorsque hello **Type de codage** d’un canal est défini trop**Standard**.

> [!NOTE]
> Seul RTP est pris en charge pour la saisie multilingue lors de la saisie de pistes multilingues et l'encodage en temps réel. Vous pouvez définir des flux de données audio too8 à l’aide de MPEG-2 TS sur RTP. La réception de plusieurs pistes audio avec RTMP ou Smooth Streaming n'est actuellement pas prise en charge. Lors de l’exécution avec l’encodage live [local live encode](media-services-live-streaming-with-onprem-encoders.md), il en existe aucune limitation de ce type, car tout ce qui est envoyé tooAMS passe par un canal sans traitement supplémentaire.
> 
> 

### <a name="ad-marker-source"></a>Source de marqueur de publicité
Vous pouvez spécifier la source de hello pour les signaux marqueurs publicitaires. Valeur par défaut est **Api**, ce qui signifie qu’encodeur live hello dans hello canal doit écouter tooan asynchrone **Ad marqueur API**.

Bonjour autre option valide est **Scte35** (autorisé uniquement si l’acquisition de hello protocole de diffusion en continu a la valeur tooRTP (MPEG-TS). Lorsque Scte35 est spécifié, encodeur en direct de hello analyse les signaux de SCTE-35 hello flux d’entrée RTP (MPEG-TS).

### <a name="cea-708-closed-captions"></a>Sous-titres CEA-708
Indicateur facultatif qui indique à hello encodeur en temps réel tooignore toutes les données de légendes 708 incorporées dans les vidéo entrant hello. Lorsque l’indicateur de hello a la valeur toofalse (valeur par défaut), les encoder hello détectera et réinsérez les données 708 en flux vidéo de sortie hello.

### <a name="video-stream"></a>Flux vidéo
facultatif. Décrit le flux vidéo entrant de hello. Si ce champ n’est pas spécifié, la valeur par défaut de hello est utilisé. Ce paramètre est autorisé uniquement si hello d’entrée de protocole de diffusion en continu a la valeur tooRTP (MPEG-TS).

#### <a name="index"></a>Index
Index de base zéro qui spécifie quel flux vidéo entrant doit être traité par l’encodeur en temps réel de hello dans hello canal. Ce paramètre s’applique uniquement si le protocole de diffusion en continu de réception est défini sur RTP (MPEG-TS).

La valeur par défaut est zéro. Il est recommandé de toosend dans un flux de transport de programme unique (SPTS). Si le flux d’entrée de hello contient plusieurs programmes, encodeur en direct de hello analyse hello Table de mappage de programme (PMT) dans l’entrée de hello, identifie les entrées hello qui ont un nom de type de flux de vidéo MPEG-2 ou H.264 et les réorganise dans l’ordre de hello spécifié dans hello PMT. index de base zéro Hello est ensuite utilisé toopick des hello énième entrée dans cette organisation.

### <a name="audio-stream"></a>Flux audio
facultatif. Décrit le flux de données audio hello d’entrée. Si ce champ n’est pas spécifié, les valeurs par défaut hello spécifiées s’appliquent. Ce paramètre est autorisé uniquement si hello d’entrée de protocole de diffusion en continu a la valeur tooRTP (MPEG-TS).

#### <a name="index"></a>Index
Il est recommandé de toosend dans un flux de transport de programme unique (SPTS). Si le flux d’entrée de hello contient plusieurs programmes, hello encodeur en direct dans hello canal analyse hello Table de mappage de programme (PMT) dans l’entrée de hello, identifie les entrées hello qui ont un nom de type de flux de MPEG-2 AAC ADTS AC-3 System-A ou AC-3 System-B ou MPEG-2 Private PES ou MPEG-1 Audio ou MPEG-2 Audio et les réorganise dans l’ordre de hello spécifié dans hello PMT. index de base zéro Hello est ensuite utilisé toopick des hello énième entrée dans cette organisation.

#### <a name="language"></a>language
identificateur de langue de hello flux audio, tooISO 639-2, par exemple selon de Hello Sinon, valeur par défaut de la hello est UND (non défini).

Il peut y avoir des flux de données audio too8 jeux spécifiés si hello d’entrée toohello canal est MPEG-2 TS sur RTP. Toutefois, il ne peut y avoir aucune deux entrées avec hello même valeur d’Index.

### <a id="preset"></a>Présélection du système
Spécifie le hello présélection toobe utilisé par l’encodeur en temps réel de hello au sein de ce canal. Actuellement, hello uniquement la valeur est **Default720p** (par défaut).

Notez que si vous avez besoin de paramètres prédéfinis personnalisés, contactez amslived à l’adresse Microsoft.com.

**Default720p** codera vidéo de hello en hello suivant 7 couches.

#### <a name="output-video-stream"></a>Flux vidéo de sortie
| Débit binaire | Largeur | Hauteur | IPS max. | Profil | Nom du flux de sortie |
| --- | --- | --- | --- | --- | --- |
| 3 500 |1 280 |720 |30 |Élevé |Video_1280x720_3500kbps |
| 2 200 |960 |540 |30 |Principal |Video_960x540_2200kbps |
| 1 350 |704 |396 |30 |Principal |Video_704x396_1350kbps |
| 850 |512 |288 |30 |Principal |Video_512x288_850kbps |
| 550 |384 |216 |30 |Principal |Video_384x216_550kbps |
| 350 |340 |192 |30 |Ligne de base |Video_340x192_350kbps |
| 200 |340 |192 |30 |Ligne de base |Video_340x192_200kbps |

#### <a name="output-audio-stream"></a>Flux audio de sortie
Audio est encodé toostereo AAC-LC à 64 Kbits/s, fréquence de 44,1 kHz d’échantillonnage.

## <a name="signaling-advertisements"></a>Signalisation des annonces
Si le paramètre Encodage en temps réel du canal est activé, vous possédez un composant dans votre pipeline qui traite les vidéos et peut les manipuler. Vous pouvez signaler pour hello canal tooinsert plus et/ou des publications dans les flux à débit adaptatif sortant hello. Tablettes sont toujours des images que vous pouvez utiliser toocover des flux d’entrée hello dans certains cas (par exemple pendant une pause publicitaire). Publier des signaux, sont des signaux synchronisés que vous incorporez dans action spéciale hello sortant flux tootell hello lecteur vidéo tootake – tels que de la publication de tooan tooswitch au moment approprié de hello. Consultez ce [blog](https://codesequoia.wordpress.com/2014/02/24/understanding-scte-35/) pour une vue d’ensemble du mécanisme de signalisation hello SCTE-35 utilisé à cet effet. Ci-dessous figure un scénario standard que vous pouvez implémenter dans votre événement en direct.

1. Permettre à vos utilisateurs d’obtenir une image antérieur à l’événement avant le démarrage de l’événement de hello.
2. Permettre à vos utilisateurs d’obtenir une image de post-l’événement après la fin de l’événement de hello.
3. Avoir vos utilisateurs d’obtenir une image de l’événement d’erreur si un problème est survenu lors de l’événement hello (par exemple, panne de courant stade de hello).
4. Envoyer un événement de hello live-publicitaire image toohide flux pendant une pause publicitaire.

Hello Voici les propriétés que vous définissez pour les publications hello. 

### <a name="duration"></a>Duration
Durée Hello, en secondes, de la pause publicitaire de hello. Cela a toobe d’une valeur positive différente de zéro dans publicitaire ordre toostart hello. Quand une pause publicitaire est en cours et la durée de hello toozero ensemble avec hello CueId correspond à pause publicitaire en cours de hello, alors que l’instruction break est annulée.

### <a name="cueid"></a>ID de file d’attente
Un ID Unique pour la pause publicitaire hello, toobe utilisé par l’application en aval tootake les mesures nécessaires. Doit toobe un entier positif. Vous pouvez définir cet valeur tooany aléatoire entier ou utiliser un hello de tootrack ID de file d’attente système en amont. Rendre certaine toonormalize tout entiers de toopositive ID avant l’envoi par hello API.

### <a name="show-slate"></a>Afficher l’ardoise
facultatif. Signaux hello encodeur en temps réel tooswitch toohello [par défaut ardoise](media-services-manage-live-encoder-enabled-channels.md#default_slate) image pendant une pause publicitaire et masquer le flux vidéo entrant de hello. Le son est également désactivé pendant l’affichage de l’ardoise. La valeur par défaut est **false**. 

image Hello utilisée sera hello celle spécifiée via asset d’ardoise par défaut hello propriété Id lors de la création du canal hello hello. séquence de Hello sera étirée toofit la taille d’image de l’affichage hello. 

## <a name="insert-slate--images"></a>Insérer des images d’ardoise
encodeur en direct de Hello dans hello canal peut être signalé tooswitch tooa ardoise image. Il peut également être signalé tooend une ardoise. 

encodeur en direct de Hello peut être configuré tooswitch tooa ardoise image et masquer hello signal vidéo entrant dans certaines situations, par exemple, pendant une coupure publicitaire. Si une telle ardoise n’est pas configurée, la vidéo d’entrée n’est pas masquée pendant cette annonce publicitaire.

### <a name="duration"></a>Duration
Durée Hello de séquence de hello en secondes. Cela a toobe d’une valeur positive différente de zéro dans la séquence de commande toostart hello. Si une ardoise est en cours d’affichage et que la durée zéro est spécifiée, cette ardoise en cours va se terminer.

### <a name="insert-slate-on-ad-marker"></a>Insérer une ardoise dans le marqueur de publicité
Lorsque le jeu tootrue, ce paramètre configure hello encodeur en temps réel tooinsert une image d’ardoise pendant une coupure publicitaire. valeur par défaut de Hello est true. 

### <a id="default_slate"></a>ID de ressource d'ardoise par défaut

facultatif. Spécifie les hello Id d’élément multimédia de hello Services multimédia qui contient l’image de hello ardoise. La valeur par défaut est Null. 


>[!NOTE] 
>Avant de créer le canal de hello, hello image d’ardoise par hello suivant contraintes doit être téléchargé en tant qu’une ressource dédiée (aucun autre fichier ne doit être dans cet élément multimédia). Cette image est utilisée uniquement lorsque encodeur en direct de hello consiste à insérer une ardoise en raison de la coupure publicitaire tooan ou a été explicitement signalé tooinsert une ardoise. encodeur en direct de Hello peut également passer en mode d’ardoise pendant certaines conditions d’erreur – par exemple si le signal d’entrée de hello est perdue. Il n’a actuellement aucun toouse option une image personnalisée lors de l’encodeur en temps réel de hello passe à un état « perdu du signal d’entrée ». Vous pouvez voter pour que cette fonctionnalité [ici](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/10190457-define-custom-slate-image-on-a-live-encoder-channel).


* Résolution maximale de 1920 x 1080
* Taille maximale de 3 Mo.
* nom de fichier Hello doit avoir une extension *.jpg.
* image de Hello doit être téléchargé dans un élément multimédia en tant que hello Qu'assetfile uniquement dans cet élément multimédia et cet AssetFile doivent être marqué comme fichier principal de hello. Hello actif ne peut pas être chiffré de stockage.

Si hello **par défaut tablettes Id d’élément multimédia** n’est pas spécifié, et **insertion d’ardoise sur un marqueur publicitaire** est défini trop**true**, une image d’Azure Media Services par défaut sera hello toohide utilisé d’entrée flux vidéo. Le son est également désactivé pendant l’affichage de l’ardoise. 

## <a name="channels-programs"></a>Programmes du canal
Un canal est associé à des programmes qui vous permettent de la publication toocontrol hello et stockage des segments dans un flux en direct. Les canaux gèrent des programmes. Hello relation de canal et le programme est très similaire tootraditional média, où un canal possède un flux constant de contenu et un programme est événements étendue toosome a expiré sur le canal.

Vous pouvez spécifier le nombre de hello d’heures que vous voulez tooretain hello enregistrée contenu pour le programme de hello en définissant un hello **fenêtre d’Archive** longueur. Cette valeur peut être définie à partir d’un minimum de 5 minutes tooa 25 heures maximum. Longueur de fenêtre d’archive détermine également hello durée maximale pendant laquelle les clients peuvent effectuer des recherches dans le temps à partir de la position de diffusion en continu hello actuel. Programmes peuvent s’exécuter sur la durée spécifiée hello, mais le contenu qui se trouve derrière la longueur de la fenêtre hello est ignoré en permanence. La valeur de cette propriété détermine également la durée pendant laquelle hello client manifestes peuvent atteindre.

Chaque programme est associé à un élément multimédia qui stocke le contenu de diffusion en continu de hello. Un élément multimédia est le conteneur d’objets blob de blocs tooa mappé dans le compte de stockage Azure hello et fichiers hello asset de hello sont stockés en tant qu’objets BLOB dans le conteneur. programme de hello toopublish afin que vos clients puissent afficher les flux hello vous devez créer un localisateur OnDemand pour hello associés actif. Ce localisateur activera toobuild une URL de diffusion en continu que vous pouvez fournir tooyour clients.

Un canal prend en charge jusqu'à toothree qui s’exécutent simultanément des programmes, vous pouvez créer plusieurs archives de hello même flux entrant. Cela vous permet de toopublish et archivage de différentes parties d’un événement en fonction des besoins. Par exemple, vos exigences d’entreprise est tooarchive 6 heures d’un programme, mais toobroadcast uniquement les 10 dernières minutes. tooaccomplish, vous devez toocreate deux des programmes qui s’exécutent simultanément. Un programme a la valeur tooarchive d’événement de hello les 6 heures, mais les programme hello ne sont pas publié. Hello autre programme est ensemble tooarchive pendant 10 minutes et ce programme est publié.

Vous ne devez pas réutiliser de programmes existants pour de nouveaux événements. Au lieu de cela, créez et démarrez un nouveau programme pour chaque événement, comme décrit dans la section de programmation d’Applications de diffusion en continu Live hello.

Démarrer le programme de hello lorsque vous êtes prêt toostart diffusion et l’archivage. Arrêter le programme de hello chaque fois que vous souhaitez toostop de diffusion en continu et l’archivage des événements de hello. 

contenu de toodelete archivé, arrêter et supprimer hello programme et supprimez actif associé de hello. Un élément multimédia ne peut pas être supprimé s’il est utilisé par un programme ; programme de Hello doit d’abord être supprimée. 

Même après l’arrêt et suppression du programme de hello, hello les utilisateurs serait en mesure de toostream votre contenu archivé comme une vidéo à la demande, pour tant que vous ne supprimez pas l’élément multimédia de hello.

Si vous souhaitez hello tooretain archivé le contenu, mais n’est pas le disponible pour la diffusion en continu, supprimez hello localisateur de diffusion en continu.

## <a name="getting-a-thumbnail-preview-of-a-live-feed"></a>Obtention d’une image miniature d’un flux en direct
Lors de l’encodage dynamique est activée, vous pouvez désormais obtenir un aperçu du flux live de hello qu’il atteint hello canal. Cela peut être un toocheck outil très utile si votre flux dynamique est atteint réellement le canal de hello. 

## <a id="states"></a>Les États des canaux et comment les États mappent toohello en mode de facturation
état actuel de Hello d’un canal. Les valeurs possibles incluent :

* **Arrêté**. Il s’agit état initial de hello Hello canal après sa création. Dans cet état, les propriétés de canal hello peuvent être mis à jour, mais de diffusion en continu n’est pas autorisée.
* **Démarrage en cours**. Hello canal est en cours de démarrage. Aucune mise à jour ni aucun streaming ne sont autorisés durant cet état. Si une erreur se produit, hello canal retourne toohello état arrêté.
* **Exécution en cours**. Hello canal est capable de traiter des flux live.
* **En cours d’arrêt**. Hello canal est en cours d’arrêt. Aucune mise à jour ni aucun streaming ne sont autorisés durant cet état.
* **Suppression en cours**. Hello canal est en cours de suppression. Aucune mise à jour ni aucun streaming ne sont autorisés durant cet état.

Hello tableau suivant montre comment canal indique le mode de facturation toohello mappage. 

| État du canal | Indicateurs de l’interface utilisateur du portail | Facturation ? |
| --- | --- | --- |
| Démarrage en cours |Démarrage en cours |Aucun (état transitoire) |
| Exécution en cours |Prêt (pas de programmes en cours d’exécution)<br/>ou<br/>Streaming (au moins un programme en cours d’exécution) |OUI |
| En cours d’arrêt |En cours d’arrêt |Aucun (état transitoire) |
| Arrêté |Arrêté |Non |

> [!NOTE]
> Actuellement, moyenne de démarrage de canal hello est d’environ 2 minutes, mais dans certains cas peut être too20 + minutes. Les réinitialisations de canal peuvent prendre jusqu'à too5 minutes.
> 
> 

## <a id="Considerations"></a>Considérations
* Lorsqu’un canal de **Standard** type d’encodage rencontre une perte d’alimentation de la source/contribution d’entrée, il compense en remplaçant hello source audio/vidéo avec une séquence d’erreur et la latence. Hello canal continue tooemit une ardoise jusqu'à ce que l’entrée de hello/contribution flux reprend. Nous vous recommandons de ne pas laisser un canal direct dans cet état pendant plus de 2 heures. Au-delà de ce point, comportement hello Hello canal lors de la reconnexion d’entrée n’est pas garanti, n’est pas son comportement en réponse tooa commande de réinitialisation. Vous avez toostop hello canal, supprimez-le et créez-en un nouveau.
* Vous ne pouvez modifier le protocole d’entrée de hello lors hello canal ou ses programmes associés sont en cours d’exécution. Si vous avez besoin d’autres protocoles, vous devez créer des canaux distincts pour chaque protocole d’entrée.
* Chaque fois que vous reconfigurez encodeur en direct de hello, appelez hello **réinitialiser** méthode sur le canal de hello. Avant de réinitialiser le canal de hello, vous disposez de programme de hello toostop. Après avoir réinitialisé le canal de hello, redémarrez le programme de hello.
* Un canal peut être arrêté seulement quand il est en cours d’exécution hello, et tous les programmes sur le canal de hello ont été arrêtés.
* Par défaut, vous pouvez uniquement ajouter 5 canaux tooyour compte Media Services. Il s’agit d’un quota conditionnel sur tous les nouveaux comptes. Pour plus d’informations, voir [Quotas et limitations](media-services-quotas-and-limitations.md).
* Vous ne pouvez modifier le protocole d’entrée de hello lors hello canal ou ses programmes associés sont en cours d’exécution. Si vous avez besoin d’autres protocoles, vous devez créer des canaux distincts pour chaque protocole d’entrée.
* Vous êtes facturé uniquement lorsque votre canal est Bonjour **en cours d’exécution** état. Pour plus d’informations, consultez trop[cela](media-services-manage-live-encoder-enabled-channels.md#states) section.
* Actuellement, hello maximum recommandé de durée d’un événement en direct est de 8 heures. Si vous avez besoin d’un canal de toorun pour de longues périodes, contactez amslived Microsoft.com.
* Assurez-vous que toohave hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez contenu toostream Bonjour **en cours d’exécution** état.
* Seul RTP est pris en charge pour la saisie multilingue lors de la saisie de pistes multilingues et l'encodage en temps réel. Vous pouvez définir des flux de données audio too8 à l’aide de MPEG-2 TS sur RTP. La réception de plusieurs pistes audio avec RTMP ou Smooth Streaming n'est actuellement pas prise en charge. Lors de l’exécution avec l’encodage live [local live encode](media-services-live-streaming-with-onprem-encoders.md), il en existe aucune limitation de ce type, car tout ce qui est envoyé tooAMS passe par un canal sans traitement supplémentaire.
* utilise de présélection encodage Hello hello la notion de « max cadence » de 30 i/s. Par conséquent, si hello entrée est de 60fps / 59.97i, les cadres d’entrée hello sont supprimés/désérialiser-interlaced too30/29,97 i/s. Si l’entrée hello est i/s 50/50i, les trames d’entrée hello sont i/s supprimés/désérialiser-interlaced too25. Si l’entrée de hello est 25 i/s, sortie reste à 25 i/s.
* N’oubliez pas les canaux de votre tooSTOP lorsqu’il est terminé. Dans le cas contraire, la facturation continue.

## <a name="known-issues"></a>Problèmes connus
* Temps de démarrage du canal a été améliorée tooan moyenne de 2 minutes, mais dans certains cas d’augmentation de la demande peut toujours être too20 + minutes.
* La prise en charge RTP est adaptée aux diffuseurs professionnels. Passez en revue les notes hello sur RTP dans [cela](https://azure.microsoft.com/blog/2015/04/13/an-introduction-to-live-encoding-with-azure-media-services/) blog.
* Images de la séquence doivent être conforme toorestrictions décrites [ici](media-services-manage-live-encoder-enabled-channels.md#default_slate). Si vous essayez de créer un canal avec une erreur de séquence par défaut qui est supérieure à 1920 x 1080, hello requête finit par out.
* Une fois encore... n’oubliez pas tooSTOP votre canaux lorsque vous avez terminé de diffusion en continu. Dans le cas contraire, la facturation continue.

## <a name="next-step"></a>Étape suivante
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Rubriques connexes
[Diffusion d’événements en direct en continu avec Azure Media Services](media-services-overview.md)

[Créer des canaux qui effectue un encodage dynamique d’un flux de vitesse de transmission unique à débit binaire tooadaptive avec le portail](media-services-portal-creating-live-encoder-enabled-channel.md)

[Créer des canaux qui effectue un encodage dynamique d’un flux de vitesse de transmission unique à débit binaire tooadaptive avec le Kit de développement .NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)

[Gérer des canaux avec l’API REST](https://docs.microsoft.com/rest/api/media/operations/channel)
 
[Concepts Azure Media Services](media-services-concepts.md)

[Spécification d’ingestion en direct au format MP4 fragmenté Azure Media Services](media-services-fmp4-live-ingest-overview.md)

[live-overview]: ./media/media-services-manage-live-encoder-enabled-channels/media-services-live-streaming-new.png

