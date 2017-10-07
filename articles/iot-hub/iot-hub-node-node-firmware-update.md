---
title: "mise à jour de microprogramme aaaDevice avec Azure IoT Hub (nœud) | Documents Microsoft"
description: "Comment mettre à jour toouse la gestion des appareils sur Azure IoT Hub tooinitiate un microprogramme de l’appareil. Vous utilisez hello Azure IoT SDK pour Node.js tooimplement une application d’appareil simulé et une application de service qui déclenche la mise à jour du microprogramme hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a>Utiliser la gestion de périphérique tooinitiate une mise à jour du microprogramme de périphérique (nœud)
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Introduction
Bonjour [prise en main la gestion des appareils] [ lnk-dm-getstarted] didacticiel, vous avez vu comment toouse hello [double de l’appareil] [ lnk-devtwin] et [directe méthodes] [ lnk-c2dmethod] tooremotely de primitives redémarrer un appareil. Ce didacticiel utilise hello mêmes primitives IoT Hub et fournit des conseils et vous montre comment toodo un bout en bout simulée mise à jour du microprogramme.  Ce modèle est utilisé dans l’implémentation de mise à jour du microprogramme hello pour exemple de périphérique Intel Edison hello.

Ce didacticiel vous explique les procédures suivantes :

* Créer une application de console Node.js qui appelle la méthode directe de hello firmwareUpdate dans l’application d’appareil simulé hello via votre hub IoT.
* Créez un appareil simulé qui implémente une méthode directe **firmwareUpdate**. Cette méthode lance un processus en plusieurs étapes qui attend l’image de microprogramme toodownload hello, télécharge l’image de microprogramme hello et enfin applique image de microprogramme hello. Lors de chaque étape de mise à jour hello, hello périphérique utilise hello signalée tooreport de propriétés sur la progression.

À la fin de hello de ce didacticiel, vous avez deux applications de console Node.js :

**dmpatterns_fwupdate_service.js**, qui appelle une méthode directe dans l’application d’appareil simulé hello, réponse de hello s’affiche et périodiquement (chaque 500 ms) hello affiche mis à jour signalés propriétés.

**dmpatterns_fwupdate_device.js**, qui connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment, reçoit une méthode directe firmwareUpdate, s’exécute via un toosimulate plusieurs États de processus pour une mise à jour de microprogramme, y compris : en attente de hello image de téléchargement, télécharger la nouvelle image de hello et enfin application de l’image de hello.

toocomplete ce didacticiel, vous devez hello suivant :

* Node.js version 0.12.x ou version ultérieure. <br/>  [Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Node.js pour ce didacticiel sur Windows ou Linux.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

Suivez hello [prise en main la gestion des appareils](iot-hub-node-node-device-management-get-started.md) article toocreate votre IoT hub et obtenir votre chaîne de connexion de IoT Hub.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Déclencher une mise à jour de microprogramme à distance sur l’appareil hello à l’aide d’une méthode directe
Dans cette section, vous créez une application console Node.js qui lance une mise à jour de microprogramme à distance sur un appareil. application Hello utilise une mise à jour de méthode directe tooinitiate hello et utilise appareil double requêtes tooperiodically obtenir l’état de hello de mise à jour du microprogramme active hello.

1. Créez un dossier vide nommé **triggerfwupdateondevice**.  Bonjour **triggerfwupdateondevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.  Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **triggerfwupdateondevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-concentrateur** et **azure-iot-périphérique-mqtt** périphérique Packages du Kit de développement logiciel :
   
    ```
    npm install azure-iothub --save
    ```
3. À l’aide d’un éditeur de texte, créez un **dmpatterns_getstarted_service.js** fichier Bonjour **triggerfwupdateondevice** dossier.
4. Ajouter des instructions au début de hello Hello suivant de hello « exiger » **dmpatterns_getstarted_service.js** fichier :
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Ajouter hello après les déclarations de variable et remplacez les valeurs d’espace réservé hello :
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. Ajouter suivant de hello fonction toofind et affiche la valeur hello hello firmwareUpdate a signalé de propriété.
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. Ajoutez hello suivant fonction tooinvoke hello firmwareUpdate méthode tooreboot hello équipement :
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. Enfin, suivant de hello Ajouter fonction de séquence de mise à jour du microprogramme toocode toostart hello et démarrer régulièrement montrant hello signalé propriétés :
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. Enregistrez et fermez hello **dmpatterns_fwupdate_service.js** fichier.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Exécuter des applications de hello
Vous êtes maintenant prêt toorun hello applications.

1. Invite de commandes hello Bonjour **manageddevice** dossier, exécutez hello suivant toobegin de commande à l’écoute de méthode directe de redémarrage hello.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. Invite de commandes hello Bonjour **triggerfwupdateondevice** dossier, exécutez hello suivant à distance de commande tootrigger hello redémarrer et pour Bonjour appareil double toofind Bonjour redémarrez dernière heure de la requête.
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. Vous consultez hello appareil réponse toohello méthode directe dans la console hello.

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez utilisé un tootrigger méthode directe à une distance mise à jour de microprogramme sur un appareil et un hello utilisé signalé progression de hello toofollow propriétés de mise à jour du microprogramme hello.

toolearn tooextend votre méthode de planification et de solution IoT des appels sur plusieurs appareils, consultez hello [planification et les tâches de diffusion] [ lnk-tutorial-jobs] didacticiel.

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
