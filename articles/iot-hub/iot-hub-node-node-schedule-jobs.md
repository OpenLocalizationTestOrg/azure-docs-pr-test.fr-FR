---
title: "travaux aaaSchedule avec Azure IoT Hub (nœud) | Documents Microsoft"
description: "Comment tooschedule un Azure IoT Hub travail tooinvoke une méthode directe sur plusieurs appareils. Vous utilisez IoT kits de développement Azure hello pour les applications pour appareil Node.js tooimplement hello simulé et un travail de service application toorun hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a>Planifier et diffuser des travaux (Node)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

IoT Hub Azure est un service entièrement géré qui permet une toocreate d’applications principal et les travaux suivi planifier et mettre à jour des millions d’appareils.  Travaux peuvent être utilisés pour hello suivant des actions :

* Mettre à jour les propriétés souhaitées
* Mettre à jour les balises
* Appeler des méthodes directes

Point de vue conceptuel, une tâche encapsule l’un de ces actions et assure le suivi hello la progression de l’exécution par rapport à un ensemble d’appareils, qui est défini par une requête de double du périphérique.  Par exemple, une application back-end peut utiliser un tooinvoke de travail une méthode de redémarrage sur 10 000 périphériques, spécifié par une requête de double dispositif et planifiées à l’avenir.  Cette application peut puis suivent la progression que chacun de ces périphériques de réception et exécuter la méthode de redémarrage hello.

Pour en savoir plus sur chacune de ces fonctionnalités, consultez les articles suivants :

* Double de l’appareil et les propriétés : [prise en main jumeaux de périphérique] [ lnk-get-started-twin] et [didacticiel : comment toouse appareil à deux propriétés][lnk-twin-props]
* méthodes directes : [Guide du développeur IoT Hub - Méthodes directes][lnk-dev-methods] et [Didacticiel : méthodes directes][lnk-c2d-methods]

Ce didacticiel vous explique les procédures suivantes :

* Créer une application d’appareil simulé qui possède une méthode directe qui permet de **lockDoor** qui peut être appelé par hello solution back-end.
* Créer une application de console Node.js que hello appels **lockDoor** méthode directe dans l’application d’appareil simulé hello à l’aide d’un Bonjour de travail et les mises à jour souhaitée des propriétés à l’aide d’un travail de l’appareil.

À la fin de hello de ce didacticiel, vous avez deux applications de console Node.js :

**simDevice.js**, qui se connecte tooyour IoT hub avec l’identité de l’appareil hello et reçoit un **lockDoor** méthode directe.

**scheduleJobService.js**, qui appelle une méthode directe périphérique hello hello appareil simulé application et mise à jour les propriétés souhaitées de double à l’aide d’un travail.

toocomplete ce didacticiel, vous devez hello suivant :

* Node.js version 0.12.x ou version ultérieure. <br/>  [Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Node.js pour ce didacticiel sur Windows ou Linux.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Création d’une application de périphérique simulé
Dans cette section, vous créez une application console Node.js qui répond tooa de méthode directe appelé par le cloud hello, qui déclenche un redémarrage de l’appareil simulé et utilise hello signalées propriétés tooenable double requêtes tooidentify périphériques et quand ils dernier redémarrage.

1. Créez un dossier vide appelé **simDevice**.  Bonjour **simDevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.  Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **simDevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** package SDK de l’appareil et **azure-iot-périphérique-mqtt** package :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. À l’aide d’un éditeur de texte, créez un nouveau **simDevice.js** fichier Bonjour **simDevice** dossier.
4. Ajouter des instructions au début de hello Hello suivant de hello « exiger » **simDevice.js** fichier :
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Ajouter un **connectionString** variable et l’utiliser toocreate un **Client** instance.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Ajouter hello suivant hello toohandle de fonction **lockDoor** (méthode).
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. Ajouter hello suivant du Gestionnaire de hello code tooregister pour hello **lockDoor** (méthode).
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. Enregistrez et fermez hello **simDevice.js** fichier.

> [!NOTE]
> tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a>Planifier des travaux pour appeler une méthode directe et mettre à jour les propriétés d’une représentation d’appareil
Dans cette section, vous créez une application de console Node.js qui lance une distance **lockDoor** sur un périphérique à l’aide des propriétés d’un directe mise à jour et la méthode hello appareil double.

1. Créez un dossier vide appelé **scheduleJobService**.  Bonjour **scheduleJobService** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.  Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **scheduleJobService** dossier, exécutez hello suivant commande tooinstall hello **azure-iothub** package SDK de l’appareil et **azure-iot-périphérique-mqtt**package :
   
    ```
    npm install azure-iothub uuid --save
    ```
3. À l’aide d’un éditeur de texte, créez un nouveau **scheduleJobService.js** fichier Bonjour **scheduleJobService** dossier.
4. Ajouter des instructions au début de hello Hello suivant de hello « exiger » **dmpatterns_gscheduleJobServiceetstarted_service.js** fichier :
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. Ajouter hello après les déclarations de variable et remplacez les valeurs d’espace réservé hello :
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. Ajoutez hello suivant fonction qui sera utilisé toomonitor l’exécution de hello du travail de hello :
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. Ajoutez hello suivant code tooschedule hello travail qui appelle la méthode de périphérique hello :
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. Ajoutez hello suivant double périphérique de code tooschedule hello travail tooupdate hello :
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. Enregistrez et fermez hello **scheduleJobService.js** fichier.

## <a name="run-hello-applications"></a>Exécuter des applications de hello
Vous êtes maintenant prêt toorun les applications hello.

1. Invite de commandes hello Bonjour **simDevice** dossier, exécutez hello suivant toobegin de commande à l’écoute de méthode directe de redémarrage hello.
   
    ```
    node simDevice.js
    ```
2. Invite de commandes hello Bonjour **scheduleJobService** dossier, exécutez hello suivant commande tootrigger hello travaux toolock hello porte et mise à jour hello double
   
    ```
    node scheduleJobService.js
    ```
3. Vous consultez hello appareil réponse toohello méthode directe dans la console hello.

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez utilisé un travail tooschedule un appareil de tooa méthode directe et la mise à jour de hello des propriétés du double hello appareil.

toocontinue mise en route avec IoT Hub et les modèles de gestion des appareils tels qu’à distance sur la mise à jour de microprogramme hello air, consultez :

[Didacticiel : Comment toodo un microprogramme mettre à jour][lnk-fwupdate]

toocontinue mise en route avec IoT Hub, consultez [prise en main d’Azure IoT bord][lnk-iot-edge].

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
