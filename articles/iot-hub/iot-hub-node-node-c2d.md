---
title: "messages aaaCloud sur l’appareil avec Azure IoT Hub (nœud) | Documents Microsoft"
description: "Comment toosend cloud-à-appareil messages appareil tooa à partir d’un hub IoT d’Azure à l’aide de kits de développement IoT hello Azure pour Node.js. Modifier une application appareil simulé tooreceive les messages cloud-à-appareil et de modifier une application de serveur principal toosend hello cloud-à-appareil les messages."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 1ccae0cada52193c2abb91504c086cac226e93da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a>Envoi de messages cloud à appareil avec IoT Hub (Node)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Introduction
Azure IoT Hub est un service entièrement géré qui permet d’autoriser des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution. Hello [prise en main IoT Hub] didacticiel montre comment toocreate un IoT hub, configurer une identité d’appareil qu’il contient et code d’une application d’appareil simulé qui envoie des messages de l’appareil-à-cloud.

Ce didacticiel s’appuie sur l’article [prise en main IoT Hub]. Cette rubrique vous explique les procédures suivantes :

* À partir de votre solution back-end, envoyer des messages cloud-à-appareil tooa seule unité via IoT Hub.
* Recevez des messages cloud-à-appareil sur un appareil.
* À partir de votre solution back-end demande l’accusé de réception (*commentaires*) pour tooa appareil les messages envoyés à partir de IoT Hub.

Vous trouverez plus d’informations sur les messages cloud-à-appareil Bonjour [guide du développeur IoT Hub][IoT Hub developer guide - C2D].

À la fin de hello de ce didacticiel, vous exécutez deux applications de console Node.js :

* **SimulatedDevice**, une version modifiée de l’application hello créée dans [prise en main IoT Hub], qui se connecte tooyour IoT hub et reçoit des messages cloud-à-appareil.
* **SendCloudToDeviceMessage**, qui envoie une application d’appareil simulé toohello cloud-à-appareil message via IoT Hub et reçoit ensuite son accusé de réception.

> [!NOTE]
> IoT Hub offre la prise en charge de plusieurs plateformes d’appareils et plusieurs langages (notamment C, Java et Javascript) par le biais des Kits de développement logiciel (SDK) d’appareils Azure IoT. Pour obtenir des instructions sur tooconnect du votre appareil toothis didacticiel code et généralement tooAzure IoT Hub, voir hello [centre de développement Azure IoT].
> 
> 

toocomplete ce didacticiel, vous devez hello suivant :

* Node.js version 0.10.x ou ultérieure.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

## <a name="receive-messages-in-hello-simulated-device-app"></a>Recevoir des messages dans une application d’appareil simulé hello
Dans cette section, vous modifiez l’application d’appareil simulé hello vous avez créé dans [prise en main IoT Hub] tooreceive les messages cloud-à-appareil à partir du hub IoT de hello.

1. À l’aide d’un éditeur de texte, d’ouvrir le fichier de SimulatedDevice.js hello.
2. Modifier hello **connectCallback** fonction toohandle les messages envoyés à partir de IoT Hub. Dans cet exemple, les appareils hello appelant toujours hello **complète** toonotify IoT Hub qu’il a traité le message d’appel de fonction. La nouvelle version de hello **connectCallback** fonction ressemble à hello suivant extrait de code :
   
    ```javascript
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
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
   
   > [!NOTE]
   > Si vous utilisez HTTP au lieu de MQTT ou AMQP comme couche de transport hello, hello **DeviceClient** instance vérifie les messages à partir du IoT Hub rarement (inférieur à 25 minutes). Pour plus d’informations sur les différences de hello entre la prise en charge MQTT, AMQP et HTTP et de limitation IoT Hub, consultez hello [guide du développeur IoT Hub][IoT Hub developer guide - C2D].
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a>Envoi d’un message cloud vers appareil
Dans cette section, vous créez une application console Node.js qui envoie des messages cloud-à-appareil toohello appareil simulé application. Vous devez hello ID de périphérique périphérique hello vous avez ajouté dans hello [prise en main IoT Hub] didacticiel. Vous devez également hello chaîne de connexion IoT Hub pour votre concentrateur que vous pouvez trouver Bonjour [portail Azure].

1. Créez un dossier vide appelé **sendcloudtodevicemessage**. Bonjour **sendcloudtodevicemessage** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante. Acceptez les valeurs par défaut hello :
   
    ```shell
    npm init
    ```
2. Votre invite de commandes Bonjour **sendcloudtodevicemessage** dossier, exécutez hello suivant commande tooinstall hello **azure-iothub** package :
   
    ```shell
    npm install azure-iothub --save
    ```
3. À l’aide d’un éditeur de texte, créez un **SendCloudToDeviceMessage.js** fichier Bonjour **sendcloudtodevicemessage** dossier.
4. Ajoutez hello suivant `require` instructions au hello démarrent Hello **SendCloudToDeviceMessage.js** fichier :
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. Ajouter hello suivant code trop**SendCloudToDeviceMessage.js** fichier. Remplacer la valeur d’espace réservé hello « {iot hub chaîne de connexion} » avec hello chaîne de connexion de IoT Hub hub hello vous avez créé dans hello de [prise en main IoT Hub] didacticiel. Remplacez espace réservé de hello « {id d’appareil} » avec l’ID de périphérique hello du périphérique hello vous avez ajouté dans hello [prise en main IoT Hub] didacticiel :
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. Ajoutez hello suivant fonction tooprint résultats toohello console Opérateur :
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Ajoutez hello suivant console toohello de fonction tooprint remise commentaires messages :
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. Ajoutez suivante de hello toosend un dispositif de tooyour de messages de code et gérer le message de commentaires de hello lors de l’appareil de hello accuse réception de message de type hello cloud sur l’appareil :
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud toodevice message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. Enregistrez et fermez le fichier **SendCloudToDeviceMessage.js** .

## <a name="run-hello-applications"></a>Exécuter des applications de hello
Vous êtes maintenant prêt toorun les applications hello.

1. Invite de commandes hello Bonjour **simulateddevice** dossier, exécutez hello commande toosend télémétrie tooIoT Hub et toolisten pour les messages cloud-à-appareil :
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Exécutez l’application d’appareil simulé hello][img-simulated-device]
2. À l’invite de commande Bonjour **sendcloudtodevicemessage** dossier, exécutez hello suivant commande toosend un message cloud-à-appareil et attendez les commentaires d’accusé de réception hello :
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Exécutez hello application toosend hello cloud-à-appareil commande][img-send-command]
   
   > [!NOTE]
   > Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, d’interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires].
   > 
   > 

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment toosend et recevoir des messages cloud-à-appareil. 

exemples de toosee des solutions de bout en bout complets qui utilisent l’IoT Hub, consultez [Azure IoT Suite].

toolearn savoir plus sur le développement de solutions avec IoT Hub, consultez hello [guide du développeur IoT Hub].

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

[prise en main IoT Hub]: iot-hub-node-node-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[guide du développeur IoT Hub]: iot-hub-devguide.md
[centre de développement Azure IoT]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[gestion des pannes temporaires]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[portail Azure]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
