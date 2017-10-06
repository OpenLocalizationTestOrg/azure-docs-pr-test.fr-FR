---
title: "propriétés de double de l’appareil Azure IoT Hub aaaUse (nœud) | Documents Microsoft"
description: "Comment jumeaux dispositif de Azure IoT Hub toouse tooconfigure périphériques. Vous utilisez hello Azure IoT SDK pour Node.js tooimplement une application d’appareil simulé et une application de service qui modifie une configuration de l’appareil à l’aide d’un double de l’appareil."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a>Périphériques de tooconfigure propriétés utilisation souhaitée (nœud)
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

À la fin de hello de ce didacticiel, vous aurez deux applications de console Node.js :

* **SimulateDeviceConfiguration.js**, une application d’appareil simulé qui attend une mise à jour de la configuration souhaitée et signale l’état hello d’un processus de mise à jour de configuration simulé.
* **SetDesiredConfigurationAndQuery.js**, une application back-end Node.js, qui définit hello souhaitée de configuration sur un appareil et requêtes hello le processus de mise à jour de configuration.

> [!NOTE]
> article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.
> 
> 

toocomplete ce didacticiel, vous devez suivant de hello :

* Node.js version 0.10.x ou ultérieure.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

Si vous avez suivi hello [prise en main jumeaux de périphérique] [ lnk-twin-tutorial] didacticiel, vous disposez déjà d’un IoT hub et une identité d’appareil appelé **myDeviceId**; et vous pouvez ignorer toohello [ Créer l’application d’appareil simulé hello] [ lnk-how-to-configure-createapp] section.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a>Créer l’application d’appareil simulé hello
Dans cette section, vous créez une application de console Node.js qui connecte le concentrateur tooyour **myDeviceId**et attend une mise à jour de la configuration souhaitée et signale ensuite les mises à jour sur le processus de mise à jour de configuration hello simulé.

1. Créez un dossier vide nommé **simulatedeviceconfiguration**. Bonjour **simulatedeviceconfiguration** dossier, créez un nouveau fichier package.json à l’aide de hello, la commande suivante à l’invite suivante. Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **simulatedeviceconfiguration** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil**, et **azure-iot-périphérique-mqtt**package :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. À l’aide d’un éditeur de texte, créez un nouveau **SimulateDeviceConfiguration.js** fichier Bonjour **simulatedeviceconfiguration** dossier.
4. Ajouter hello suivant code toohello **SimulateDeviceConfiguration.js** de fichiers et remplacez-le par hello **{chaîne de connexion de périphérique}** espace réservé avec la chaîne de connexion de périphérique hello vous avez copié quand vous créé hello **myDeviceId** identité d’appareil :
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    Hello **Client** objet expose tous les hello méthodes requis toointeract avec jumeaux de périphérique à partir de l’appareil de hello. Hello le code précédent, une fois qu’il initialise hello **Client** de l’objet, récupère hello double de périphérique pour **myDeviceId**et l’attache un gestionnaire de mise à jour hello sur les propriétés de votre choisies. Gestionnaire de Hello vérifie qu’une demande de modification de configuration en comparant hello configIds, puis appelle une méthode qui démarre la modification de la configuration hello.
   
    Notez que pour des raisons de hello de simplicité, de code hello précédent utilise une valeur par défaut codées en dur pour la configuration initiale hello. Une application réelle chargerait probablement la configuration à partir d’un stockage local.
   
   > [!IMPORTANT]
   > Événements de modification de propriété souhaitée sont toujours émis une seule fois lors de la connexion du périphérique, assurez-vous que toocheck qu’il existe une modification réelle dans hello souhaité propriétés avant d’effectuer une action.
   > 
   > 
5. Ajouter hello suivant les méthodes avant hello `client.open()` invocation :
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    Hello **initConfigChange** mises à jour de la méthode a signalé des propriétés sur l’objet de double hello périphérique local avec la demande de mise à jour de configuration hello et jeux hello état trop**en attente**, puis les mises à jour hello appareil double sur le service de hello. Après la mise à jour de double de périphérique hello, elle simule un processus à long terme qui arrête l’exécution de hello de **completeConfigChange**. Cette double de périphérique local hello méthode mises à jour de l’a signalé des propriétés définissant le statut de hello trop**réussite** et suppression hello **pendingConfig** objet. Il met ensuite à jour le double de périphérique hello sur le service de hello.
   
    À noter que, la bande passante toosave indiqué propriétés sont mises à jour en spécifiant uniquement les toobe hello propriétés modifiées (nommé **correctif** Bonjour au-dessus de code), au lieu de remplacer l’ensemble du document hello.
   
   > [!NOTE]
   > Ce didacticiel ne simule pas de comportement pour des mises à jour de configuration simultanées. Certains processus de mise à jour de configuration peuvent être en mesure de tooaccommodate des modifications de configuration de la cible pendant l’exécution de mise à jour hello, d’autres peuvent comporter des tooqueue, ainsi que d’autres utilisateurs peuvent rejeter les avec une condition d’erreur. Assurez-vous que tooconsider hello le comportement souhaité pour votre processus de configuration spécifique et ajouter une logique approprié de hello avant le lancement de la modification de configuration hello.
   > 
   > 
6. Exécutez l’application hello :
   
        node SimulateDeviceConfiguration.js
   
    Vous devez voir le message de type hello `retrieved device twin`. Gardez à l’application hello en cours d’exécution.

## <a name="create-hello-service-app"></a>Créer l’application de service hello
Dans cette section, vous allez créer une application de console Node.js que hello mises à jour *propriétés souhaitée* sur hello double de périphérique associé **myDeviceId** avec un nouvel objet de configuration de télémétrie. Il interroge jumeaux de périphérique hello stockées dans le hub IoT de hello et montre la différence hello entre hello souhaitée et a signalé des configurations de périphérique de hello.

1. Créez un dossier vide nommé **setdesiredandqueryapp**. Bonjour **setdesiredandqueryapp** dossier, créez un nouveau fichier package.json à l’aide de hello, la commande suivante à l’invite suivante. Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **setdesiredandqueryapp** dossier, exécutez hello suivant commande tooinstall hello **azure-iothub** package :
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. À l’aide d’un éditeur de texte, créez un nouveau **SetDesiredAndQuery.js** fichier Bonjour **addtagsandqueryapp** dossier.
4. Ajouter hello suivant code toohello **SetDesiredAndQuery.js** de fichiers et remplacez-le par hello **{chaîne de connexion de hub iot}** espace réservé par chaîne de connexion de IoT Hub vous avez copié lorsque vous avez créé votre hub de hello :
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    Hello **Registre** objet expose tous les hello méthodes requis toointeract avec jumeaux de périphérique à partir du service de hello. Hello le code précédent, une fois qu’il initialise hello **Registre** de l’objet, récupère hello double de périphérique pour **myDeviceId**et met à jour ses propriétés souhaitées par un nouvel objet de configuration de télémétrie. Après cela, il appelle hello **queryTwins** fonction événement 10 secondes.

    > [!IMPORTANT]
    > Cette application interroge IoT Hub toutes les 10 secondes à titre d’exemple. Utilisez des requêtes toogenerate orientés utilisateur rapports entre plusieurs appareils et pas les modifications toodetect. Si votre solution nécessite des notifications d’événements d’appareil en temps réel, utilisez des [notifications jumelles][lnk-twin-notifications].
    > 
    >.

1. Ajouter hello suivant code juste avant hello `registry.getDeviceTwin()` hello de tooimplement invocation **queryTwins** (fonction) :
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    requêtes de code précédentes Hello hello jumeaux appareil stockées dans le hub IoT de hello et commander des photos hello souhaitée et a signalé des configurations de télémétrie. Consultez toohello [langage de requête IoT Hub] [ lnk-query] toolearn comment toogenerate enrichi les rapports sur tous vos appareils.
2. Avec **SimulateDeviceConfiguration.js** en cours d’exécution, exécutez l’application hello avec :
   
        node SetDesiredAndQuery.js 5m
   
    Vous devez voir configuration signalé de hello modifier à partir de **réussite** trop**en attente** trop**réussite** à nouveau avec active de nouveau hello fréquence d’envoi des cinq minutes au lieu de 24 heures.
   
   > [!IMPORTANT]
   > Il existe un délai d’une minute tooa entre l’opération de rapport d’appareil hello et le résultat de la requête hello. Il s’agit de tooenable hello requête infrastructure toowork à très grande échelle. tooretrieve des vues cohérentes d’un double d’appareil unique utilisent hello **getDeviceTwin** méthode Bonjour **Registre** classe.
   > 
   > 

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous définissez la configuration souhaitée en tant que *propriétés souhaitée* à partir d’une application back-end et écrit un toodetect d’application appareil simulé qui changent et simuler un processus de mise à jour de plusieurs étapes reporting son état en tant que  *signalé propriétés* double de périphérique toohello.

Hello utilisation suivant comment les ressources toolearn à :

* envoyer la télémétrie des appareils avec hello [prise en main IoT Hub] [ lnk-iothub-getstarted] (didacticiel),
* planifier ou exécuter des opérations sur les grands ensembles de périphériques Voir hello [planification et les tâches de diffusion] [ lnk-schedule-jobs] didacticiel.
* contrôler les périphériques de manière interactive (telles que l’activation sur un ventilateur à partir d’une application contrôlée par l’utilisateur), avec hello [utiliser les méthodes directes] [ lnk-methods-tutorial] didacticiel.

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
