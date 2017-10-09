---
title: travaux de Azure IoT Hub aaaUnderstand | Documents Microsoft
description: "Guide du développeur - planification toorun travaux sur plusieurs périphériques connectés tooyour IoT hub. Les tâches peuvent mettre à jour les balises et les propriétés souhaitées, et appeler des méthodes directes sur plusieurs appareils."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a>Planifier des travaux sur plusieurs appareils
## <a name="overview"></a>Vue d'ensemble
Comme décrit dans les articles précédents, Azure IoT Hub utilise un certain nombre de composantes ([balises et propriétés de jumeau d’appareil][lnk-twin-devguide], et [méthodes directes][lnk-dev-methods]).  En règle générale, les applications back-end activer tooupdate administrateurs et opérateurs de périphérique et d’interagissent avec des appareils IoT en bloc et à une heure planifiée.  Travaux encapsulent l’exécution de hello de mises à jour des deux périphériques et méthodes directes par rapport à un ensemble d’appareils à la fois de la planification.  Par exemple, un opérateur utiliseriez une application back-end lancer et suivre un travail de tooreboot un ensemble d’appareils dans la construction de 43 et étage 3 à un moment qui ne serait pas toohello sans interruption des opérations de construction de hello.

### <a name="when-toouse"></a>Lorsque toouse
Pensez à l’aide de travaux lorsque : une solution principaux besoins tooschedule et les suivre la progression des hello suivant des activités sur un ensemble de périphériques :

* Mettre à jour les propriétés souhaitées
* Mettre à jour les balises
* Appeler des méthodes directes

## <a name="job-lifecycle"></a>Cycle de vie de tâche
Tâches sont lancées par hello solution back-end et gérées par IoT Hub.  Vous pouvez lancer un travail via une URI de service (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) et vérifier la progression d’un travail en cours via une URI de service (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).  Une fois qu’un travail est initié, interrogation pour les travaux Active l’état de hello hello principal application toorefresh de travaux en cours d’exécution.

> [!NOTE]
> Lorsque vous lancez un travail, les valeurs et les noms de propriété ne peuvent contenir US-ASCII imprimable alphanumérique, à l’exception dans l’ensemble suivant de hello : ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

## <a name="reference-topics"></a>Rubriques de référence :
Hello rubriques de référence suivantes vous fournit plus d’informations sur l’utilisation de travaux.

## <a name="jobs-tooexecute-direct-methods"></a>Méthodes de travaux tooexecute directes
Détails pour l’exécution de la demande hello HTTP 1.1 est Hello suivant un [méthode directe] [ lnk-dev-methods] sur un ensemble de périphériques à l’aide d’une tâche :

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
condition de requête Hello peut également être sur un seul Id de périphérique ou sur une liste d’ID de l’appareil comme indiqué ci-dessous

**Exemples**
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
Le [langage de requête IoT Hub][lnk-query] couvre le langage de requête IoT Hub plus en détail.

## <a name="jobs-tooupdate-device-twin-properties"></a>Propriétés de travaux tooupdate périphérique double
Hello Voici des détails de la demande de mise à jour des propriétés de l’appareil double à l’aide d’un travail hello HTTP 1.1 :

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a>Vérification de la progression des travaux
Hello Voici hello détails de la demande HTTP 1.1 pour [interrogation pour les travaux][lnk-query]:

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

Hello continuationToken est fournie à partir de la réponse de hello.  

## <a name="jobs-properties"></a>Propriétés des travaux
Hello Voici une liste de propriétés et les descriptions correspondantes, ce qui peuvent être utilisées lors de l’interrogation pour les tâches ou les résultats de la tâche.

| Propriété | Description |
| --- | --- |
| **jobId** |Application fourni un ID de tâche de hello. |
| **startTime** |Heure de début application fournie (ISO-8601) pour le travail de hello. |
| **endTime** |IoT Hub fourni date (ISO-8601) de fin du travail hello. Valide uniquement lorsque le travail de hello atteint l’état de hello 'terminé'. |
| **type** |Types de tâches : |
| **scheduledUpdateTwin**: un tooupdate de travail utilisé un ensemble de propriétés souhaitées ou de balises. | |
| **scheduledDeviceMethod**: un tooinvoke de travail utilisé une méthode de l’appareil sur un ensemble de jumeaux de périphérique. | |
| **statut** |État actuel du travail de hello. Valeurs possibles pour l'état : |
| **en attente** : planifié et en attente toobe récupéré par le service de travail hello. | |
| **planifiée** : planifiée pour une heure dans hello futures. | |
| **running** : le travail est actuellement actif. | |
| **cancelled** : le travail a été annulé. | |
| **failed** : échec de la tâche. | |
| **completed** : le travail est terminé..&lt;/seg&gt; | |
| **deviceJobStatistics** |Statistiques sur l’exécution de la tâche hello. |

Propriétés **deviceJobStatistics**.

| Propriété | Description |
| --- | --- |
| **deviceJobStatistics.deviceCount** |Nombre de périphériques dans la tâche de hello. |
| **deviceJobStatistics.failedCount** |Nombre d’appareils où le travail de hello a échoué. |
| **deviceJobStatistics.succeededCount** |Nombre de périphériques sur lequel le travail de hello a réussi. |
| **deviceJobStatistics.runningCount** |Nombre de périphériques qui sont en cours d’exécution des travaux de hello. |
| **deviceJobStatistics.pendingCount** |Nombre de périphériques qui sont en attente de travail de hello toorun. |

### <a name="additional-reference-material"></a>Matériel de référence supplémentaire
Les autres rubriques de référence de hello guide du développeur IoT Hub sont les suivantes :

* [Points de terminaison IoT Hub] [ lnk-endpoints] décrit hello différents points de terminaison qui expose de chaque IoT hub pour les opérations de gestion et d’exécution.
* [Limitation et les quotas] [ lnk-quotas] décrit les quotas hello qui s’appliquent toohello IoT Hub service hello limitation tooexpect de comportement lorsque vous utilisez le service de hello.
* [Azure IoT périphérique et service kits de développement logiciel] [ lnk-sdks] listes hello langue différents kits de développement logiciel vous une utilisation lorsque vous développez des applications de périphérique et le service qui interagissent avec IoT Hub.
* [Langage de requête IoT Hub jumeaux d’appareil, les tâches et le routage des messages] [ lnk-query] décrit le langage de requête IoT Hub vous pouvez utiliser les informations de tooretrieve à partir de IoT Hub sur votre jumeaux de périphérique et les travaux de hello.
* [Prise en charge IoT Hub MQTT] [ lnk-devguide-mqtt] fournit plus d’informations sur la prise en charge IoT Hub pour le protocole MQTT hello.

## <a name="next-steps"></a>Étapes suivantes
Si vous souhaitez que tootry certains des concepts hello décrits dans cet article, peut vous intéresser hello suivant IoT Hub didacticiel :

* [Planifier et diffuser des travaux][lnk-jobs-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
