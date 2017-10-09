---
title: "aaaGet en main Azure IoT Hub (nœud) | Documents Microsoft"
description: "Découvrez comment toosend appareil-à-cloud messages tooAzure IoT Hub à l’aide de kits de développement logiciel IoT pour Node.js. Créer appareil simulé et tooregister des applications de service de votre appareil, envoyer des messages et lire les messages de hub IoT."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a>Connectez votre concentrateur de IoT tooyour appareil simulé à l’aide du nœud
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

À la fin de hello de ce didacticiel, vous avez trois applications de console Node.js :

* **CreateDeviceIdentity.js**, ce qui crée une identité d’appareil et clé de sécurité associés tooconnect votre application d’appareil simulé.
* **ReadDeviceToCloudMessages.js**, qui affiche la télémétrie hello envoyée par votre application d’appareil simulé.
* **SimulatedDevice.js**, qui se connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et envoie un message de télémétrie chaque seconde à l’aide de hello le protocole MQTT.

> [!NOTE]
> article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild toorun de deux applications sur les périphériques et votre principal de la solution.
> 
> 

toocomplete ce didacticiel, vous devez hello suivant :

* Node.js version 0.10.x ou ultérieure.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Votre IoT Hub est maintenant créé. Vous avez hello nom d’hôte IoT Hub et hello chaîne de connexion IoT Hub que vous avez besoin reste de hello toocomplete de ce didacticiel.

## <a name="create-a-device-identity"></a>Création d’une identité d’appareil
Dans cette section, vous créer une application de console Node.js qui crée une identité d’appareil dans le Registre des identités hello dans votre hub IoT. Appareils de se connecter uniquement tooIoT hub si elle a une entrée dans le Registre des identités hello. Pour plus d’informations, consultez hello **Registre des identités** section Hello [guide du développeur IoT Hub][lnk-devguide-identity]. Lorsque vous exécutez cette application console, il génère un ID d’appareil unique et clé que votre appareil peut utiliser tooidentify lui-même lorsqu’il envoie l’appareil-à-cloud messages tooIoT Hub.

1. Créez un dossier vide appelé **createdeviceidentity**. Bonjour **createdeviceidentity** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante. Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **createdeviceidentity** dossier, exécutez hello suivant commande tooinstall hello **azure-iothub** package SDK de Service :
   
    ```
    npm install azure-iothub --save
    ```
3. À l’aide d’un éditeur de texte, créez un **CreateDeviceIdentity.js** fichier Bonjour **createdeviceidentity** dossier.
4. Ajoutez hello suivant `require` instruction au début de hello de hello **CreateDeviceIdentity.js** fichier :
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. Ajouter hello suivant code toohello **CreateDeviceIdentity.js** de fichiers et de remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello vous avez créé dans la section précédente de hello de : 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. Ajoutez hello suivant code toocreate une définition de périphérique dans le Registre des identités hello dans votre hub IoT. Ce code crée un appareil si l’ID de périphérique hello n’existe pas dans le Registre des identités hello, sinon elle retourne la clé hello d’unité de hello existante :
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. Enregistrez et fermez le fichier **CreateDeviceIdentity.js** .
8. toorun hello **createdeviceidentity** application, exécutez hello commande à l’invite de commandes hello dans le dossier de createdeviceidentity hello suivante :
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. Prenez note de hello **ID de périphérique** et **clé de périphérique**. Vous avez besoin de ces valeurs lorsque vous créez une application qui se connecte tooIoT Hub en tant que périphérique.

> [!NOTE]
> Hello Registre des identités IoT Hub stocke uniquement toohello IoT hub de périphérique identités tooenable un accès sécurisé. Il stocke toouse ID et les clés de périphérique en tant qu’informations d’identification de sécurité et d’un indicateur activée/désactivée que vous pouvez utiliser l’accès toodisable pour un périphérique. Si votre application doit toostore autres métadonnées spécifiques au périphérique, elle doit utiliser un magasin spécifique à l’application. Pour plus d’informations, consultez hello [guide du développeur IoT Hub][lnk-devguide-identity].
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a>Recevoir des messages appareil-à-cloud
Dans cette section, vous créez une application console Node.js qui lit les messages appareil-à-cloud à partir d’IoT Hub. Un hub IoT expose un [concentrateurs d’événements][lnk-event-hubs-overview]-point de terminaison compatible tooenable vous tooread les messages appareil-à-cloud. tookeep les choses simples, ce didacticiel crée un lecteur de base qui n’est pas approprié pour un déploiement d’un débit élevé. Hello [traiter les messages appareil-à-cloud] [ lnk-process-d2c-tutorial] didacticiel vous montre comment les messages tooprocess appareil-à-cloud à grande échelle. Hello [prise en main les concentrateurs d’événements] [ lnk-eventhubs-tutorial] didacticiel fournit des informations supplémentaires sur le tooprocess des messages à partir de concentrateurs d’événements et est applicable toohello points de terminaison de Hub IoT Hub événement compatible.

> [!NOTE]
> Hello point de terminaison de Hub d’événements compatibles pour la lecture des messages appareil-à-cloud toujours utilise le protocole AMQP hello.
> 
> 

1. Créez un dossier vide appelé **readdevicetocloudmessages**. Bonjour **readdevicetocloudmessages** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante. Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **readdevicetocloudmessages** dossier, exécutez hello suivant commande tooinstall hello **concentrateurs d’événements azure** package :
   
    ```
    npm install azure-event-hubs --save
    ```
3. À l’aide d’un éditeur de texte, créez un **ReadDeviceToCloudMessages.js** fichier Bonjour **readdevicetocloudmessages** dossier.
4. Ajoutez hello suivant `require` instructions au hello démarrent Hello **ReadDeviceToCloudMessages.js** fichier :
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. Ajouter hello après la déclaration de variable et remplacer la valeur d’espace réservé de hello par hello chaîne de connexion de IoT Hub pour votre concentrateur :
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. Ajoutez hello suivant deux fonctions de la console de sortie toohello impression :
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. Ajouter hello suivant hello toocreate de code **EventHubClient**, ouvrez hello connexion tooyour IoT Hub et créer un récepteur pour chaque partition. Cette application utilise un filtre lorsqu’il crée un récepteur afin que hello récepteur lit uniquement les messages envoyés tooIoT Hub après que le récepteur de hello commence à s’exécuter. Ce filtre est utile dans un environnement de test afin de voir simplement hello ensemble actuel de messages. Dans un environnement de production, votre code doit Assurez-vous qu’elle traite tous les messages de type hello. Pour plus d’informations, consultez hello [comment tooprocess les messages appareil-à-cloud IoT Hub] [ lnk-process-d2c-tutorial] didacticiel :
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. Enregistrez et fermez hello **ReadDeviceToCloudMessages.js** fichier.

## <a name="create-a-simulated-device-app"></a>Création d’une application de périphérique simulé
Dans cette section, vous créez une application console Node.js qui simule un appareil qui envoie l’IoT hub tooan de messages appareil-à-cloud.

1. Créez un dossier vide appelé **simulateddevice**. Bonjour **simulateddevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante. Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **simulateddevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** package SDK de l’appareil et **azure-iot-périphérique-mqtt**package :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. À l’aide d’un éditeur de texte, créez un **SimulatedDevice.js** fichier Bonjour **simulateddevice** dossier.
4. Ajoutez hello suivant `require` instructions au hello démarrent Hello **SimulatedDevice.js** fichier :
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. Ajouter un **connectionString** variable et l’utiliser toocreate un **Client** instance. Remplacez **{youriothostname}** avec nom hello de hub IoT de hello, vous avez créé hello *créez un IoT Hub* section. Remplacez **{yourdevicekey}** avec la valeur de clé de périphérique hello générées dans hello *créer une identité d’appareil* section :
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. Ajoutez hello suivant sortie toodisplay de fonction à partir de l’application hello :
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Créer un rappel et utiliser hello **setInterval** fonction toosend un IoT hub de message tooyour chaque seconde :
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
        // Create a message and send it toohello IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
8. Ouvrez hello connexion tooyour IoT Hub et démarrer l’envoi de messages :
   
    ```
    client.open(connectCallback);
    ```
9. Enregistrez et fermez hello **SimulatedDevice.js** fichier.

> [!NOTE]
> tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].
> 
> 

## <a name="run-hello-apps"></a>Exécuter des applications de hello
Vous êtes maintenant prêt toorun hello applications.

1. À l’invite de commande Bonjour **readdevicetocloudmessages** dossier, exécutez hello suivant toobegin commande analyse votre IoT hub :
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Messages de l’appareil-à-cloud Node.js IoT Hub service application toomonitor][7]
2. À l’invite de commande Bonjour **simulateddevice** dossier, exécutez hello suivant toobegin commande envoi tooyour IoT hub de télémétrie des données :
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Messages de l’appareil-à-cloud Node.js IoT Hub appareil application toosend][8]
3. Hello **utilisation** vignette Bonjour [portail Azure] [ lnk-portal] affiche hello le nombre de messages envoyés toohello IoT hub :
   
    ![Azure portail d’utilisation vignette affichage du nombre de messages envoyés tooIoT Hub][43]

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub. Vous avez utilisé ce périphérique identité tooenable hello simulée appareil application toosend messages appareil-à-cloud toohello hub IoT. Vous avez créé également une application qui affiche les messages hello reçus par IoT hub de hello. 

toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :

* [Connexion de votre appareil][lnk-connect-device]
* [Prise en main de la gestion d’appareils][lnk-device-management]
* [Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Découvrir l’architecture Azure IoT Edge sur Linux)

toolearn tooextend vos messages IoT solution et des processus de périphérique dans le cloud à grande échelle, voir hello [traiter les messages appareil-à-cloud] [ lnk-process-d2c-tutorial] didacticiel.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
