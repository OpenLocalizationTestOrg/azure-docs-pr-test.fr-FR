---
title: "aaaAzure IoT Hub direct de méthodes (nœud) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub direct de méthodes. Vous utilisez hello Azure IoT SDK pour Node.js tooimplement une application d’appareil simulé qui inclut une méthode directe et une application de service qui appelle la méthode directe hello."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a>Utilisation de méthodes directes sur votre appareil IoT avec Node.js
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

À la fin de hello de ce didacticiel, vous avez deux applications de console Node.js :

* **CallMethodOnDevice.js**, qui appelle une méthode dans l’application d’appareil simulé hello et affiche la réponse de hello.
* **SimulatedDevice.js**, qui se connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et répond méthode toohello appelée par le cloud de hello.

> [!NOTE]
> article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild toorun de deux applications sur les périphériques et votre principal de la solution.
> 
> 

toocomplete ce didacticiel, vous devez hello suivant :

* Node.js version 0.10.x ou ultérieure.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Création d’une application de périphérique simulé
Dans cette section, vous créez une application console Node.js qui répond méthode tooa appelée par le cloud de hello.

1. Créez un dossier vide appelé **simulateddevice**. Bonjour **simulateddevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante. Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **simulateddevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** package SDK de l’appareil et **azure-iot-périphérique-mqtt**package :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. À l’aide d’un éditeur de texte, créez un nouveau **SimulatedDevice.js** fichier Bonjour **simulateddevice** dossier.
4. Ajoutez hello suivant `require` instructions au hello démarrent Hello **SimulatedDevice.js** fichier :
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Ajouter un **connectionString** variable et l’utiliser toocreate un **DeviceClient** instance. Remplacez **{chaîne de connexion de périphérique}** avec chaîne de connexion de périphérique hello générées dans hello *créer une identité d’appareil* section :
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Ajoutez hello suivant fonction tooimplement hello (méthode) sur l’appareil de hello :
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Ouvrez tooyour IoT hub hello connexion et démarrer l’écouteur de méthode initialize hello :
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. Enregistrez et fermez hello **SimulatedDevice.js** fichier.

> [!NOTE]
> tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, les tentatives de connexion), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].
> 
> 

## <a name="call-a-method-on-a-device"></a>Appeler une méthode sur un appareil
Dans cette section, vous créez une application de console Node.js qui appelle une méthode dans l’application d’appareil simulé hello et affiche ensuite la réponse de hello.

1. Créez un dossier vide nommé **callmethodondevice**. Bonjour **callmethodondevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante. Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **callmethodondevice** dossier, exécutez hello suivant commande tooinstall hello **azure-iothub** package :
   
    ```
    npm install azure-iothub --save
    ```
3. À l’aide d’un éditeur de texte, créez un **CallMethodOnDevice.js** fichier Bonjour **callmethodondevice** dossier.
4. Ajoutez hello suivant `require` instructions au hello démarrent Hello **CallMethodOnDevice.js** fichier :
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. Ajouter hello après la déclaration de variable et remplacer la valeur d’espace réservé de hello par hello chaîne de connexion de IoT Hub pour votre concentrateur :
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. Créez hello client tooopen hello connexion tooyour IoT hub.
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. Ajoutez hello suivant fonction tooinvoke hello (méthode) et impression hello appareil réponse toohello console de l’appareil :
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. Enregistrez et fermez hello **CallMethodOnDevice.js** fichier.

## <a name="run-hello-apps"></a>Exécuter des applications de hello
Vous êtes maintenant prêt toorun hello applications.

1. À l’invite de commande Bonjour **simulateddevice** dossier, exécutez hello suivant toostart commande écoute les appels de méthode à partir de votre IoT Hub :
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. À l’invite de commande Bonjour **callmethodondevice** dossier, exécutez hello suivant toobegin commande analyse votre IoT hub :
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. Vous verrez l’appareil de hello réagir toohello méthode par l’impression de message de type hello et application hello appelée réponse de hello hello méthode affichage à partir de l’appareil de hello :
   
    ![][9]

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub. Vous avez utilisé ce périphérique identité tooenable hello simulée appareil application tooreact toomethods appelée par le cloud de hello. Vous avez créé également une application qui appelle des méthodes sur l’appareil de hello et affiche la réponse hello périphérique de hello. 

toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :

* [Prise en main d’IoT Hub]
* [Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]

toolearn tooextend votre méthode de planification et de solution IoT des appels sur plusieurs appareils, consultez hello [planification et les tâches de diffusion] [ lnk-tutorial-jobs] didacticiel.

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Prise en main d’IoT Hub]: iot-hub-node-node-getstarted.md
