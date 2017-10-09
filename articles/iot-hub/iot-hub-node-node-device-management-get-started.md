---
title: "aaaGet a démarré avec la gestion des appareils Azure IoT Hub (nœud) | Documents Microsoft"
description: "Comment toouse tooinitiate de gestion des appareils IoT Hub un périphérique distant du redémarrage. Vous utilisez hello Azure IoT SDK pour Node.js tooimplement une application d’appareil simulé qui inclut une méthode directe et une application de service qui appelle la méthode directe hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a>Prise en main de la gestion d’appareils (Node)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Ce didacticiel vous explique les procédures suivantes :

* Utilisez hello toocreate portail Azure un IoT Hub et créer une identité d’appareil dans votre hub IoT.
* Créer une application d’appareil simulé disposant d’une méthode directe permettant le redémarrage de cet appareil. Méthodes directes sont appelés à partir du cloud de hello.
* Créer une application de console Node.js qui appelle la méthode directe de redémarrage hello dans l’application d’appareil simulé hello via votre hub IoT.

À la fin de hello de ce didacticiel, vous avez deux applications de console Node.js :

**dmpatterns_getstarted_device.js**, qui connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment, reçoit une méthode directe de redémarrage, simule un redémarrage physique et indique le temps de hello pour le dernier redémarrage de hello.

**dmpatterns_getstarted_service.js**, qui appelle une méthode directe dans l’application d’appareil simulé hello, affiche les réponse hello et hello affiche mis à jour a signalé des propriétés.

toocomplete ce didacticiel, vous devez hello suivant :

* Node.js version 0.12.x ou version ultérieure. <br/>  [Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Node.js pour ce didacticiel sur Windows ou Linux.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Création d’une application de périphérique simulé
Dans cette section, vous allez :

* Créer une application de console Node.js qui répond tooa de méthode directe appelé par le cloud de hello
* Déclencher un redémarrage d’appareil simulé
* Hello d’utilisation signalées propriétés tooenable double requêtes tooidentify périphériques et quand ils dernier redémarrage

1. Créez un dossier vide nommé **manageddevice**.  Bonjour **manageddevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.  Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **manageddevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** package SDK de l’appareil et **azure-iot-périphérique-mqtt**package :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. À l’aide d’un éditeur de texte, créez un **dmpatterns_getstarted_device.js** fichier Bonjour **manageddevice** dossier.
4. Ajouter des instructions au début de hello Hello suivant de hello « exiger » **dmpatterns_getstarted_device.js** fichier :
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Ajouter un **connectionString** variable et l’utiliser toocreate un **Client** instance.  Remplacez la chaîne de connexion hello avec la chaîne de connexion de votre périphérique.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Ajouter hello suivant de méthode directe de fonction tooimplement hello de périphérique de hello
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. Ouvrez tooyour IoT hub hello connexion et démarrer l’écouteur de méthode directe hello :
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. Enregistrez et fermez hello **dmpatterns_getstarted_device.js** fichier.

> [!NOTE]
> tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Déclencher un arrêt à distance sur l’appareil hello à l’aide d’une méthode directe
Dans cette section, vous créez une application console Node.js qui lance un redémarrage à distance sur un appareil avec une méthode directe. application Hello utilise hello de toodiscover requêtes appareil double dernier redémarrage de cet appareil.

1. Créez un dossier vide nommé **triggerrebootondevice**.  Bonjour **triggerrebootondevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.  Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **triggerrebootondevice** dossier, exécutez hello suivant commande tooinstall hello **azure-iothub** package SDK de l’appareil et **azure-iot-périphérique-mqtt** package :
   
    ```
    npm install azure-iothub --save
    ```
3. À l’aide d’un éditeur de texte, créez un **dmpatterns_getstarted_service.js** fichier Bonjour **triggerrebootondevice** dossier.
4. Ajouter des instructions au début de hello Hello suivant de hello « exiger » **dmpatterns_getstarted_service.js** fichier :
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Ajouter hello après les déclarations de variable et remplacez les valeurs d’espace réservé hello :
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. Ajoutez hello suivant fonction tooinvoke hello méthode tooreboot hello cible un périphérique :
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. Ajouter suivant de hello la fonction tooquery pour appareil de hello et obtenir hello dernière heure de redémarrage :
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. Ajoutez hello suivant code toocall hello fonctions qui déclenchent hello redémarrer méthode directe et de requête pour hello redémarrer dernière heure :
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. Enregistrez et fermez hello **dmpatterns_getstarted_service.js** fichier.

## <a name="run-hello-apps"></a>Exécuter des applications de hello
Vous êtes maintenant prêt toorun hello applications.

1. Invite de commandes hello Bonjour **manageddevice** dossier, exécutez hello suivant toobegin de commande à l’écoute de méthode directe de redémarrage hello.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. Invite de commandes hello Bonjour **triggerrebootondevice** dossier, exécutez hello suivant à distance de commande tootrigger hello redémarrer et pour Bonjour appareil double toofind Bonjour redémarrez dernière heure de la requête.
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. Vous consultez hello appareil réponse toohello méthode directe dans la console hello.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
