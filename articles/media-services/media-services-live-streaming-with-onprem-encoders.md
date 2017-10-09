---
title: "aaaStream live avec des encodeurs locaux qui créent les flux de débits - Azure | Documents Microsoft"
description: "Cette rubrique décrit comment tooset un canal qui reçoit plusieurs débits live flux à partir d’un encodeur localement. Hello flux peut ensuite être remis tooclient les applications de lecture via un ou plusieurs points de terminaison, à l’aide de hello suite de protocoles de diffusion en continu adaptatives : HLS, Smooth Streaming, DASH."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: d9f0912d-39ec-4c9c-817b-e5d9fcf1f7ea
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 04/12/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 00709cecfc3b5b5dcfaa8f1e4b25bcf9d470d50b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-with-on-premises-encoders-that-create-multi-bitrate-streams"></a>Streaming en direct avec des encodeurs locaux qui créent des flux multidébits
## <a name="overview"></a>Vue d’ensemble
Dans Azure Media Services, un *canal* représente un pipeline de traitement du contenu vidéo en flux continu. Un canal reçoit des flux d’entrée live de l’une des deux manières suivantes :

* Un encodeur dynamique local envoie un plusieurs débits RTMP ou Smooth Streaming (MP4 fragmenté) toohello chaîne de flux qui n’est pas activé tooperform live encodage avec Media Services. Hello ingéré passer de flux de canaux sans traitement supplémentaire. Cette méthode est appelée *pass-through*. Vous pouvez utiliser hello suivant encodeurs en temps réel qui ont plusieurs débits Smooth Streaming en tant que sortie : Media Excel, Ateme, imaginez les Communications, Envivio, Cisco et élémentaire. Hello suivant encodeurs en temps réel ont RTMP en tant que sortie : Adobe Flash Media d’encodeur Live, Telestream Wirecast, Haivision, Teradek et TriCaster. Un encodeur en temps réel peut également envoyer un canal tooa de flux de données unique à plusieurs débits qui n’est pas activé pour l’encodage live, mais nous ne recommandons pas que. Media Services assure une toocustomers de flux hello qui les demandent.

  > [!NOTE]
  > À l’aide d’une méthode directe d’est le moyen le plus économique hello toodo la diffusion en continu.


* Un encodeur dynamique local envoie un canal unique à plusieurs débits flux toohello est activé tooperform dynamique avec Media Services dans un des hello suivant les formats d’encodage : RTP (MPEG-TS), RTMP ou Smooth Streaming (MP4 fragmenté). canal de Hello effectue ensuite l’encodage dynamique de hello entrants unique à plusieurs débits flux tooa débits (adaptatif) flux vidéo. Media Services assure une toocustomers de flux hello qui les demandent.

À compter de version de hello 2.10 de Media Services, lorsque vous créez un canal, vous pouvez spécifier comment vous souhaitez que votre flux d’entrée du canal tooreceive hello. Vous pouvez également spécifier si vous souhaitez que hello canal tooperform dynamique de codage de votre flux de données. Deux options s'offrent à vous :

* **Transfert direct**: spécifiez cette valeur si vous envisagez de toouse un encodeur dynamique local qui aura un flux de débits (un flux direct) en tant que sortie. Dans ce cas, les flux entrants hello passe par toohello de sortie sans encodage. Il s’agit de comportement hello d’un canal avant la mise en production hello 2.10. Cette rubrique fournit des détails sur l’utilisation des canaux de ce type.
* **Live Encoding**: choisissez cette valeur si vous envisagez de votre flux de débits unique à plusieurs débits flux live tooa toouse Media Services tooencode. N’oubliez pas que laisser un canal d’encodage en temps réel dans l’état **En cours d’exécution** occasionne des frais de facturation. Nous vous recommandons d’arrêter immédiatement vos canaux en cours d’exécution après l’événement de diffusion en continu est tooavoid complète des frais supplémentaires de toutes les heures. Media Services assure une toocustomers de flux hello qui les demandent.

> [!NOTE]
> Cette rubrique décrit les attributs de canaux qui ne sont pas activées encodage dynamique tooperform. Pour plus d’informations sur l’utilisation des canaux activé encodage dynamique tooperform, consultez [en continu à l’aide de flux de débits Azure Media Services toocreate](media-services-manage-live-encoder-enabled-channels.md).
>
>

Hello suivant schéma représente un workflow de diffusion en continu qui utilise un flux de données local encodeur en temps réel toohave plusieurs débits RTMP ou MP4 fragmenté (Smooth Streaming) en tant que sortie.

![Flux de travail live][live-overview]

## <a id="scenario"></a>Scénario courant de streaming en direct
Hello étapes suivantes décrivent les tâches impliquées dans la création d’applications courantes de diffusion en continu.

1. Connecter un ordinateur de tooa caméra vidéo. Démarrez et configurez un encodeur live local qui produit un flux multidébit au format MP4 fragmenté (Smooth Streaming) ou RTMP en sortie. Pour plus d’informations, voir [Prise en charge RTMP et encodeurs live dans Azure Media Services](http://go.microsoft.com/fwlink/?LinkId=532824).

    Vous pouvez également effectuer cette étape après la création du canal.
2. Créez et démarrez un canal.

3. URL de réception du canal de hello de récupérer.

    Hello encodeur en temps réel utilise hello réception du canal de toohello URL toosend hello flux.
4. Récupérer l’URL d’aperçu hello canal.

    Utilisez cette tooverify URL que votre canal reçoit correctement les flux live hello.
5. Créez un programme.

    Lorsque vous utilisez hello portail Azure, la création d’un programme crée également un élément multimédia.

    Lorsque vous utilisez hello SDK .NET ou REST, vous devez toocreate un élément multimédia et toouse cette ressource lors de la création d’un programme.
6. Publier les actifs de hello a associé à un programme de hello.   

    >[!NOTE]
    >Lors de la création de votre compte Azure Media Services, un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. Hello, point de terminaison à partir de laquelle vous souhaitez toostream contenu de diffusion en continu a toobe Bonjour **en cours d’exécution** état.

7. Démarrer le programme de hello lorsque vous êtes prêt toostart diffusion et l’archivage.

8. Si vous le souhaitez, encodeur en direct de hello peut être signalé toostart une publication. publication de Hello est insérée dans le flux de sortie hello.

9. Arrêter le programme de hello chaque fois que vous souhaitez toostop de diffusion en continu et l’archivage des événements de hello.

10. Suppression du programme de hello (et éventuellement supprimer actif de hello).     

## <a id="channel"></a>Description d’un canal et de ses composants associés
### <a id="channel_input"></a>Configurations de l’entrée (réception) des canaux
#### <a id="ingest_protocols"></a>Protocole de streaming de réception
Media Services prend en charge la réception des flux live en utilisant des flux au format MP4 fragmenté ou RTMP multidébit comme protocoles de diffusion en continu. Lors de la réception de hello RTMP protocole de diffusion en continu est activée, deux points de terminaison (entrées) de réception sont créés pour le canal de hello :

* **URL principale**: hello de spécifie une URL qualifiée complète des RTMP principal du canal hello réception du point de terminaison.
* **URL secondaire** (facultatif) : Spécifie hello URL complète des RTMP secondaire du canal hello réception du point de terminaison.

Utilisez les URL secondaire hello tooimprove hello durabilité et tolérance de panne de votre réception flux (comme encodeur basculement et tolérance de panne), en particulier pour les scénarios suivants de hello :

- Encodeur unique double en envoyant des URL du serveur principal et secondaire tooboth :

    Hello principal objectif de ce scénario est tooprovide plus fluctuations toonetwork de résilience et jitters. Certains codeurs RTMP ne gèrent pas correctement les déconnexions du réseau. En cas de déconnexion d’un réseau, un encodeur peut arrêter le codage, puis envoyez pas les données de salutation mis en mémoire tampon quand une reconnexion se produit. Cela provoque parfois des discontinuités et des pertes de données. Déconnexion du réseau peut se produire en raison d’un réseau incorrecte ou de maintenance sur hello côté Azure. Principal/secondaire URL réduisent les problèmes de réseau hello et fournissent un processus de mise à niveau contrôlé. Chaque fois qu’une déconnexion réseau planifiée se produit, Media Services gère hello principal et secondaire se déconnecte et fournit un retardée déconnecter entre hello deux. Encodeurs ont tookeep heure envoi de données, puis reconnectez-vous. commande Hello Hello déconnecte peut être aléatoire, mais il y aura toujours un délai entre l’URL principal/secondaire ou principal de base de données secondaire. Dans ce scénario, les encodeur hello sont toujours de point de défaillance unique de hello.

- Plusieurs encodeurs, avec chaque encoder en exécutant un push tooa dédié point :

    Ce scénario met en place une redondance d’encodeurs et d’ingestion. Dans ce scénario, encoder1 pousse les URL principale toohello et encoder2 exécute un push de toohello des URL secondaire. En cas d’échec d’un encodeur, hello autres encodeur peut conserver envoi de données. La redondance des données peut être assurée, car les Services de support ne déconnecte pas l’URL principales et secondaires à hello même temps. Ce scénario suppose que les encodeurs sont synchronisés et fournissent exactement hello des mêmes données.  

- Plusieurs encodeurs double en envoyant des URL du serveur principal et secondaire tooboth :

    Dans ce scénario, les encodeurs de push de données tooboth les URL principale et secondaire. Cela fournit la meilleure fiabilité de hello et la tolérance de panne, ainsi que la redondance des données. Ce scénario peut tolérer une panne des deux encodeurs, ainsi que des déconnexions, même si l’un des encodeurs cesse de fonctionner. Il suppose que les encodeurs sont synchronisés et fournissent exactement hello des mêmes données.  

Pour plus d’informations sur les encodeurs live RTMP, consultez la page [Prise en charge RTMP et encodeurs live dans Azure Media Services](http://go.microsoft.com/fwlink/?LinkId=532824).

#### <a name="ingest-urls-endpoints"></a>URL (points de terminaison) de réception
Un canal fournit un point de terminaison d’entrée (URL de réception) que vous spécifiez dans l’encodeur en temps réel de hello, afin de l’encodeur de hello pouvez pousser le flux tooyour canaux.   

Vous pouvez obtenir hello URL d’ingestion lorsque vous créez le canal de hello. Pour vous tooget ces URL, le canal de hello n’a pas toobe Bonjour **en cours d’exécution** état. Lorsque vous êtes prêt toostart toohello le canal de données de distribution, le canal de hello doit être Bonjour **en cours d’exécution** état. Après le démarrage de la réception de données par le canal de hello, vous pouvez afficher un aperçu de votre flux de données via une URL d’aperçu hello.

Vous avez la possibilité de recevoir un flux live au format MP4 fragmenté (Smooth Streaming) via une connexion SSL. tooingest via le protocole SSL, assurez-vous que tooupdate hello tooHTTPS de l’URL de réception. Il n’est pas possible de recevoir un flux RTMP via SSL pour le moment.

#### <a id="keyframe_interval"></a>Intervalle d’image clé
Lorsque vous utilisez un flux de débits toogenerate local encodeur en temps réel, intervalle d’image clé hello spécifie la durée hello du groupe hello d’images (GOP) utilisé par cet encodeur externe. Une fois que le canal de hello reçoit ce flux entrant, vous pouvez remettre à votre flux dynamique tooclient des applications de lecture dans un des hello suivant formats : diffusion en continu lisse, une diffusion en continu adaptative dynamique via HTTP (tiret) et HTTP Live Streaming (HLS). Lors du streaming en direct, HLS est toujours empaquetée de façon dynamique. Par défaut, Media Services calcule automatiquement hello TLS empaquetage coefficient de segment (fragments par segment) en fonction de l’intervalle d’image clé hello qui est reçu à partir de l’encodeur en temps réel de hello.

Hello tableau suivant montre comment la durée du segment hello est calculée :

| Intervalle d’image clé | Coefficient d’empaquetage de segment HLS (FragmentsPerSegment) | Exemple |
| --- | --- | --- |
| Inférieur ou égal à too3 secondes |3 |Si KeyFrameInterval (ou groupe d’images) est de 2 secondes, le coefficient d’empaquetage de segment TLS hello par défaut est 3 too1. Cela crée un segment HLS de 6 secondes. |
| too5 3 secondes |2:1 |Si KeyFrameInterval (ou groupe d’images) est de 4 secondes, le coefficient d’empaquetage de segment TLS hello par défaut est 2 too1. Cela crée un segment HLS de 8 secondes. |
| Supérieur à 5 secondes |1:1 |Si KeyFrameInterval (ou groupe d’images) est de 6 secondes, le coefficient d’empaquetage de segment TLS hello par défaut est 1 too1. Cela crée un segment HLS de 6 secondes. |

Vous pouvez modifier le taux de fragments par segment hello en sortie du canal configuration hello et en réglant FragmentsPerSegment sur ChannelOutputHls.

Vous pouvez également modifier la valeur d’intervalle hello image clé en définissant la propriété de KeyFrameInterval hello sur ChanneInput. Si vous définissez explicitement KeyFrameInterval, le coefficient d’empaquetage de segment TLS hello FragmentsPerSegment est calculée à l’aide des règles de hello décrites précédemment.  

Si vous définissez explicitement KeyFrameInterval et FragmentsPerSegment, Media Services utilisera les valeurs hello que vous définissez.

#### <a name="allowed-ip-addresses"></a>Adresses IP autorisées
Vous pouvez définir les adresses IP hello autorisées toopublish toothis vidéo channel. Une adresse IP autorisée peut être spécifiée en tant que valeurs hello suivantes :

* Une adresse IP unique (par exemple, 10.0.0.1)
* une plage d’adresses IP utilisant une adresse IP et un masque de sous-réseau CIDR (par exemple, 10.0.0.1/22)
* une plage d’adresses IP utilisant une adresse IP et un masque de sous-réseau décimal séparé par des points (par exemple, 10.0.0.1(255.255.252.0))

Si aucune adresse IP n’est spécifiée et qu’il n’existe pas de définition de règle, alors aucune adresse IP ne sera autorisée. tooallow n’importe quelle adresse IP, créez une règle et définissez 0.0.0.0/0.

### <a name="channel-preview"></a>Aperçu du canal
#### <a name="preview-urls"></a>URL d’aperçu
Les canaux fournissent un aperçu point de terminaison (URL d’aperçu) que vous utilisez toopreview et validez votre flux de données avant de poursuivre le traitement et de remise.

Vous pouvez obtenir les URL d’aperçu hello lorsque vous créez le canal de hello. Pour vous tooget hello URL canal de hello n’a pas toobe Bonjour **en cours d’exécution** état. Après le démarrage de la réception de données par le canal de hello, vous pouvez afficher un aperçu de votre flux de données.

Actuellement, les flux d’aperçu hello peut être remis uniquement dans MP4 fragmenté (Smooth Streaming) format, quel que soit hello spécifié type d’entrée. Vous pouvez utiliser hello [analyse l’intégrité de la diffusion en continu lisse](http://smf.cloudapp.net/healthmonitor) contenu smooth Streaming lecteur tootest hello. Vous pouvez également utiliser un lecteur qui a hébergé Bonjour tooview portail Azure à votre flux de données.

#### <a name="allowed-ip-addresses"></a>Adresses IP autorisées
Vous pouvez définir les adresses IP hello qui sont autorisés à point de terminaison tooconnect toohello aperçu. Si aucune adresse IP n’est spécifiée, toutes les adresses IP sont autorisées. Une adresse IP autorisée peut être spécifiée en tant que valeurs hello suivantes :

* Une adresse IP unique (par exemple, 10.0.0.1)
* une plage d’adresses IP utilisant une adresse IP et un masque de sous-réseau CIDR (par exemple, 10.0.0.1/22)
* une plage d’adresses IP utilisant une adresse IP et un masque de sous-réseau décimal séparé par des points (par exemple, 10.0.0.1(255.255.252.0))

### <a name="channel-output"></a>Sortie du canal
Pour plus d’informations sur les canaux de sortie, consultez hello [intervalle d’image clé](#keyframe_interval) section.

### <a name="channel-managed-programs"></a>Programmes gérés par canal
Un canal est associé à des programmes que vous pouvez utiliser la publication toocontrol hello et stockage des segments dans un flux en direct. Les canaux gèrent les programmes. Hello relation canal et un programme est très similaire media tootraditional, où un canal possède un flux constant de contenu et un programme est événements étendue toosome a expiré sur le canal.

Vous pouvez spécifier le nombre de hello d’heures que vous voulez tooretain hello enregistrée contenu pour le programme de hello en définissant un hello **fenêtre d’Archive** longueur. Cette valeur peut être définie à partir d’un minimum de 5 minutes tooa 25 heures maximum. Longueur de fenêtre d’archive détermine également hello durée maximale pendant laquelle les clients peuvent effectuer des recherches dans le temps à partir de la position de diffusion en continu hello actuel. Programmes peuvent s’exécuter sur la durée spécifiée hello, mais le contenu qui se trouve derrière la longueur de la fenêtre hello est ignoré en permanence. La valeur de cette propriété détermine également la durée pendant laquelle hello client manifestes peuvent atteindre.

Chaque programme est associé à un élément multimédia qui stocke le contenu de diffusion en continu de hello. Un élément multimédia est le conteneur d’objets blob de blocs tooa mappé dans le compte de stockage Azure hello et fichiers hello asset de hello sont stockés en tant qu’objets BLOB dans le conteneur. programme de hello toopublish afin que vos clients puissent afficher les flux hello, vous devez créer un localisateur OnDemand pour un composant de hello associé. Vous pouvez utiliser cette toobuild recherche une URL de diffusion en continu que vous pouvez fournir tooyour clients.

Un canal prend en charge jusqu'à toothree exécuter simultanément des programmes, vous pouvez créer plusieurs archives de hello même flux entrant. Vous pouvez publier et archiver différentes parties d’un événement en fonction des besoins. Par exemple, imaginez que vos exigences d’entreprise est tooarchive 6 heures d’un programme, mais toobroadcast les hello uniquement les 10 dernières minutes. tooaccomplish, vous devez toocreate deux des programmes qui s’exécutent simultanément. Un programme a la valeur tooarchive d’événement de hello les 6 heures, mais les programme hello ne sont pas publié. Hello autre programme est ensemble tooarchive pendant 10 minutes, et ce programme est publié.

Vous ne devez pas réutiliser de programmes existants pour de nouveaux événements. Créez plutôt un programme pour chaque événement. Démarrer le programme de hello lorsque vous êtes prêt toostart diffusion et l’archivage. Arrêter le programme de hello chaque fois que vous souhaitez toostop de diffusion en continu et l’archivage des événements de hello.

contenu de toodelete archivé, arrêter et supprimer hello programme, puis supprimez actif associé de hello. Un élément multimédia ne peut pas être supprimé si un programme l’utilise. programme de Hello doit d’abord être supprimée.

Même après l’arrêt et suppression du programme de hello, les utilisateurs peuvent diffuser votre contenu archivé comme une vidéo à la demande, jusqu'à ce que vous supprimez hello actif. Si vous souhaitez tooretain hello archivé contenu mais n’êtes pas le disponible pour la diffusion en continu, supprimez hello localisateur de diffusion en continu.

## <a id="states"></a>États du canal et facturation
Les valeurs possibles pour l’état actuel d’un canal hello sont les suivantes :

* **Arrêté**: il s’agit d’état initial de hello du canal de hello après sa création. Dans cet état, les propriétés de canal hello peuvent être mis à jour, mais de diffusion en continu n’est pas autorisée.
* **Démarrage**: canal de hello est en cours de démarrage. Aucune mise à jour ni aucun streaming ne sont autorisés durant cet état. Si une erreur se produit, le canal de hello retourne toohello **arrêté** état.
* **En cours d’exécution**: canal de hello peut traiter des flux live.
* **L’arrêt**: canal de hello est en cours d’arrêt. Aucune mise à jour ni aucun streaming ne sont autorisés durant cet état.
* **Suppression**: canal de hello est en cours de suppression. Aucune mise à jour ni aucun streaming ne sont autorisés durant cet état.

Hello tableau suivant montre comment canal indique le mode de facturation toohello mappage.

| État du canal | Indicateurs de l’interface utilisateur du portail | Facturation ? |
| --- | --- | --- | --- |
| **Démarrage en cours** |**Démarrage en cours** |Aucun (état transitoire) |
| **Exécution** |**Prêt** (aucun programme en cours d’exécution)<p><p>ou<p>**Diffusion en continu** (au moins un programme en cours d’exécution) |Oui |
| **En cours d’arrêt** |**En cours d’arrêt** |Aucun (état transitoire) |
| **Arrêté** |**Arrêté** |Non |

## <a id="cc_and_ads"></a>Sous-titrage codé et insertion de publicités
Hello tableau suivant montre les normes prises en charge de sous-titrage et d’insertion de publicité.

| Standard | Remarques |
| --- | --- |
| CEA-708 et EIA-608 (708/608) |CEA-708 et EIA-608 sont sous-titrage normes pour hello États-Unis et au Canada.<p><p>Actuellement, le sous-titrage est pris en charge uniquement si contenues dans le flux d’entrée de hello encodé. Vous devez toouse un encodeur multimédias en direct qui peut insérer 608 ou 708 sous-titres dans le flux encodé hello qui a envoyé les Services tooMedia. Media Services fournit le contenu de hello visionneuses tooyour de sous-titres insérés. |
| TTML dans .ismt (pistes textuelles Smooth Streaming) |Empaquetage dynamique de Media Services permet à votre contenu toostream de clients dans un des hello suivant formats : DASH, HLS ou Smooth Streaming. Toutefois, si vous réception fragmenté MP4 (Smooth Streaming) avec des légendes à l’intérieur du format .ismt (pistes de texte Smooth Streaming), vous pouvez remettre hello flux tooonly clients Smooth Streaming. |
| SCTE-35 |SCTE-35 est un système de signalisation numérique qui a utilisé l’insertion de publicités toocue. Récepteurs en aval utilisent la publicité toosplice hello signal dans le flux de données hello pour hello période. SCTE-35 doit être envoyé sous forme de piste partiellement dans les flux d’entrée hello.<p><p>Actuellement, le format de flux d’entrée hello uniquement pris en charge qui transporte les signaux est fragmenté MP4 (Smooth Streaming). format de sortie Hello uniquement pris en charge est également Smooth Streaming. |

## <a id="considerations"></a>Considérations
Lorsque vous utilisez un toosend d’encodeur dynamique local un canal de tooa de flux de débits, hello suivant les contraintes s’appliquent :

* Assurez-vous que vous avez suffisamment libre Internet connectivité toosend données toohello réception points.
* L’utilisation d’une URL de réception secondaire nécessite de la bande passante supplémentaire.
* flux de débits entrants Hello peut avoir un maximum de 10 niveaux de qualité vidéo (couches) et un maximum de 5 pistes audio.
* Hello plus haut débit binaire moyen pour un des niveaux de qualité vidéo hello doit être inférieure à 10 Mbits/s.
* Hello agrégat de débits binaires de moyenne hello pour tous les flux audio et vidéo de hello doit être inférieure à 25 Mbits/s.
* Vous ne pouvez pas modifier le protocole d’entrée de hello lors de la couche de hello ou ses programmes associés sont en cours d’exécution. Si vous avez besoin d’autres protocoles, vous devez créer des canaux distincts pour chaque protocole d’entrée.
* Vous pouvez recevoir un flux à débit binaire unique. Mais étant donné que le canal de hello ne traite pas les flux de hello, les applications clientes hello recevront également un flux à débit binaire unique. (Nous ne recommandons pas cette option.)

Voici les autres tooworking connexes considérations avec les canaux et les composants associés :

* Chaque fois que vous reconfigurez encodeur en direct de hello, appelez hello **réinitialiser** méthode sur le canal de hello. Avant de réinitialiser le canal de hello, vous disposez de programme de hello toostop. Après avoir réinitialisé le canal de hello, redémarrez le programme de hello.
* Un canal peut être arrêté seulement quand il est Bonjour **en cours d’exécution** état et tous les programmes sur le canal de hello ont été arrêtés.
* Par défaut, vous pouvez ajouter le compte de service de média seulement 5 canaux tooyour. Pour plus d’informations, consultez [Quotas et limitations](media-services-quotas-and-limitations.md).
* Vous êtes facturé uniquement quand votre canal est Bonjour **en cours d’exécution** état. Pour plus d’informations, consultez toohello [Channel États et facturation](media-services-live-streaming-with-onprem-encoders.md#states) section.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="feedback"></a>Commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Rubriques connexes
[Spécification d’ingestion en direct au format MP4 fragmenté Azure Media Services](media-services-fmp4-live-ingest-overview.md)

[Vue d’ensemble d’Azure Media Services et scénarios courants](media-services-overview.md)

[Concepts Media Services](media-services-concepts.md)

[live-overview]: ./media/media-services-manage-channels-overview/media-services-live-streaming-current.png
