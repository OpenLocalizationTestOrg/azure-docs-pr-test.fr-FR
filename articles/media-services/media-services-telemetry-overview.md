---
title: "aaaAzure Media Services télémétrie | Documents Microsoft"
description: "Cet article donne une vue d’ensemble des données de télémétrie d’Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95c20ec4-c782-4063-8042-b79f95741d28
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 659e1c947a77aad0e4acacb541d95714da4775ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-telemetry"></a>Télémétrie Azure Media Services

Azure Media Services (AMS) vous permet de tooaccess les données de télémétrie/métriques pour ses services. version actuelle de Hello de AMS vous permet de collecter des données de télémétrie pour live **canal**, **StreamingEndpoint**et live **Archive** entités. 

Télémétrie est écrite la table de stockage tooa dans un compte de stockage Azure que vous spécifiez (en règle générale, vous devez utiliser de compte de stockage hello associé à votre compte AMS). 

système de télémétrie Hello ne gère pas de rétention des données. Vous pouvez supprimer les anciennes données de télémétrie hello en supprimant des tables de stockage hello.

Cette rubrique explique comment tooconfigure et consommer des données de télémétrie hello AMS.

## <a name="configuring-telemetry"></a>Configuration de la télémétrie

Vous pouvez configurer la télémétrie sur une granularité au niveau du composant. Il existe deux niveaux de détail : « Normal » et « Détaillé ». Actuellement, les deux niveaux de retourne hello mêmes informations. Il est recommandé de toouse « Normal. 

Hello suivant rubriques indiquent comment les données de télémétrie tooenable :

[Activation de la télémétrie avec .NET](media-services-dotnet-telemetry.md) 

[Activation de la télémétrie avec REST](media-services-rest-telemetry.md)

## <a name="consuming-telemetry-information"></a>informations sur l’utilisation de la télémétrie

Télémétrie est écrit tooan Table de stockage Azure hello compte de stockage que vous avez spécifié lors de la configuration des données de télémétrie pour hello compte Media Services. Cette section décrit les tables de stockage hello pour les mesures de hello.

Vous pouvez utiliser les données de télémétrie dans un des hello suivant façons :

- Lire les données directement à partir de stockage de tables Azure (par exemple, à l’aide de hello SDK de stockage). Pour la description hello des tables de stockage de données de télémétrie, consultez hello **consommation des informations de télémétrie** dans [cela](https://msdn.microsoft.com/library/mt742089.aspx) rubrique.

Ou

- Utiliser hello Bonjour Media Services .NET SDK pour lire les données de stockage, comme décrit dans [cela](media-services-dotnet-telemetry.md) rubrique. 


schéma de télémétrie Hello décrit ci-dessous est conçue toogive de bonnes performances dans les limites de stockage de Table Azure hello :

- Les données sont partitionnées par le compte d’ID et l’ID du service de télémétrie tooallow à partir de chaque toobe service interrogée indépendamment.
- Les partitions contiennent hello date toogive une limite supérieure raisonnable sur la taille de la partition hello.
- Dans le temps inverse ordre tooallow hello plus récent télémétrie éléments toobe clés de ligne sont interrogés pour un service donné.

Cela permet à nombreux toobe requêtes courantes de hello efficace :

- Téléchargement parallèle, indépendant de données pour des services distincts.
- Récupération de toutes les données d’un service donné dans une plage de dates.
- La récupération des données les plus récentes de hello pour un service.

### <a name="telemetry-table-storage-output-schema"></a>Schéma de sortie de stockage de table de données de télémétrie

Les données de télémétrie sont stockées dans l’agrégat d’une table, « TelemetryMetrics20160321 » où « 20160321 » est la date de la table de hello créé. Le système de télémétrie crée une table distincte pour chaque nouveau jour basé sur l’heure UTC 00:00. table de Hello est utilisée toostore des valeurs récurrentes comme vitesse de transmission dans une fenêtre donnée de temps, les octets envoyés, etc. de réception. 

Propriété|Valeur|Exemples/notes
---|---|---
PartitionKey|{account ID}_{entity ID}|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66<br/<br/>Hello compte ID est inclus dans le flux de travail toosimplify clé de partition hello où plusieurs comptes Media Services écrivez toohello même compte de stockage.
RowKey|{secondes toomidnight} _ {valeur aléatoire}|01688_00199<br/><br/>clé de ligne Hello commence par nombre hello des requêtes de style n premières secondes toomidnight tooallow au sein d’une partition. Pour plus d’informations, consultez [cet](../cosmos-db/table-storage-design-guide.md#log-tail-pattern) article. 
Timestamp|Date/Heure|Auto horodateur à partir de la table Azure 2016 de hello-09-09T22:43:42.241Z
Type|type Hello d’entité hello fournissant les données de télémétrie|Channel/StreamingEndpoint/Archive<br/><br/>Le type d’événement est simplement une valeur de chaîne.
Nom|nom Hello d’événement de télémétrie hello|ChannelHeartbeat/StreamingEndpointRequestLog
ObservedTime|l’événement de télémétrie hello Hello temps s’est produite (UTC)|2016-09-09T22:42:36.924Z<br/><br/>Hello observée heure est fournie par la télémétrie de hello envoi hello entité (par exemple un canal). Il peut y avoir des problèmes de synchronisation de l’heure entre les composants, cette valeur est donc approximative
ServiceID|{ID de service}|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
Propriétés spécifiques à une entité|Comme défini par l’événement de hello|StreamName: stream1, Bitrate 10123, …<br/><br/>les propriétés restantes Hello sont définies pour hello donné du type d’événement. Le contenu de la table Azure est constitué de paires clé / valeur.  (autrement dit, des lignes différentes dans la table de hello ont différents ensembles de propriétés).

### <a name="entity-specific-schema"></a>Schéma spécifique à une entité

Il existe trois types d’entrées spécifiques à une entité des données TELEMETRIQUE chaque objet d’un push avec hello suivant fréquence :

- Points de terminaison de diffusion en continu : toutes les 30 secondes
- Canaux en temps réel : toutes les minutes
- Archive en temps réel : toutes les minutes

**Point de terminaison de diffusion en continu**

Propriété|Valeur|Exemples
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Timestamp automatique à partir de la table Azure 2016-09-09T22:43:42.241Z
Type|Type|StreamingEndpoint
Nom|Nom|StreamingEndpointRequestLog
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|ID de service|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
HostName|Nom d’hôte du point de terminaison hello|builddemoserver.origin.mediaservices.windows.net
StatusCode|État HTTP des enregistrements|200
ResultCode|Détails du code de résultat|S_OK
RequestCount|Demande totale dans l’agrégation de hello|3
Octets envoyés|Octets agrégés envoyés|2987358
ServerLatency|Latence moyenne du serveur (stockage inclus)|129
E2ELatency|Latence moyenne de bout en bout|250

**Canal en temps réel**

Propriété|Valeur|Exemples/notes
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Auto horodateur à partir de la table Azure 2016 de hello-09-09T22:43:42.241Z
Type|Type|Canal
Nom|Nom|ChannelHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|ID de service|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
TrackType|Type de piste vidéo/audio/texte|vidéo/audio
TrackName|Nom de la piste de hello|vidéo/audio_1
Bitrate|Suivre la vitesse de transmission|785000
CustomAttributes||   
IncomingBitrate|Vitesse de transmission entrante réelle|784548
OverlapCount|Chevauchement des hello de réception|0
DiscontinuityCount|Discontinuité de piste|0
LastTimestamp|Timestamp des dernières données reçues|1800488800
NonincreasingCount|Nombre de fragments ignorée en raison de l’augmentation toonon l’horodatage|2
UnalignedKeyFrames|Si nous avons reçu des fragments (parmi les différents niveaux de qualité) où les trames-clés ne sont pas alignées |true
UnalignedPresentationTime|Si nous avons reçu des fragments (parmi les différents niveaux/pistes de qualité) où l’heure de présentation n’est pas alignée|true
UnexpectedBitrate|True, si la vitesse de transmission réelle/calculée pour la piste audio/vidéo > 40 000 bits/s et IncomingBitrate == 0 ou IncomingBitrate et actualBitrate diffèrent de 50 % |true
Healthy|True, si <br/>overlapCount, <br/>DiscontinuityCount, <br/>NonIncreasingCount, <br/>UnalignedKeyFrames, <br/>UnalignedPresentationTime, <br/>UnexpectedBitrate<br/> sont tous 0|true<br/><br/>Intègre est une fonction composite qui retourne la valeur false lorsqu’un des hello après le blocage de conditions :<br/><br/>- OverlapCount > 0<br/>- DiscontinuityCount > 0<br/>- NonincreasingCount > 0<br/>- UnalignedKeyFrames == True<br/>- UnalignedPresentationTime == True<br/>- UnexpectedBitrate == True

**Archive en temps réel**

Propriété|Valeur|Exemples/notes
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Auto horodateur à partir de la table Azure 2016 de hello-09-09T22:43:42.241Z
Type|Type|Archivage
Nom|Nom|ArchiveHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|ID de service|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
ManifestName|URL du programme|asset-eb149703-ed0a-483c-91c4-e4066e72cce3/a0a5cfbf-71ec-4bd2-8c01-a92a2b38c9ba.ism
TrackName|Nom de la piste de hello|audio_1
TrackType|Type de piste de hello|Audio/vidéo
CustomAttribute|Chaîne hexadécimale qui fait la distinction entre des pistes différentes avec les mêmes nom et vitesse de transmission (angles multiples de la caméra)|
Bitrate|Suivre la vitesse de transmission|785000
Healthy|True si FragmentDiscardedCount == 0 && ArchiveAcquisitionError == False|True (ces deux valeurs ne sont pas présentes dans la mesure de hello, mais ils sont présents dans les événements de source de hello)<br/><br/>Intègre est une fonction composite qui retourne la valeur false lorsqu’un des hello après le blocage de conditions :<br/><br/>- FragmentDiscardedCount > 0<br/>- ArchiveAcquisitionError == True

## <a name="general-qa"></a>Questions et réponses d’ordre général

### <a name="how-tooconsume-metrics-data"></a>Comment les données de métriques tooconsume ?

Les données de métriques sont stockées comme une série de Tables Azure dans le compte de stockage du client hello. Ces données peuvent être utilisées à l’aide de hello suite d’outils :

- Kit de développement logiciel (SDK) AMS
- Explorateur de stockage Microsoft Azure (prend en charge le format de valeurs séparées par des toocomma d’exportation et traité dans Excel)
- API REST

### <a name="how-toofind-average-bandwidth-consumption"></a>Comment toofind moyenne de consommation de bande passante ?

la consommation de bande passante moyenne Hello est moyenne hello octets envoyés pour un intervalle de temps.

### <a name="how-toodefine-streaming-unit-count"></a>Comment les unités de diffusion en continu toodefine compter ?

nombre d’unités de diffusion en continu de Hello peut être défini comme le débit de pointe hello points de terminaison de diffusion en continu du service hello divisé par le débit de pointe hello d’un point de terminaison de diffusion en continu. débit d’utilisable Hello maximal d’un point de terminaison de diffusion en continu est Mbits/160 s.
Par exemple, supposons que le débit de pointe hello du service d’un client est de 40 Mbits/s (hello valeur maximale d’octets envoyés sur un intervalle de temps). Ensuite, hello nombre d’unités de diffusion en continu est égale too(40 MBps) * (8 bits/octet) /(160 Mbps) = 2 unités de diffusion en continu.

### <a name="how-toofind-average-requestssecond"></a>Comment toofind moyenne demandes/seconde ?

Nombre moyen de hello toofind de demandes/seconde, de calcul nombre moyen de hello de requêtes (nombre de demandes) sur un intervalle de temps.

### <a name="how-toodefine-channel-health"></a>Comment toodefine canal de contrôle d’intégrité ?

Contrôle d’intégrité du canal peut être défini comme une fonction booléenne composite afin qu’il soit false lorsqu’une des conditions suivantes de hello contenir :

- OverlapCount > 0
- DiscontinuityCount > 0
- NonincreasingCount > 0
- UnalignedKeyFrames == True 
- UnalignedPresentationTime == True 
- UnexpectedBitrate == True


### <a name="how-toodetect-discontinuities"></a>Comment toodetect discontinuités ?

des discontinuités toodetect, recherche toutes les entrées de données de canal où DiscontinuityCount > 0. Hello correspondant ObservedTime timestamp indique les heures de hello auquel des discontinuités de hello s’est produite.

### <a name="how-toodetect-timestamp-overlaps"></a>Comment toodetect timestamp chevauche ?

chevauchements d’horodatage toodetect, recherche toutes les entrées de données de canal où OverlapCount > 0. Hello correspondant ObservedTime timestamp indique hello fois à quels hello timestamp chevauche s’est produites.

### <a name="how-toofind-streaming-request-failures-and-reasons"></a>Toofind de diffusion en continu de demander les raisons et les échecs ?

échecs de requêtes de diffusion en continu toofind et raisons, rechercher toutes les entrées de données de point de terminaison de diffusion en continu où ResultCode n’est pas égal tooS_OK. champ de StatusCode Hello correspondant indique la raison hello Échec de la demande hello.

### <a name="how-tooconsume-data-with-external-tools"></a>Comment tooconsume des données avec des outils externes ?

Données TELEMETRIQUE peuvent être traitées et visualisées par hello suite d’outils :

- PowerBI
- Application Insights
- Azure Monitor (anciennement Shoebox)
- Tableau de bord dynamique AMS
- Portail Azure (en attente de publication)

### <a name="how-toomanage-data-retention"></a>La rétention des données toomanage ?

système de télémétrie Hello ne fournit pas gestion de rétention des données ou la suppression automatique des anciens enregistrements. Par conséquent, vous devez toomanage et supprimez manuellement les enregistrements obsolètes à partir de la table de stockage hello. Vous pouvez faire référence toostorage Kit de développement logiciel de façon toodo il.

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
