---
title: "procédure pas à pas solution d’analyse préconfiguré aaaRemote | Documents Microsoft"
description: "Obtenir une description de hello Azure IoT préconfiguré son architecture et surveillance à distance de la solution."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a>Présentation de la solution préconfigurée de surveillance à distance

Hello surveillance à distance IoT Suite [solution préconfigurée] [ lnk-preconfigured-solutions] est une implémentation d’un bout à bout surveillance des solutions pour plusieurs ordinateurs en cours d’exécution dans des emplacements distants. solution de Hello associe des principaux services Azure tooprovide une implémentation générique de scénario d’entreprise hello. Vous pouvez utiliser la solution de hello comme point de départ pour votre propre implémentation et [personnaliser] [ lnk-customize] il toomeet vos propres besoins professionnels spécifiques.

Cet article vous guide certains éléments clés hello tooenable de solution d’analyse à distance hello toounderstand son fonctionnement. Ces connaissances vous aident à :

* Résoudre les problèmes dans les solutions hello.
* Planifier comment toocustomize toohello solution toomeet vos besoins spécifiques. 
* Concevoir votre propre solution IoT utilisant des services Azure.

## <a name="logical-architecture"></a>Architecture logique

Hello suivant schéma présente des composants logiques de hello de solution de hello préconfiguré :

![Architecture logique](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a>Simulations d’appareils

Dans la solution de hello préconfiguré, appareil simulé de hello représente un périphérique de refroidissement (comme un bâtiment climatisation ou l’unité de gestion des installations air). Lorsque vous déployez la solution de hello préconfiguré, vous déployez également automatiquement quatre périphériques simulés qui s’exécutent dans un [la tâche Web Azure][lnk-webjobs]. les appareils Hello simulée facilitent vous tooexplore hello comportement de hello solution sans hello besoin toodeploy tous les périphériques physiques. toodeploy un appareil physique réel, consultez hello [connecter votre solution préconfigurée de surveillance à distance de toohello périphérique] [ lnk-connect-rm] didacticiel.

### <a name="device-to-cloud-messages"></a>Messages appareil-à-cloud

Chaque appareil simulé peut envoyer hello suivant les types de message tooIoT Hub :

| Message | Description |
| --- | --- |
| Démarrage |Lorsque le périphérique de hello démarre, il envoie un **informations de périphérique** message contenant des informations sur lui-même toohello back-end. Ces données incluent l’id de périphérique hello et une liste des commandes hello et méthodes hello périphérique prend en charge. |
| Présence |Un périphérique envoie régulièrement un **présence** tooreport de message si l’appareil de hello peut détecter la présence hello d’un capteur. |
| Télémétrie |Un périphérique envoie régulièrement un **télémétrie** message qui affiche les valeurs de température de hello et de l’humidité collectées à partir de l’appareil de hello simulés de simulée capteurs. |

> [!NOTE]
> solution de Hello stocke la liste hello des commandes prises en charge par le périphérique hello dans une base de données de la base de données Cosmos et non en double d’appareil hello.

### <a name="properties-and-device-twins"></a>Propriétés et représentations d’appareil

Hello simulés périphériques les envoient hello suivant appareil propriétés toohello [double] [ lnk-device-twins] dans hello IoT hub en tant que *signalé propriétés*. Hello envoie de périphérique signalé propriétés au démarrage et dans la réponse tooa **changement d’état appareil** commande ou la méthode.

| Propriété | Objectif |
| --- | --- |
| Config.TelemetryInterval | L’unité de fréquence (secondes) hello envoie des données de télémétrie |
| Config.TemperatureMeanValue | Spécifie la valeur moyenne de hello de télémétrie de température hello simulé |
| Device.DeviceID |ID qui est fourni ou affecté lors de la création d’une unité dans la solution de hello |
| Device.DeviceState | État signalée par le périphérique de hello |
| Device.CreatedTime |APPAREIL hello a été créé dans la solution de hello |
| Device.StartupTime |APPAREIL hello a été démarré. |
| Device.LastDesiredPropertyChange |numéro de version Hello de propriété désirée de hello dernière modification |
| Device.Location.Latitude |Emplacement de latitude de l’appareil de hello |
| Device.Location.Longitude |Emplacement de longitude de l’appareil de hello |
| System.Manufacturer |Fabricant de l'appareil |
| System.ModelNumber |Numéro de modèle du périphérique de hello |
| System.SerialNumber |Numéro de série du périphérique de hello |
| System.FirmwareVersion |Version actuelle du microprogramme sur l’appareil de hello |
| System.Platform |Architecture de la plate-forme de périphérique de hello |
| System.Processor |Périphérique hello en cours d’exécution de processeur |
| System.InstalledRAM |Quantité de RAM installée sur l’appareil de hello |

Simulateur de Hello amorce ces propriétés dans les périphériques simulés avec des exemples de valeurs. Chaque fois que simulateur de hello Initialise un appareil simulé, l’appareil de hello signale hello métadonnées prédéfinies tooIoT Hub en tant que propriétés déclarées. Propriétés déclarées peuvent uniquement être mis à jour par périphérique de hello. toochange une propriété signalée, vous permet de définir une propriété de votre choix dans le portail de la solution. Il incombe hello du périphérique hello pour :

1. Extraire périodiquement des propriétés souhaitées à partir du hub IoT de hello.
2. Mettre à jour sa configuration avec la valeur de la propriété hello souhaité.
3. Envoyer le nouveau concentrateur de retour toohello valeur hello comme propriété signalée.

À partir du tableau de bord hello solution, vous pouvez utiliser *propriétés souhaitée* tooset des propriétés sur un périphérique à l’aide de hello [double de l’appareil][lnk-device-twins]. En règle générale, un appareil lit une valeur de propriété souhaitée tooupdate de concentrateur hello que son état interne et le hello du rapport modifier comme une propriété signalée.

> [!NOTE]
> Hello appareil simulé code utilise uniquement hello **Desired.Config.TemperatureMeanValue** et **Desired.Config.TelemetryInterval** hello tooupdate de propriétés souhaitées signalé a renvoyé des propriétés tooIoT concentrateur. Toutes les autres demandes de modification de propriété de votre choix sont ignorés dans les appareil simulé hello.

### <a name="methods"></a>Méthodes

Hello simulés appareils peuvent gérer hello méthodes suivantes ([direct de méthodes][lnk-direct-methods]) à partir du portail de solution hello via IoT hub de hello appelé :

| Méthode | Description |
| --- | --- |
| InitiateFirmwareUpdate |Fait en sorte que hello appareil tooperform une mise à jour du microprogramme |
| Reboot |Fait en sorte que hello appareil tooreboot |
| FactoryReset |Fait en sorte que tooperform de périphérique hello une réinitialisation |

Certaines méthodes utilisent des propriétés déclarées tooreport sur la progression. Par exemple, hello **InitiateFirmwareUpdate** méthode simule la mise à jour de hello en cours d’exécution en mode asynchrone sur le périphérique de hello. méthode Hello retourne immédiatement sur le périphérique de hello, sans interrompre la tâche asynchrone hello toosend état mises à jour à l’aide du tableau de bord de solution toohello signalé propriétés.

### <a name="commands"></a>Commandes

les appareils Hello simulée peuvent gérer hello suivant les commandes (messages cloud-à-appareil) envoyés à partir du portail de solution hello via IoT hub de hello :

| Commande | Description |
| --- | --- |
| PingDevice |Envoie un *ping* toocheck de périphérique toohello il est actif |
| StartTelemetry |Appareil de hello démarre l’envoi de données de télémétrie |
| StopTelemetry |Appareil de hello cesse d’envoyer des données de télémétrie |
| ChangeSetPointTemp |Valeur de définir le point de hello modifications quels hello autour des données aléatoires sont générées |
| DiagnosticTelemetry |Déclencheurs hello toosend de simulateur d’appareil une valeur de télémétrie supplémentaires (externalTemp) |
| ChangeDeviceState |Modifie une propriété de l’état étendu pour appareil de hello et envoie un message d’information d’appareil hello à partir de l’appareil de hello |

> [!NOTE]
> Pour voir une comparaison de ces commandes (cloud-à-appareil) et des méthodes (méthodes directes), consultez [Conseils pour les communications cloud-à-appareil][lnk-c2d-guidance].

## <a name="iot-hub"></a>IoT Hub

Hello [IoT hub] [ lnk-iothub] reçoit les données envoyées à partir d’appareils de hello dans le cloud de hello et rend les travaux d’Analytique de flux de données Azure (ASA) toohello disponibles. Chaque travail ASA de flux de données utilise un flux d’hello de tooread IoT Hub consommateur groupe distinct des messages à partir de vos appareils.

Hello IoT hub dans les solutions hello également :

- Gère un registre des identités qui stocke les identificateurs hello et les clés d’authentification de tous les périphériques hello autorisés tooconnect toohello portal. Vous pouvez activer et désactiver des appareils via le Registre des identités hello.
- Envoie des commandes tooyour périphériques pour le compte du portail de solution hello.
- Appelle les méthodes sur vos appareils pour le compte du portail de solution hello.
- Gère les représentations d’appareil pour tous les appareils inscrits. Un double appareil stocke des valeurs de propriété de hello signalés par un périphérique. Un double appareil stocke également les propriétés souhaitées, définies dans le portail solution hello pour hello appareil tooretrieve lors de la prochaine connexion.
- Planifications de travaux tooset des propriétés pour plusieurs appareils ou d’appeler des méthodes sur plusieurs appareils.

## <a name="azure-stream-analytics"></a>Azure Stream Analytics

Dans la solution de surveillance à distance de hello [Analytique de flux de données Azure] [ lnk-asa] (ASA) distribue des messages de périphérique reçus par les composants hello IoT hub tooother principal pour le traitement ou de stockage. Différentes tâches ASA réalisent des fonctions spécifiques, en fonction du contenu hello de messages de type hello.

**Tâche 1 : Les informations de périphérique** filtre les messages d’informations de périphérique à partir de flux de messages entrants hello et les envoie de point de terminaison tooan concentrateur d’événements. Un appareil envoie des messages d’informations de périphérique au démarrage et dans la réponse tooa **SendDeviceInfo** commande. Cette tâche utilise hello suivant requête définition tooidentify **informations de périphérique** messages :

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

Ce travail envoie ses tooan sortie concentrateur d’événements pour un traitement ultérieur.

**tâche 2 : règles** compare les valeurs de télémétrie entrantes (température et humidité) aux seuils définis pour chaque appareil. Les valeurs de seuil sont définies dans l’éditeur de règles hello disponible dans le portail de solution hello. Chaque paire appareil/valeur est stockée par horodatage dans un objet blob que Stream Analytics lit comme des **Données de référence**. travail de Hello compare une valeur non vide à seuil de jeu hello pour appareil de hello. Si elle dépasse hello ' >' de condition, produites par la tâche de hello un **alarme** événement qui indique que ce seuil hello est dépassé et fournit le dispositif de hello, valeur et les valeurs d’horodatage. Cette tâche utilise hello suivant requête définition tooidentify télémétrie les messages qui doivent déclencher une alarme :

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

Hello travail envoie ses tooan sortie concentrateur d’événements pour un traitement ultérieur et évite les détails de chaque alerte tooblob de stockage où portail de solution hello peut lire les informations d’alerte hello.

**Tâche 3 : Télémétrie** opère sur les flux de données de télémétrie de périphérique entrant hello de deux manières. Hello envoie d’abord tous les messages de télémétrie à partir du stockage d’objets blob toopersistent hello périphériques de stockage à long terme. Hello calcule ensuite humidité moyenne, minimale et maximale des valeurs sur une fenêtre glissante de cinq minutes et envoie ce stockage tooblob de données. portail de solution Hello lit les données de télémétrie hello graphiques de hello de toopopulate de stockage blob. Cette tâche utilise hello après la définition de la requête :

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a>Event Hubs

Hello **Infos sur l’appareil** et **règles** les travaux ASA sortie leur données tooEvent concentrateurs tooreliably par progression sur toohello **processeur d’événements** en cours d’exécution Bonjour la tâche Web.

## <a name="azure-storage"></a>Stockage Azure

solution de Hello utilise toopersist de stockage d’objets blob Azure toutes les données de télémétrie brut et résumée hello à partir d’appareils de hello dans les solutions hello. portail de Hello lit les données de télémétrie hello graphiques de hello de toopopulate de stockage blob. toodisplay alertes, portail de solution hello lit hello données de stockage d’objets blob qui enregistre lorsque hello a dépassé les valeurs de données de télémétrie configuré des valeurs de seuil. solution de Hello utilise également des objets blob stockage toorecord hello seuil valeurs que vous définissez dans le portail de solution hello.

## <a name="webjobs"></a>WebJobs

En outre simulateurs de périphérique toohosting hello, hello WebJobs dans les solutions hello également hello d’hôte **processeur d’événements** en cours d’exécution dans une tâche Web Azure qui gère les réponses aux commandes. Il utilise la commande réponse messages tooupdate hello commande historique de l’appareil (stocké dans la base de données de la base de données Cosmos hello).

## <a name="cosmos-db"></a>Cosmos DB

solution de Hello utilise une Cosmos DB de base de données toostore informations hello périphériques connectés toohello solution. Ces informations comprennent l’historique de hello des commandes envoyées toodevices à partir du portail de solution hello et des méthodes appelées à partir du portail de solution hello.

## <a name="solution-portal"></a>Portail de la solution

portail de solution Hello est une application web déployée dans le cadre de la solution de hello préconfiguré. pages de clés Hello dans le portail de solution hello sont hello le tableau de bord et de la liste des appareils hello.

### <a name="dashboard"></a>tableau de bord

Cette page dans l’application hello web utilise des contrôles javascript Power BI (consultez [référentiel de PowerBI-visuals](https://www.github.com/Microsoft/PowerBI-visuals)) données de télémétrie hello toovisualize à partir d’appareils de hello. solution de Hello utilise hello ASA télémétrie travail toowrite hello télémétrie tooblob stockage des données.

### <a name="device-list"></a>Liste des appareils

Vous pouvez effectuer les opérations suivantes à partir de cette page dans le portail de solution hello :

* Configurer un nouvel appareil. Cette action définit l’id d’appareil unique hello et génère la clé d’authentification hello. Il écrit les informations hello tooboth de périphérique hello Registre des identités IoT Hub et Cosmos DB base de données spécifique à la solution hello.
* Gérer les propriétés de l’appareil. Cela comprend l’affichage des propriétés existantes et l’intégration des nouvelles propriétés.
* Envoyer les commandes de périphérique tooa.
* Afficher l’historique des commandes hello pour un périphérique.
* Désactiver et activer les appareils.

## <a name="next-steps"></a>Étapes suivantes

Hello billets de blog TechNet suivants fournissent plus de détails sur hello solution préconfigurée de surveillance à distance :

* [La surveillance à distance IoT Suite - sous le capot de hello-](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (en anglais)](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

Vous pouvez continuer la mise en route avec IoT Suite en lisant hello suivant des articles :

* [Se connecter à votre solution préconfigurée de surveillance à distance de toohello périphérique][lnk-connect-rm]
* [Autorisations sur le site de azureiotsuite.com hello][lnk-permissions]

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
