---
title: "Se connecter Arduino tooAzure IoT - leçon 1 : déploiement d’une application | Documents Microsoft"
description: "Cloner hello exemple Arduino d’application à partir de GitHub et exécutez gulp toodeploy cette tooyour application Adafruit estompe M0 WiFi. Cet exemple d’application clignote hello GPIO"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: projets de led arduino, clignotement de led arduino, code de clignotement de led arduino, programme de clignotement arduino, exemple de clignotement arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Créer et déployer des applications de clignotement hello
## <a name="what-you-will-do"></a>Procédure à suivre
Cloner hello exemple Arduino d’application à partir de GitHub et utiliser hello gulp outil toodeploy hello exemple application tooyour Adafruit estompe M0 Wi-Fi Arduino tableau. application d’exemple Hello hello clignote GPIO n° 13 sur barod LED toutes les deux secondes.

Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting-page].

## <a name="what-you-will-learn"></a>Contenu
* Comment toodeploy et exécution hello exemple d’application dans votre tableau de Arduino.

## <a name="what-you-need"></a>Ce dont vous avez besoin
Vous devez avoir correctement terminé hello opérations suivantes :

* [Configuration de votre appareil][configure-your-device]
* [Obtenir les outils de hello][get-the-tools]

## <a name="open-hello-sample-application"></a>Exemple d’application hello ouvert
tooopen hello exemple d’application, procédez comme suit :

1. Clonez le dépôt d’exemples hello à partir de GitHub en exécutant hello de commande suivante :

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. Ouvrir l’exemple d’application hello dans Visual Studio Code par hello suivant les commandes en cours d’exécution :

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Structure du référentiel][repo-structure]

Hello `app.ino` fichier Bonjour `app` sous-dossier est le fichier de source de la clé de hello qui contient hello code toocontrol hello DEL.

### <a name="install-application-dependencies"></a>Installation des dépendances de l’application
Installer les bibliothèques hello et autres modules que vous avez besoin pour l’application d’exemple hello en exécutant hello commande suivante :

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Configurer la connexion du périphérique hello
tooconfigure hello connexion du périphérique, procédez comme suit :

1. Obtenir le port série de hello du périphérique hello avec cli de découverte de périphérique hello :

   ```bash
   devdisco list --usb
   ```

   Vous devez voir une sortie similaire toohello suivant et trouver hello usb port COM de votre carte Arduino : ![la détection des périphériques][device-discovery]

2. Les fichiers ouverts hello `config.json` hello du dossier de la leçon et ajouter la valeur hello hello trouvé le numéro de port COM :

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > Pour le port COM de hello, sur la plateforme Windows, d’un format de hello `COM1, COM2, ...`. Sur macOS ou Ubuntu, il commence par `/dev/`.

## <a name="deploy-and-run-hello-sample-application"></a>Déployer et exécuter l’exemple d’application hello
### <a name="install-hello-required-tools-for-your-arduino-board"></a>Installer les outils de hello requis pour votre carte mère Arduino

Installer hello Kit de développement logiciel Azure IoT Hub pour votre carte mère Arduino en exécutant hello de commande suivante :

```bash
gulp install-tools
```

Cette tâche peut prendre un toocomplete beaucoup de temps, en fonction de votre connexion réseau.

> [!NOTE]
> Veuillez quitter hello instance Arduino IDE en cours d’exécution lors de l’exécution des tâches de gulp : `install-tools`, `run`.

### <a name="deploy-and-run-hello-sample-app"></a>Déployer et exécuter l’exemple d’application hello
Déployer et exécuter l’exemple d’application hello en exécutant hello de commande suivante :

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a>Vérifiez que hello application fonctionne
Si vous ne voyez pas hello LED clignote, consultez hello [guide de dépannage] [ troubleshooting-page] des problèmes de toocommon solutions.

![LED clignotante][led-blinking]

## <a name="summary"></a>Résumé
Vous avez installé des hello requis outils toowork avec votre carte mère Arduino et déployé un Bonjour exemple application tooyour Arduino tableau tooblink DEL. Vous pouvez désormais créer, déployer et exécuter un autre exemple d’application qui se connecte à votre tooAzure de carte Arduino toosend d’IoT Hub et recevoir des messages.

## <a name="next-steps"></a>Étapes suivantes
[Obtenir des outils Azure hello][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md