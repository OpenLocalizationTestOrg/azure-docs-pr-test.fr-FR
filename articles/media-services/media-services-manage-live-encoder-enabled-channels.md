---
title: "Comment effectuer une diffusion de vidéo en flux continu à l’aide d’Azure Media Services pour créer des flux à vitesses de transmission multiples | Microsoft Docs"
description: "Cette rubrique décrit comment configurer un canal qui reçoit un flux dynamique à débit binaire unique à partir d’un encodeur local, puis effectue un encodage en temps réel en flux à débit binaire adaptatif avec Media Services. Le flux peut ensuite être distribué aux applications de lecture clientes via un ou plusieurs points de terminaison de streaming à l’aide d’un des protocoles de diffusion en continu adaptatifs suivants : HLS, Smooth Stream, MPEG DASH."
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
ms.openlocfilehash: d5f76d532b236e67a4e69eb820e2cfc3033a80c6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="live-streaming-using-azure-media-services-to-create-multi-bitrate-streams"></a>Comment effectuer une diffusion de vidéo en flux continu à l’aide d’Azure Media Services pour créer des flux à vitesses de transmission multiples.
## <a name="overview"></a>Vue d'ensemble
Dans Azure Media Services (AMS), un **canal** représente un pipeline de traitement du contenu vidéo en flux continu. Un **canal** reçoit des flux d’entrée live de l’une des deux manières suivantes :

* Un encodeur dynamique envoie un flux à vitesse de transmission unique vers le canal activé pour effectuer un encodage en direct avec Media Services dans l’un des formats suivants : RTP (MPEG-TS), RTMP ou Smooth Streaming (MP4 fragmenté). Le canal procède ensuite à l’encodage en temps réel du flux à débit unique entrant en flux vidéo multidébit (adaptatif). Lorsqu’il y est invité, Media Services fournit le flux aux clients.
* Un encodeur live local envoie au canal un paquet **RTMP** ou **Smooth Streaming** (MP4 fragmenté) à débit binaire multiple qui n’est pas activé pour effectuer un encodage live avec AMS. Les flux reçus transitent par les **canaux**sans traitement supplémentaire. Cette méthode est appelée **pass-through**. Vous pouvez utiliser les encodeurs en direct suivants qui produisent un flux Smooth Streaming multidébit : MediaExcel, Ateme, Imagine Communications, Envivio, Cisco et Elemental. Les encodeurs en direct suivants produisent un flux au format RTMP : Adobe Flash Media Live Encoder (FMLE), Telestream Wirecast, Haivision, Teradek et Tricaster.  Un encodeur live peut également envoyer un flux à débit binaire unique vers un canal qui n’est pas activé pour le Live Encoding, mais ce n’est pas recommandé. Lorsqu’il y est invité, Media Services fournit le flux aux clients.
  
  > [!NOTE]
  > L’utilisation d’une méthode pass-through est le moyen le plus économique de diffuser une vidéo en flux continu.
  > 
  > 

À compter de la version de Media Services 2.10, lorsque vous créez un canal, vous pouvez spécifier la façon dont vous souhaitez qu’il reçoive le flux d’entrée. Vous pouvez également indiquer si vous souhaitez ou non que le canal effectue un encodage en temps réel de votre flux. Deux options s'offrent à vous :

* **Aucun** : indiquez cette valeur si vous envisagez d’utiliser un encodeur live local qui produira des flux multidébits (un flux pass-through). Le cas échéant, le flux entrant est transmis à la sortie sans encodage. Il s’agit du comportement d’un canal avant la version 2.10.  Pour plus d’informations sur l’utilisation des canaux de ce type, consultez [Vidéo en flux continu avec des encodeurs locaux qui créent des flux à vitesses de transmission multiples](media-services-live-streaming-with-onprem-encoders.md).
* **Standard** : choisissez cette valeur si vous envisagez d’utiliser Media Services pour encoder votre flux live à débit binaire unique en flux à débit binaire multiple. N'oubliez pas qu'il existe un impact sur la facturation pour le codage en direct et que laisser un canal d'encodage en temps réel dans l'état « Actif » occasionne des frais de facturation.  Il est recommandé d'arrêter immédiatement vos canaux en cours d'exécution une fois votre événement de diffusion en continu en temps réel terminé pour éviter des frais horaires supplémentaires.

> [!NOTE]
> Cette rubrique décrit les attributs des canaux qui sont activés pour effectuer un encodage en temps réel (type d’encodage**standard** ). Pour obtenir des informations sur l’utilisation des canaux qui ne sont pas activés pour effectuer l’encodage live, consultez [Vidéo en flux continu avec des encodeurs locaux qui créent des flux à vitesses de transmission multiples](media-services-live-streaming-with-onprem-encoders.md).
> 
> Assurez-vous d’examiner la section [Considérations](media-services-manage-live-encoder-enabled-channels.md#Considerations) .
> 
> 

## <a name="billing-implications"></a>Implications de facturation
La facturation d'un canal d'encodage en temps réel commence dès que son état passe à « En cours d'exécution » via l'API.   Vous pouvez également afficher l’état dans le portail Azure ou dans l’outil Azure Media Services Explorer (http://aka.ms/amse).

Le tableau suivant montre comment les états du canal sont mappés aux états de facturation dans l’API et le portail Azure. Notez que les états sont légèrement différents entre l'API et le portail. Dès qu’un canal est dans l’état « En cours d’exécution » via l’API, ou dans l’état « Prêt » ou « Diffusion en continu » dans le portail Azure, la facturation est active.
Pour arrêter la facturation, vous devez arrêter le canal via l’API ou dans le portail Azure.
Vous êtes responsable de l'arrêt de vos canaux lorsque vous avez terminé d'utiliser le canal d'encodage en temps réel.  Ne pas arrêter un canal d'encodage provoque la facturation continue.

### <a id="states"></a>États du canal et mappage au mode de facturation
État actuel d’un canal. Les valeurs possibles incluent :

* **Arrêté**. Ceci est l'état initial du canal après sa création (sauf si le démarrage automatique a été sélectionné dans le portail). Aucune facturation ne survient dans cet état. Dans cet état, les propriétés du canal peuvent être mises à jour, mais la diffusion en continu n’est pas autorisée.
* **Démarrage en cours**. Le canal est en cours de démarrage. Aucune facturation ne survient dans cet état. Aucune mise à jour ou diffusion en continu n’est autorisée durant cet état. Si une erreur se produit, le canal retourne à l’état Arrêté.
* **Exécution en cours**. Le canal est capable de traiter des flux dynamiques. Il facture désormais l'utilisation. Vous devez arrêter le canal pour empêcher toute facturation supplémentaire. 
* **En cours d’arrêt**. Le canal est en cours d’arrêt. Aucune facturation ne survient dans cet état de transition. Aucune mise à jour ou diffusion en continu n’est autorisée durant cet état.
* **Suppression en cours**. Le canal est en cours de suppression. Aucune facturation ne survient dans cet état de transition. Aucune mise à jour ou diffusion en continu n’est autorisée durant cet état.

Le tableau suivant montre comment les états du canal sont mappés au mode de facturation. 

| État du canal | Indicateurs de l’interface utilisateur du portail | Existe-t-il une facturation ? |
| --- | --- | --- |
| Démarrage en cours |Démarrage en cours |Aucun (état transitoire) |
| Exécution en cours |Prêt (pas de programmes en cours d’exécution)<br/>ou<br/>Diffusion en continu (au moins un programme en cours d'exécution) |OUI |
| En cours d’arrêt |En cours d’arrêt |Aucun (état transitoire) |
| Arrêté |Arrêté |Non |

### <a name="automatic-shut-off-for-unused-channels"></a>Fermeture automatique des canaux inutilisés
Depuis le 25 janvier 2016, Media Services a déployé une mise à jour qui ferme automatiquement un canal (avec encodage en temps réel activé) s’il reste non utilisé pendant une longue période. Cela s'applique aux canaux qui n’ont aucun programme actif et qui ont été laissés à l’état d’exécution sans un flux de contribution d’entrée pendant une période prolongée.

Le seuil nominal de la période inutilisée est de 12 heures, mais il est susceptible de changer.

## <a name="live-encoding-workflow"></a>Flux de travail d'encodage en temps réel
Le diagramme suivant représente un flux de travail de diffusion en continu dynamique où un canal reçoit un flux à débit binaire unique dans l’un des protocoles suivants : RTMP, Smooth Streaming ou RTP (MPEG-TS). Il encode ensuite le flux dans un flux à débit binaire multiple. 

![Flux de travail live][live-overview]

## <a id="scenario"></a>Scénario courant de diffusion dynamique en continu
Ci-après figurent les étapes générales impliquées dans la création d’applications courantes de diffusion en continu dynamique.

> [!NOTE]
> Actuellement, la durée maximale recommandée d’un événement en direct est de 8 heures. Contactez amslived à Microsoft.com si vous avez besoin d’exécuter un canal pour de longues périodes. N’oubliez pas qu’il existe un impact sur la facturation pour l’encodage en temps réel et que laisser un canal d’encodage en temps réel dans l’état « Actif » occasionne des frais de facturation horaires.  Il est recommandé d'arrêter immédiatement vos canaux en cours d'exécution une fois votre événement de diffusion en continu en temps réel terminé pour éviter des frais horaires supplémentaires. 
> 
> 

1. Connectez une caméra vidéo à un ordinateur. Lancez et configurez un encodeur dynamique local capable de générer un flux à vitesse binaire **unique** dans l’un des protocoles suivants : RTMP, Smooth Streaming ou RTP (MPEG-TS). 
   
    Cette étape peut également être effectuée après la création du canal.
2. Créez et démarrez un canal. 
3. Récupérez l’URL de réception du canal. 
   
    L’URL de réception est utilisée par l’encodeur dynamique pour envoyer le flux au canal.
4. Récupérez l’URL d’aperçu du canal. 
   
    Utilisez cette URL pour vérifier que votre canal reçoit correctement le flux dynamique.
5. Créez un programme. 
   
    Lors de l’utilisation du portail Azure, la création d’un programme crée également un élément multimédia. 
   
    Lors de l’utilisation du Kit SDK .NET ou de REST, vous devez créer une ressource et préciser son utilisation lors de la création d’un programme. 
6. Publiez la ressource associée au programme.   
   
    >[!NOTE]
    >Une fois votre compte AMS créé, un point de terminaison de streaming **par défaut** est ajouté à votre compte à l’état **Arrêté**. Le point de terminaison à partir duquel vous souhaitez diffuser du contenu doit se trouver dans l’état **En cours d’exécution**. 
    
7. Démarrez le programme dès que vous êtes prêt à lancer le streaming et l’archivage.
8. Un signal peut éventuellement être envoyé à l’encodeur dynamique pour qu’il démarre une publicité. La publicité est insérée dans le flux de sortie.
9. Arrêtez le programme chaque fois que vous voulez arrêter le streaming et l’archivage de l’événement.
10. Supprimez le programme (et éventuellement la ressource).   

> [!NOTE]
> Il est très important de ne pas oublier d'arrêter un canal d'encodage en temps réel. N'oubliez pas qu'il existe un impact sur la facturation horaire pour l'encodage en temps réel et que laisser un canal d'encodage en temps réel dans l'état « Actif » occasionne des frais de facturation.  Il est recommandé d'arrêter immédiatement vos canaux en cours d'exécution une fois votre événement de diffusion en continu en temps réel terminé pour éviter des frais horaires supplémentaires. 
> 
> 

## <a id="channel"></a>Configurations de l’entrée (réception) du canal
### <a id="Ingest_Protocols"></a>Protocole de diffusion en continu de réception
Si le **Type d’encodeur** est défini sur **Standard**, les options valides sont les suivantes :

* **RTP** (MPEG-TS) : flux de transport MPEG-2 via RTP.  
* **RTMP**
* **MP4 fragmenté** (Smooth Streaming) à débit binaire unique

#### <a name="rtp-mpeg-ts---mpeg-2-transport-stream-over-rtp"></a>RTP (MPEG-TS) : flux de transport MPEG-2 via RTP.
Cas d’utilisation classique : 

Les diffuseurs professionnels utilisent généralement des encodeurs dynamiques locaux haut de gamme des fournisseurs comme Elemental Technologies, Ericsson, Ateme, Imagine ou Envivio pour envoyer un flux. Ils sont souvent utilisés conjointement avec un service informatique et des réseaux privés.

Considérations :

* L’utilisation d’une entrée SPTS (Single Program Transport Stream) est vivement recommandée. 
* Vous pouvez utiliser en entrée jusqu'à 8 flux audio à l'aide de MPEG-2 TS via RTP. 
* Le flux vidéo doit avoir un débit binaire moyen inférieur à 15 Mbits/s.
* La somme des débits binaires moyens des flux audio doit être inférieure à 1 Mbits/s.
* Voici les codecs pris en charge :
  
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

* Le flux entrant ne peut pas contenir de vidéo à débit binaire multiple
* Le flux vidéo doit avoir un débit binaire moyen inférieur à 15 Mbits/s.
* Le flux audio doit avoir un débit binaire moyen inférieur à 1 Mbits/s.
* Voici les codecs pris en charge :
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

Utilisez les encodeurs dynamiques locaux des fournisseurs que sont Elemental Technologies, Ericsson, Ateme, Envivio pour envoyer le flux d’entrée via Internet à un centre de données Azure à proximité.

Considérations :

Identique au flux [RTMP à débit binaire unique](media-services-manage-live-encoder-enabled-channels.md#single_bitrate_RTMP).

#### <a name="other-considerations"></a>Autres considérations
* Vous ne pouvez pas modifier le protocole d’entrée pendant l’exécution du canal ou de ses programmes associés. Si vous avez besoin d’autres protocoles, vous devez créer des canaux distincts pour chaque protocole d’entrée.
* La résolution maximale pour le flux vidéo entrant est définie sur 1920x1080. Si le flux vidéo est entrelacé, elle est définie au plus sur 60 champs par seconde. S’il est progressif, elle est définie sur 30 images/seconde.

### <a name="ingest-urls-endpoints"></a>URL (points de terminaison) de réception
Un canal fournit un point de terminaison d’entrée (URL de réception) que vous spécifiez dans l’encodeur dynamique pour que ce dernier puisse envoyer les flux vers vos canaux.

Vous pouvez obtenir les URL de réception dès que vous avez créé un canal. Pour les obtenir, il n’est pas nécessaire que le canal soit à l’état **En cours d’exécution** . Lorsque vous êtes prêt à commencer l’envoi de données dans le canal, ce dernier doit être à l’état **En cours d’exécution** . Une fois que le canal commence à recevoir les données, vous pouvez prévisualiser votre flux via l’URL d’aperçu.

Vous avez la possibilité de recevoir un flux dynamique au format MP4 fragmenté (Smooth Streaming) via une connexion SSL. Pour assurer la réception via SSL, veillez à mettre à jour l’URL de réception pour HTTPS. Notez que, actuellement, AMS ne prend pas en charge SSL avec les domaines personnalisés.  

### <a name="allowed-ip-addresses"></a>Adresses IP autorisées
Vous pouvez définir les adresses IP autorisées à publier du contenu vidéo sur ce canal. Les adresses IP autorisées peuvent être spécifiées en tant qu’adresses IP uniques (par exemple, '10.0.0.1'), une plage d’adresses IP utilisant une adresse IP et un masque de sous-réseau CIDR (par exemple, 10.0.0.1/22), ou une plage d’adresses IP utilisant une adresse IP et un masque de sous-réseau décimal séparé par des points (par exemple, '10.0.0.1(255.255.252.0)').

Si aucune adresse IP n’est spécifiée et qu’il n’existe pas de définition de règle, alors aucune adresse IP n’est autorisée. Pour autoriser toutes les adresses IP, créez une règle et définissez la valeur 0.0.0.0/0.

## <a name="channel-preview"></a>Aperçu du canal
### <a name="preview-urls"></a>URL d’aperçu
Les canaux fournissent un point de terminaison d’aperçu (URL d’aperçu) permettant de prévisualiser et de valider le flux avant de lui appliquer un traitement supplémentaire et de le distribuer.

Vous pouvez obtenir l’URL d’aperçu lors de la création du canal. Pour obtenir l’URL, il n’est pas nécessaire que le canal soit à l’état **En cours d’exécution** .

Une fois que le canal commence à recevoir les données, vous pouvez prévisualiser votre flux.

> [!NOTE]
> Actuellement, le flux d'aperçu ne peut être distribué qu'au format MP4 fragmenté (Smooth Streaming), quel que soit le type d'entrée spécifié. Vous pouvez utiliser le lecteur [http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor) pour tester la diffusion au format Smooth Streaming. Vous pouvez également utiliser un lecteur hébergé dans le portail Azure pour afficher votre flux.
> 
> 

### <a name="allowed-ip-addresses"></a>Adresses IP autorisées
Vous pouvez définir les adresses IP autorisées à se connecter au point de terminaison d’aperçu. Si aucune adresse IP n’est spécifiée, alors toutes les adresses IP seront autorisées. Les adresses IP autorisées peuvent être spécifiées en tant qu’adresses IP uniques (par exemple, 10.0.0.1), une plage d’adresses IP utilisant une adresse IP et un masque de sous-réseau CIDR (par exemple, 10.0.0.1/22), ou une plage d’adresses IP utilisant une adresse IP et un masque de sous-réseau décimal séparé par des points (par exemple, 10.0.0.1[255.255.252.0]).

## <a name="live-encoding-settings"></a>Paramètres d’encodage en temps réel
Cette section décrit comment les paramètres de l’encodeur dynamique dans le canal peuvent être ajustés, lorsque le paramètre **Type d’encodage** d’un canal est défini sur **Standard**.

> [!NOTE]
> Seul RTP est pris en charge pour la saisie multilingue lors de la saisie de pistes multilingues et l'encodage en temps réel. Vous pouvez définir jusqu'à 8 flux audio en entrée à l'aide de MPEG-2 TS via RTP. La réception de plusieurs pistes audio avec RTMP ou Smooth Streaming n'est actuellement pas prise en charge. Il n’existe aucune limitation en cas d’encodage live avec des [encodeurs live locaux](media-services-live-streaming-with-onprem-encoders.md), car tout le contenu envoyé au système AMS passe par un canal sans traitement supplémentaire.
> 
> 

### <a name="ad-marker-source"></a>Source de marqueur de publicité
Vous pouvez spécifier la source des signaux des marqueurs de publicité. La valeur par défaut est **Api**, qui indique que l’encodeur dynamique dans le canal doit écouter une **API de marqueur de publicité** asynchrone.

L’autre option valide est **Scte35** (autorisée uniquement si le protocole de diffusion en continu de réception est défini sur RTP (MPEG-TS). Si l’option Scte35 est spécifiée, l’encodeur dynamique analyse les signaux SCTE-35 du flux d’entrée RTP (MPEG-TS).

### <a name="cea-708-closed-captions"></a>Sous-titres CEA-708
Indicateur facultatif qui spécifie à l’encodeur dynamique d’ignorer les données des sous-titres CEA-708 intégrées à la vidéo entrante. Lorsque l’indicateur est défini sur false (par défaut), l’encodeur détecte et réinsère les données CEA-708 dans les flux vidéo de sortie.

### <a name="video-stream"></a>Flux vidéo
facultatif. Décrit le flux vidéo d’entrée. Si ce champ n’est pas spécifié, la valeur par défaut est utilisée. Ce paramètre est autorisé uniquement si le protocole de diffusion en continu d’entrée est défini sur RTP (MPEG-TS).

#### <a name="index"></a>Index
Index de base zéro qui précise le flux vidéo d’entrée qui doit être traité par l’encodeur dynamique dans le canal. Ce paramètre s’applique uniquement si le protocole de diffusion en continu de réception est défini sur RTP (MPEG-TS).

La valeur par défaut est zéro. L’envoi dans un flux SPTS est recommandé. Si le flux d’entrée contient plusieurs programmes, l’encodeur dynamique analyse la table de mappage de programmes (PMT) dans l’entrée, identifie les entrées dont le nom de type de flux est Vidéo MPEG-2 ou H.264, puis les réorganise en suivant l’ordre spécifié dans la table PMT. L’index de base zéro permet ensuite de choisir la nième entrée dans cette disposition.

### <a name="audio-stream"></a>Flux audio
facultatif. Décrit les flux audio d’entrée. Si ce champ n’est pas spécifié, les valeurs par défaut spécifiées s’appliquent. Ce paramètre est autorisé uniquement si le protocole de diffusion en continu d’entrée est défini sur RTP (MPEG-TS).

#### <a name="index"></a>Index
L’envoi dans un flux SPTS est recommandé. Si le flux d’entrée contient plusieurs programmes, l’encodeur dynamique au sein du canal analyse la table de mappage de programmes (PMT) dans l’entrée, identifie les entrées dont le nom de type de flux est Audio MPEG-2 AAC ADTS, AC-3 System-A, AC-3 System-B, MPEG-2 Private PES, MPEG-1 ou MPEG-2, puis les réorganise en suivant l’ordre spécifié dans la table PMT. L’index de base zéro permet ensuite de choisir la nième entrée dans cette disposition.

#### <a name="language"></a>Langage
Identificateur de langue du flux audio, conformément à la norme ISO 639-2, par exemple ENG. En son absence, la valeur par défaut est UND (non définie).

Jusqu’à 8 jeux de flux audio peuvent être spécifiés si l’entrée du canal est définie sur MPEG-2 TS via RTP. Toutefois, deux entrées ne peuvent pas posséder la même valeur d’index.

### <a id="preset"></a>Présélection du système
Spécifie la présélection à utiliser par l’encodeur dynamique dans ce canal. Actuellement, la seule valeur autorisée est **Default720p** (par défaut).

Notez que si vous avez besoin de paramètres prédéfinis personnalisés, contactez amslived à l’adresse Microsoft.com.

**Default720p** encode la vidéo dans les 7 couches suivantes.

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
Le flux audio est encodé au format stéréo AAC-LC à 64 Kbits/s, avec un taux d’échantillonnage de 44,1 kHz.

## <a name="signaling-advertisements"></a>Signalisation des annonces
Si le paramètre Encodage en temps réel du canal est activé, vous possédez un composant dans votre pipeline qui traite les vidéos et peut les manipuler. Vous pouvez indiquer au canal d’insérer des ardoises et/ou des annonces dans le flux à débit binaire adaptatif sortant. Les ardoises sont des images fixes que vous pouvez utiliser pour couvrir le flux d’entrée dynamique dans certains cas (par exemple pendant une pause publicitaire). Les signaux publicitaires sont des signaux synchronisés que vous intégrez au flux sortant pour indiquer au lecteur vidéo d’effectuer une action spéciale, par exemple de basculer vers une annonce au moment approprié. Consultez ce [blog](https://codesequoia.wordpress.com/2014/02/24/understanding-scte-35/) pour obtenir une vue d’ensemble du mécanisme de signalisation SCTE-35 utilisé à cet effet. Ci-dessous figure un scénario standard que vous pouvez implémenter dans votre événement en direct.

1. Avant le début de l’événement, faites que vos observateurs obtiennent une image ANTÉRIEURE À L’ÉVÉNEMENT
2. À l’issue de l’événement, faites que vos observateurs obtiennent une image POST-ÉVÉNEMENT.
3. Faites que vos observateurs obtiennent une image ÉVÉNEMENT AVEC ERREUR si un problème se produit au cours de l’événement (par exemple, une panne de courant dans un stade).
4. Envoyez une image PAUSE PUBLICITAIRE pour masquer le flux d’événements en direct pendant une pause publicitaire.

Ci-après figurent les propriétés que vous pouvez définir pour la signalisation des annonces : 

### <a name="duration"></a>Durée
Durée (en secondes) de la pause publicitaire. Pour que la pause publicitaire commence, ce doit être une valeur positive différente de zéro. Si une pause publicitaire est en cours et que la durée est définie sur zéro avec la propriété ID de file d’attente correspondant à la pause publicitaire en cours, alors cette pause est annulée.

### <a name="cueid"></a>ID de file d’attente
ID unique de la pause publicitaire à utiliser par une application en aval pour prendre les actions appropriées. Ce doit être un entier positif. Vous pouvez définir cette valeur sur un entier positif aléatoire quelconque ou utiliser un système en amont pour suivre les ID de file d'attente. Assurez-vous de normaliser les ID en entiers positifs avant de procéder à la soumission via l’API.

### <a name="show-slate"></a>Afficher l’ardoise
facultatif. Signale à l’encodeur en direct de basculer vers l’image de l’ [ardoise par défaut](media-services-manage-live-encoder-enabled-channels.md#default_slate) pendant une pause publicitaire et de masquer le flux vidéo entrant. Le son est également désactivé pendant l’affichage de l’ardoise. La valeur par défaut est **false**. 

L’image utilisée sera celle qui est spécifiée par la propriété ID de ressource d’ardoise par défaut au moment de la création du canal. L’ardoise est étirée pour s’ajuster à la taille de l’image de l’écran. 

## <a name="insert-slate--images"></a>Insérer des images d’ardoise
L’encodeur dynamique dans le canal peut être informé de basculer vers une image d’ardoise. Il peut également être informé de mettre fin à une ardoise en cours. 

L’encodeur dynamique peut être configuré pour basculer vers une image d’ardoise et masquer le signal vidéo entrant dans certaines situations, par exemple, pendant une pause publicitaire. Si une telle ardoise n’est pas configurée, la vidéo d’entrée n’est pas masquée pendant cette annonce publicitaire.

### <a name="duration"></a>Durée
Durée (en secondes) de l’affichage de l’ardoise. Pour que l’affichage de l’ardoise commence, ce doit être une valeur positive différente de zéro. Si une ardoise est en cours d’affichage et que la durée zéro est spécifiée, cette ardoise en cours va se terminer.

### <a name="insert-slate-on-ad-marker"></a>Insérer une ardoise dans le marqueur de publicité
S’il est défini sur true, ce paramètre configure l’encodeur dynamique pour insérer une image d’ardoise pendant une pause publicitaire. La valeur par défaut est true. 

### <a id="default_slate"></a>ID de ressource d'ardoise par défaut

facultatif. Spécifie l’ID de la ressource Media Services qui contient l’image d’ardoise. La valeur par défaut est Null. 


>[!NOTE] 
>Avant de créer le canal, l’image d’ardoise avec les contraintes suivantes doit être chargée en tant que ressource dédiée (aucun autre fichier ne doit exister dans cette ressource). Cette image est utilisée uniquement lorsque l’encodeur en direct insère une ardoise pour cause de coupure publicitaire ou qu’un signal explicite lui a été envoyé pour qu’il insère une ardoise. L’encodeur en direct peut également passer en mode ardoise pendant certaines conditions d’erreur, par exemple en cas de perte du signal d’entrée. Il n’est pas possible actuellement d’utiliser une image personnalisée lorsque l’encodeur en direct entre dans un état « signal d’entrée perdu » de ce type. Vous pouvez voter pour que cette fonctionnalité [ici](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/10190457-define-custom-slate-image-on-a-live-encoder-channel).


* Résolution maximale de 1920 x 1080
* Taille maximale de 3 Mo.
* Le nom de fichier doit avoir une extension *.jpg.
* L'image doit être téléchargée dans une ressource en tant que seul AssetFile de cette ressource et cet AssetFile doit être marqué comme fichier principal. La ressource ne peut pas être de type stockage chiffré.

Si **l’ID de ressource d’ardoise par défaut** n’est pas spécifié, et que le paramètre **Insérer une ardoise dans le marqueur de publicité** est défini sur **true**, une image d’Azure Media Services par défaut est utilisée pour masquer le flux vidéo d’entrée. Le son est également désactivé pendant l’affichage de l’ardoise. 

## <a name="channels-programs"></a>Programmes du canal
Un canal est associé à des programmes vous permettant de contrôler la publication et le stockage des segments dans un flux dynamique. Les canaux gèrent des programmes. La relation entre canal et programme est très similaire au contenu multimédia traditionnel où un canal présente un flux de contenu constant et un programme est limité à un événement minuté sur ce canal.

Vous pouvez spécifier le nombre d’heures pendant lesquelles vous souhaitez conserver le contenu enregistré pour le programme en définissant la durée de la **fenêtre d’archivage** . Cette valeur peut être comprise entre 5 minutes et 25 heures. La durée de la fenêtre d’archivage détermine également la plage maximale de temps dans laquelle les clients peuvent effectuer des recherches en arrière à partir de la position dynamique actuelle. Les programmes peuvent durer davantage que le laps de temps spécifié, mais le contenu qui se situe en dehors de la longueur de fenêtre est ignoré en permanence. La valeur de cette propriété détermine également la longueur maximale que les manifestes de client peuvent atteindre.

Chaque programme est associé à une ressource qui stocke le contenu diffusé en continu. Un élément multimédia est mappé à un conteneur d’objets blob de blocs dans le compte de stockage Azure et les fichiers de l’élément multimédia sont stockés sous la forme d’objets blob dans ce conteneur. Pour publier le programme afin que vos clients puissent visionner le flux, vous devez créer un localisateur OnDemand pour la ressource associée. Le fait de posséder ce localisateur vous permettra de générer une URL de diffusion en continu que vous pourrez fournir à vos clients.

Un canal prend en charge jusqu’à trois programmes exécutés simultanément, ce qui permet de créer plusieurs archives du même flux entrant. Cela vous permet de publier et d’archiver différentes parties d’un événement en fonction des besoins. Par exemple, imaginez que vous devez archiver 6 heures d’un programme, mais diffuser uniquement les 10 dernières minutes. Pour ce faire, vous devez créer deux programmes exécutés simultanément. Un programme est configuré pour archiver 6 heures de l’événement, mais il n’est pas publié. L’autre programme est configuré pour archiver pendant 10 minutes et il est publié.

Vous ne devez pas réutiliser de programmes existants pour de nouveaux événements. Au lieu de cela, créez et démarrez un nouveau programme pour chaque événement, tel que décrit dans la section Programmation d’applications de streaming en direct.

Démarrez le programme dès que vous êtes prêt à lancer le streaming et l’archivage. Arrêtez le programme chaque fois que vous voulez arrêter le streaming et l’archivage de l’événement. 

Pour supprimer du contenu archivé, arrêtez et supprimez le programme, puis supprimez l’élément multimédia associé. Un élément multimédia ne peut pas être supprimé s’il est utilisé par un programme ; le programme doit d’abord être supprimé. 

Même après l’arrêt et la suppression du programme, les utilisateurs pourront lire votre contenu archivé en tant que vidéo à la demande tant que vous n’aurez pas supprimé l’élément multimédia.

Si vous souhaitez conserver le contenu archivé sans qu’il soit disponible pour la diffusion, supprimez le localisateur de diffusion en continu.

## <a name="getting-a-thumbnail-preview-of-a-live-feed"></a>Obtention d’une image miniature d’un flux en direct
Si le paramètre Encodage en temps réel est activé, vous pouvez désormais obtenir un aperçu du flux en direct lorsqu’il atteint le canal. Ce peut être un outil intéressant lorsqu’il s’agit de vérifier si votre flux en direct atteint réellement le canal. 

## <a id="states"></a>États du canal et mappage des états au mode de facturation
État actuel d’un canal. Les valeurs possibles incluent :

* **Arrêté**. C’est l’état initial du canal après sa création. Dans cet état, les propriétés du canal peuvent être mises à jour, mais le streaming n’est pas autorisé.
* **Démarrage en cours**. Le canal est en cours de démarrage. Aucune mise à jour ni aucun streaming ne sont autorisés durant cet état. Si une erreur se produit, le canal retourne à l’état Arrêté.
* **Exécution en cours**. Le canal est capable de traiter des flux dynamiques.
* **En cours d’arrêt**. Le canal est en cours d’arrêt. Aucune mise à jour ni aucun streaming ne sont autorisés durant cet état.
* **Suppression en cours**. Le canal est en cours de suppression. Aucune mise à jour ni aucun streaming ne sont autorisés durant cet état.

Le tableau suivant montre comment les états du canal sont mappés au mode de facturation. 

| État du canal | Indicateurs de l’interface utilisateur du portail | Facturation ? |
| --- | --- | --- |
| Démarrage en cours |Démarrage en cours |Aucun (état transitoire) |
| Exécution en cours |Prêt (pas de programmes en cours d’exécution)<br/>ou<br/>Streaming (au moins un programme en cours d’exécution) |OUI |
| En cours d’arrêt |En cours d’arrêt |Aucun (état transitoire) |
| Arrêté |Arrêté |Non |

> [!NOTE]
> Actuellement, la moyenne de démarrage du canal est d'environ 2 minutes, mais parfois peut prendre jusqu'à 20 minutes. La réinitialisation du canal peut prendre jusqu’à 5 minutes.
> 
> 

## <a id="Considerations"></a>Considérations
* Quand un canal de type de codage **Standard** subit une perte de flux de source d'entrée/contribution, il compense cette perte en remplaçant l'audio ou la vidéo source par une ardoise d'erreur et un silence. Le canal continue d’émettre une ardoise jusqu’à la reprise du flux d’entrée/de contribution. Nous vous recommandons de ne pas laisser un canal direct dans cet état pendant plus de 2 heures. Au-delà de ce point, ni le comportement du canal au moment de la reconnexion de l’entrée ni son comportement en réponse à une commande de réinitialisation ne sont garantis. Vous devez alors arrêter le canal, le supprimer et en créer un autre.
* Vous ne pouvez pas modifier le protocole d’entrée pendant l’exécution du canal ou de ses programmes associés. Si vous avez besoin d’autres protocoles, vous devez créer des canaux distincts pour chaque protocole d’entrée.
* Chaque fois que vous reconfigurez l’encodeur dynamique, appelez la méthode de réinitialisation **Reset** sur le canal. Avant de réinitialiser le canal, vous devez arrêter le programme. Une fois le canal réinitialisé, redémarrez le programme.
* Un canal peut être arrêté uniquement lorsqu’il est en cours d’exécution et que tous les programmes du canal ont été arrêtés.
* Par défaut, vous pouvez seulement ajouter 5 canaux à votre compte Media Services. Il s’agit d’un quota conditionnel sur tous les nouveaux comptes. Pour plus d’informations, voir [Quotas et limitations](media-services-quotas-and-limitations.md).
* Vous ne pouvez pas modifier le protocole d’entrée pendant l’exécution du canal ou de ses programmes associés. Si vous avez besoin d’autres protocoles, vous devez créer des canaux distincts pour chaque protocole d’entrée.
* Vous êtes facturé uniquement lorsque votre canal est à l’état **En cours d’exécution** . Pour plus d’informations, reportez-vous à [cette](media-services-manage-live-encoder-enabled-channels.md#states) section.
* Actuellement, la durée maximale recommandée d’un événement en direct est de 8 heures. Veuillez contacter amslived à l’adresse Microsoft.com si vous avez besoin d’exécuter un canal sur de plus longues périodes.
* Assurez-vous que le point de terminaison à partir duquel vous souhaitez diffuser du contenu se trouve dans l’état **En cours d’exécution**.
* Seul RTP est pris en charge pour la saisie multilingue lors de la saisie de pistes multilingues et l'encodage en temps réel. Vous pouvez définir jusqu'à 8 flux audio en entrée à l'aide de MPEG-2 TS via RTP. La réception de plusieurs pistes audio avec RTMP ou Smooth Streaming n'est actuellement pas prise en charge. Il n’existe aucune limitation en cas d’encodage live avec des [encodeurs live locaux](media-services-live-streaming-with-onprem-encoders.md), car tout le contenu envoyé au système AMS passe par un canal sans traitement supplémentaire.
* La valeur d'encodage prédéfinie utilise la notion de « fréquence d’images max » de 30 i/s. Par conséquent, si l'entrée est 60 i/s/59,97i, les images d’entrée sont réduites/désentrelacées à 30/29,97 i/s. Si l'entrée est 50 i/s/50i, les images d’entrée sont réduites/désentrelacées à 25 i/s. Si l'entrée est 25 i/s, la sortie reste à 25 i/s.
* N'oubliez pas d'ARRÊTER VOS CANAUX lorsque vous avez terminé. Dans le cas contraire, la facturation continue.

## <a name="known-issues"></a>Problèmes connus
* Le temps de démarrage du canal a été amélioré pour une moyenne de 2 minutes, mais parfois la demande croissante  peut prendre jusqu'à 20 minutes.
* La prise en charge RTP est adaptée aux diffuseurs professionnels. Consultez les notes relatives à RTP dans [ce](https://azure.microsoft.com/blog/2015/04/13/an-introduction-to-live-encoding-with-azure-media-services/) blog.
* Les images d'ardoise doivent être conformes aux restrictions décrites [ici](media-services-manage-live-encoder-enabled-channels.md#default_slate). Si vous essayez de créer un canal à partir d’une ardoise par défaut d’une résolution supérieure à 1920 x 1080, la requête se termine par une erreur.
* Une fois encore... n'oubliez pas d'ARRÊTER VOS CANAUX lorsque vous avez terminé la diffusion en continu. Dans le cas contraire, la facturation continue.

## <a name="next-step"></a>Étape suivante
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Rubriques connexes
[Diffusion d’événements en direct en continu avec Azure Media Services](media-services-overview.md)

[Créer des canaux encodant en temps réel un flux à débit binaire unique en flux à débit binaire adaptatif avec le portail](media-services-portal-creating-live-encoder-enabled-channel.md)

[Créer des canaux encodant en temps réel un flux à débit binaire unique en flux à débit binaire adaptatif avec le Kit de développement logiciel (SDK) .NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)

[Gérer des canaux avec l’API REST](https://docs.microsoft.com/rest/api/media/operations/channel)
 
[Concepts Azure Media Services](media-services-concepts.md)

[Spécification d’ingestion en direct au format MP4 fragmenté Azure Media Services](media-services-fmp4-live-ingest-overview.md)

[live-overview]: ./media/media-services-manage-live-encoder-enabled-channels/media-services-live-streaming-new.png

