---
title: "Connect Arduino (C) tooAzure IoT - leçon 4 : Cloud-à-appareil | Documents Microsoft"
description: "Un exemple d’application s’exécute sur la carte Adafruit Feather M0 WiFi et surveille les messages entrants à partir de votre IoT Hub. Une nouvelle tâche gulp envoie des messages tooAdafruit estompe M0 WiFi à partir de votre hello tooblink du hub IoT DEL."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "contrôle de la led avec arduino à partir du web, contrôle de la led avec arduino via le web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Exécuter un tooreceive d’application exemple messages cloud-à-appareil
Dans cet article, vous déployez un exemple d’application sur votre carte Adafruit Feather M0 WiFi Arduino.

exemple d’application Hello surveille les messages entrants à partir de votre hub IoT. Aussi, vous exécutez une tâche de gulp sur votre ordinateur ordinateur toosend messages tooyour Arduino tableau à partir de votre hub IoT. Lors de l’application d’exemple hello reçoit des messages hello, il clignote hello DEL. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].

## <a name="what-you-will-do"></a>Procédure à suivre
* Connectez le hub IoT tooyour hello exemple application.
* Déployer et exécuter l’exemple d’application hello.
* Envoyer des messages à partir de votre hello IoT hub tooyour Arduino tableau tooblink DEL.

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :
* Comment les messages entrants de toomonitor à partir de votre hub IoT.
* Comment les messages à partir de votre tooyour de hub IoT Arduino tableau toosend cloud-à-appareil.

## <a name="what-you-need"></a>Ce dont vous avez besoin
* Votre carte Arduino, configurée et prête à l’utilisation. toolearn tooset de votre tableau Arduino, voir [configurer votre périphérique][configure-your-device].
* Un IoT Hub créé dans le cadre de votre abonnement Azure. toolearn comment toocreate votre IoT hub, consultez [créer votre Azure IoT Hub][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Connecter le hub IoT tooyour hello exemple application

1. Assurez-vous que vous êtes dans le dossier de dépôt hello `iot-hub-c-feather-m0-getting-started`.

   Ouvrir l’exemple d’application hello dans Visual Studio Code par hello suivant les commandes en cours d’exécution :

   ```bash
   cd Lesson4
   code .
   ```

   Hello d’avis `app.ino` fichier Bonjour `app` sous-dossier. Hello `app.ino` fichier est le fichier de source de la clé de hello qui contient les messages entrants toomonitor code hello à partir du hub IoT de hello. Hello `blinkLED` fonction clignote hello DEL.

   ![Structure de référentiel dans l’exemple d’application hello][repo-structure]

2. Obtenir le port série de hello du périphérique hello avec cli de découverte de périphérique hello :

   ```bash
   devdisco list --usb
   ```

   Vous devez voir une sortie similaire toohello suivant et trouver hello usb port COM de votre carte Arduino :

   ![Découverte de l’appareil][device-discovery]

3. Les fichiers ouverts hello `config.json` dans le dossier de leçon hello et valeur d’entrée hello hello trouvé le numéro de port COM :

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > Pour le port COM de hello, sur la plateforme Windows, d’un format de hello `COM1, COM2, ...`. Sur macOS ou Ubuntu, il commence par `/dev/`.

4. Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. Rendre hello suivant remplacements Bonjour `config-arduino.json` fichier :

   Si vous avez terminé les étapes de hello dans [créer un compte d’application et de stockage Azure fonction] [ create-an-azure-function-app-and-storage-account] sur cet ordinateur, toutes les configurations de hello sont héritées, vous pouvez sauter des tâches de toohello hello étape du déploiement et exemple d’application hello en cours d’exécution. Si vous avez terminé les étapes de hello dans [créer un compte d’application et de stockage Azure fonction] [ create-an-azure-function-app-and-storage-account] sur un autre ordinateur, vous avez besoin des espaces réservés de hello tooreplace Bonjour `config-arduino.json` fichier. Hello `config-arduino.json` fichier se trouve dans le sous-dossier hello de votre dossier de base.

   ![Contenu du fichier de configuration-arduino.json hello][config-arduino-json]

   * Remplacez **[Wi-Fi SSID]** avec votre SSID Wi-Fi qui connectés toohello Internet.
   * Remplacez **[Wi-Fi password]** par votre mot de passe Wi-Fi. Supprimez la chaîne de hello si votre Wi-Fi ne nécessite pas un mot de passe.
   * Remplacez **[chaîne de connexion de périphérique IoT]** avec la chaîne de connexion de périphérique hello que vous obtenez en exécutant hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` commande.
   * Remplacez **[chaîne de connexion de hub IoT]** avec hello chaîne de connexion de hub IoT que vous obtenez en exécutant hello `az iot hub show-connection-string --name {my hub name}` commande.

## <a name="deploy-and-run-hello-sample-application"></a>Déployer et exécuter l’exemple d’application hello
Déployer et exécuter des application d’exemple hello sur votre carte mère Arduino par hello suivant les commandes en cours d’exécution :

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

commande de gulp Hello déploie le tableau Arduino tooyour hello exemple application. Il exécute ensuite application hello sur votre carte mère Arduino et une tâche distincte sur votre hôte tooyour Arduino carte pour ordinateur toosend 20 blink messages à partir de votre hub IoT.

Après l’exécution de l’exemple d’application hello, il commence à écouter toomessages à partir de votre hub IoT. Pendant ce temps, tâche de gulp de hello envoie plusieurs messages « clignoter » à partir de votre tooyour de hub IoT Arduino carte. Pour chaque message blink hello carte reçoit, exemple d’application hello appelle hello `blinkLED` hello tooblink de fonction DEL.

Vous devez voir hello LED clignote toutes les deux secondes comme tâche de gulp hello envoie des messages de 20 à partir de votre tooyour de hub IoT Arduino carte. Hello dernier un est un message « arrêter » qui arrête l’application hello de s’exécuter.

![Exemple d’application avec la commande gulp et les messages de clignotement][sample-application]

## <a name="summary"></a>Résumé
Vous avez correctement envoyé des messages à partir de votre hello IoT hub tooyour Arduino tableau tooblink DEL. la tâche suivante Hello est facultative : modifier hello et désactiver le comportement de hello DEL.

## <a name="next-steps"></a>Étapes suivantes
[Modifier hello et désactiver le comportement de hello DEL][change-the-on-and-off-led-behavior]


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md