---
title: "aaaUse métriques toomonitor Azure IoT Hub | Documents Microsoft"
description: "Comment surveiller et toouse Azure IoT Hub métriques tooassess hello l’intégrité globale de vos hubs IoT."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a47108fd-f994-4105-b21d-5b8f697b699c
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7d045013fb0229f488e72c93a6f668048b9d5c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-iot-hub-metrics"></a>Comprendre les métriques IoT Hub
Métriques de IoT Hub vous permettent de mieux données sur l’état de hello des ressources d’Azure IoT hello dans votre abonnement Azure. Activer de métriques IoT Hub vous tooassess hello l’intégrité globale du hello IoT Hub service et les appareils hello connecté tooit. Statistiques de la direction de l’utilisateur sont importants car ils vous permettent de voir ce qui se passe vos problèmes de causes IoT hub et aide sans avoir besoin de toocontact prise en charge Azure.

Les métriques sont activées par défaut. Vous pouvez afficher les métriques de IoT Hub de hello portail Azure.

## <a name="how-tooview-iot-hub-metrics"></a>Comment tooview les métriques IoT Hub
1. Créez un hub IoT. Vous trouverez des instructions sur la façon de toocreate un hub IoT Bonjour [prise en main] [ lnk-get-started] guide.
2. Ouvrez le panneau hello de votre hub IoT. Ici, cliquez sur **Métriques**.
   
    ![][1]
3. À partir du Panneau de métriques hello, vous pouvez afficher les métriques de hello pour votre IoT hub et créer des vues personnalisées de vos mesures de. Vous pouvez choisir toosend votre point de terminaison du service Event Hubs de tooan données métriques ou d’un compte de stockage Azure en cliquant sur **paramètres de diagnostic**.
   
    ![][2]

## <a name="iot-hub-metrics-and-how-toouse-them"></a>Les métriques IoT Hub et la manière dont toouse les
IoT Hub fournit plusieurs mesures toogive une vue d’ensemble de la santé de votre concentrateur et de hello hello nombre total des périphériques connectés. Vous pouvez combiner les informations de plusieurs mesures toopaint une image plus grande d’état hello de hub IoT de hello. Hello tableau suivant décrit les mesures de hello qu'effectue le suivi de chaque IoT hub, et comment chaque mesure est liée toohello globale état hello IoT hub.

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Tentatives d’envoi de message de télémétrie|Nombre|Total|Nombre de toobe de tentative de messages appareil-à-cloud télémétrie envoyé tooyour IoT hub|
|d2c.telemetry.ingress.success|Messages de télémétrie envoyés|Nombre|Total|Nombre de messages de l’appareil-à-cloud télémétrie envoyé tooyour IoT hub|
|c2d.commands.egress.complete.success|Commandes terminées|Nombre|Total|Nombre de commandes cloud-à-appareil effectués par l’appareil de hello|
|c2d.commands.egress.abandon.success|Commandes abandonnées|Nombre|Total|Nombre de commandes cloud-à-appareil abandonnées par le périphérique de hello|
|c2d.commands.egress.reject.success|Commandes rejetées|Nombre|Total|Nombre de commandes cloud-à-appareil rejetés par le périphérique de hello|
|devices.totalDevices|Nombre total d’appareils|Nombre|Total|Nombre de périphériques inscrits tooyour IoT hub|
|devices.connectedDevices.allProtocol|Appareils connectés|Nombre|Total|Nombre d’unités connectées tooyour IoT hub|
|d2c.telemetry.egress.success|Messages de télémétrie remis|Nombre|Total|Nombre de fois où les messages ont été correctement écrites tooendpoints (total)|
|d2c.telemetry.egress.dropped|Messages supprimés|Nombre|Total|Nombre de messages ignorés, car ils ne correspond pas à tous les itinéraires et itinéraire de secours hello a été désactivée.|
|d2c.telemetry.egress.orphaned|Messages orphelins|Nombre|Total|nombre de Hello de messages ne correspond ne pas à tous les itinéraires, y compris la gamme de secours hello|
|d2c.telemetry.egress.invalid|Messages non valides|Nombre|Total|Hello nombre de messages non remis en raison tooincompatibility avec point de terminaison hello|
|d2c.telemetry.egress.fallback|Messages correspondant à une condition de secours|Nombre|Total|Nombre de messages écrits de point de terminaison de secours toohello|
|d2c.endpoints.egress.eventHubs|Messages remis tooEvent points de terminaison de Hub|Nombre|Total|Nombre de messages ont des points de terminaison de Hub tooEvent écrit avec succès|
|d2c.endpoints.latency.eventHubs|Latence des messages des points de terminaison Event Hub|Millisecondes|Moyenne|latence de Hello moyenne entre toohello IoT hub message en entrée et d’entrée de message dans un point de terminaison de Hub d’événements, en millisecondes|
|d2c.endpoints.egress.serviceBusQueues|Messages remis tooService points de terminaison de file d’attente du Bus|Nombre|Total|Nombre de messages ont des points de terminaison de file d’attente du Bus tooService écrit avec succès|
|d2c.endpoints.latency.serviceBusQueues|Latence des messages des points de terminaison de files d’attente Service Bus|Millisecondes|Moyenne|latence de Hello moyenne entre toohello IoT hub message en entrée et d’entrée de message dans un point de terminaison de file d’attente du Bus de Service, en millisecondes|
|d2c.endpoints.egress.serviceBusTopics|Messages remis tooService points de terminaison de la rubrique Bus|Nombre|Total|Nombre de fois où les messages ont été correctement écrit tooService rubrique Bus points de terminaison|
|d2c.endpoints.latency.serviceBusTopics|Latence des messages des points de terminaison de rubriques Service Bus|Millisecondes|Moyenne|latence de Hello moyenne entre toohello IoT hub message en entrée et d’entrée de message dans un point de terminaison de la rubrique Service Bus, en millisecondes|
|d2c.endpoints.egress.builtIn.events|Messages remis du point de terminaison toohello intégrés (messages/événements)|Nombre|Total|Nombre de fois où les messages ont été le point de terminaison a été écrite toohello intégrés (messages/événements)|
|d2c.endpoints.latency.builtIn.events|Latence des messages pour point de terminaison hello intégrés (messages/événements)|Millisecondes|Moyenne|latence de Hello moyenne entre toohello IoT hub message en entrée et d’entrée de message dans hello intégrés point de terminaison (événements/messages), en millisecondes |
|d2c.twin.read.success|Lectures de représentations réussies d’appareils|Nombre|Total|nombre de Hello de toutes les lectures de double d’initiée par l’appareil.|
|d2c.twin.read.failure|Lectures de représentations d’appareils en échec|Nombre|Total|nombre de Hello de tous les échecs d’initiés par le périphérique de double lectures.|
|d2c.twin.read.size|Taille de la réponse des lectures de représentations des appareils|Octets|Moyenne|moyenne de Hello, min et max de réussite initiée par l’appareil à deux lectures.|
|d2c.twin.update.success|Mises à jour de représentations réussies d’appareils|Nombre|Total|nombre de Hello de toutes les mises à jour de double d’initiée par l’appareil.|
|d2c.twin.update.failure|Mises à jour de représentations d’appareils en échec|Nombre|Total|nombre de Hello de tous les échecs d’initiés par le périphérique de double les mises à jour.|
|d2c.twin.update.size|Taille des mises à jour de représentations d’appareils|Octets|Moyenne|moyenne de Hello, min et taille maximale de tous les initiés par le périphérique à deux mises à jour.|
|c2d.methods.success|Appels de méthode directe réussis|Nombre|Total|nombre de Hello réussite directe d’appels de méthode.|
|c2d.methods.failure|Appels de méthode directe en échec|Nombre|Total|nombre de Hello de tous les échecs d’appels de méthode directe.|
|c2d.methods.requestSize|Taille de demande des appels de méthode directe|Octets|Moyenne|moyenne de Hello, min et max de toutes les demandes de méthode directe.|
|c2d.methods.responseSize|Taille de réponse des appels de méthode directe|Octets|Moyenne|moyenne de Hello, min et max de toutes les réponses de réussite méthode directe.|
|c2d.twin.read.success|Lectures de représentations réussies de serveur principal|Nombre|Total|nombre de Hello de toutes les lectures de double d’initiée par back-end.|
|c2d.twin.read.failure|Lectures de représentations de serveur principal en échec|Nombre|Total|nombre de Hello de tous les échecs initiée par back-end de double lectures.|
|c2d.twin.read.size|Taille de la réponse des lectures de représentations de serveur principal|Octets|Moyenne|moyenne de Hello, min et max de réussite initiée par back-end à deux lectures.|
|c2d.twin.update.success|Mises à jour de représentations réussies de serveur principal|Nombre|Total|nombre de Hello de toutes les mises à jour de double d’initiée par back-end.|
|c2d.twin.update.failure|Mises à jour de représentations de serveur principal en échec|Nombre|Total|nombre de Hello de tous les échecs initiée par back-end de double les mises à jour.|
|c2d.twin.update.size|Taille des mises à jour de représentations de serveur principal|Octets|Moyenne|moyenne de Hello, min et max taille de tous les initiée par back-end à deux mises à jour.|
|twinQueries.success|Requêtes de représentations réussies|Nombre|Total|nombre de Hello de toutes les requêtes de double réussie.|
|twinQueries.failure|Requêtes de représentations en échec|Nombre|Total|nombre de Hello de toutes les requêtes ayant échoué double.|
|twinQueries.resultSize|Taille du résultat des requêtes de représentations|Octets|Moyenne|moyenne de Hello, min et max de la taille des résultats de toutes les requêtes réussies double hello.|
|jobs.createTwinUpdateJob.success|Créations réussies des travaux de mises à jour de représentations|Nombre|Total|nombre de Hello de tous les travaux de mise à jour de double réussie.|
|jobs.createTwinUpdateJob.failure|Créations des travaux de mises à jour de représentations en échec|Nombre|Total|nombre de Hello de tout échec de la création de travaux de mise à jour de double.|
|jobs.createDirectMethodJob.success|Créations réussies des travaux d’appel de méthode|Nombre|Total|nombre de Hello de tous les travaux d’appel de méthode directe réussie.|
|jobs.createDirectMethodJob.failure|Créations des travaux d’appel de méthode en échec|Nombre|Total|nombre de Hello de tout échec de la création de travaux d’appel de méthode directe.|
|jobs.listJobs.success|Travaux de toolist appels réussis|Nombre|Total|nombre de Hello de tous les travaux de toolist appels réussis.|
|jobs.listJobs.failure|Échecs des appels toolist travaux|Nombre|Total|nombre de Hello de tous les travaux de toolist d’appels ayant échoué.|
|jobs.cancelJob.success|Annulations de travaux réussies|Nombre|Total|nombre de Hello de réussite appelle toocancel un travail.|
|jobs.cancelJob.failure|Annulations de travaux en échec|Nombre|Total|nombre de Hello de tous les appels ayant échoué toocancel un travail.|
|jobs.queryJobs.success|Requêtes de travaux réussies|Nombre|Total|nombre de Hello de tous les travaux de tooquery appels réussis.|
|jobs.queryJobs.failure|Requêtes de travaux en échec|Nombre|Total|nombre de Hello de tous les travaux de tooquery d’appels ayant échoué.|
|jobs.completed|Travaux terminés|Nombre|Total|nombre de Hello de toutes les tâches terminées.|
|jobs.failed|Travaux en échec|Nombre|Total|nombre de Hello de toutes les tâches ayant échoué.|

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez déjà vu une vue d’ensemble des métriques de IoT Hub, suivez ce lien de toolearn plus d’informations sur la gestion de Azure IoT Hub :

* [Surveillance des opérations][lnk-monitor]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Guide du développeur IoT Hub][lnk-devguide]
* [Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-metrics/enable-metrics-1.png
[2]: media/iot-hub-metrics/enable-metrics-2.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-operations-monitoring]: iot-hub-operations-monitoring.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
