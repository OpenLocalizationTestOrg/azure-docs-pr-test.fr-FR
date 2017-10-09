---
title: "Connect Arduino (C) tooAzure IoT - leçon 3 : exécuter l’exemple | Documents Microsoft"
description: "Déployer et exécuter un tooAdafruit d’application exemple estompe M0 Wi-Fi qui envoie l’IoT hub tooyour de messages et clignote hello DEL."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "service de cloud IOT, arduino envoyer des données toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Exécuter un toosend d’application exemple messages appareil-à-cloud
## <a name="what-you-will-do"></a>Procédure à suivre
Cet article vous explique comment toodeploy et exécuter un exemple d’application sur votre Arduino de Wi-Fi Adafruit estompe M0 board qui envoie les messages tooyour IoT hub.

Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].

## <a name="what-you-will-learn"></a>Contenu
Vous allez apprendre comment toouse hello gulp outil toodeploy et exécuter l’exemple d’application de Arduino hello dans votre tableau de Arduino.

## <a name="what-you-need"></a>Ce dont vous avez besoin
* Avant de commencer cette tâche, vous devez avoir terminé avec succès [créer une application de la fonction Azure et un stockage compte tooprocess et magasin IoT hub messages][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obtenir vos chaînes de connexion d’IoT Hub et d’appareil
Hello la chaîne de connexion de périphérique est tooconnect utilisé votre concentrateur de IoT tooyour Arduino du tableau. chaîne de connexion de hub IoT Hello est tooconnect utilisé votre identité d’appareil IoT hub toohello qui représente votre Arduino board dans le hub IoT de hello.

* Liste de tous vos hubs IoT dans votre groupe de ressources en exécutant hello suivant commande CLI d’Azure :

```bash
az iot hub list -g iot-sample --query [].name
```

Utilisez `iot-sample` en tant que valeur hello `{resource group name}` si vous n’avez modifié la valeur de hello.

* Obtenir la chaîne de connexion de hub IoT hello en exécutant hello suivant commande CLI d’Azure :

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`est le nom hello que vous avez spécifié lorsque vous créez votre hub IoT et inscrit votre tableau Arduino.

* Obtenir la chaîne de connexion de périphérique de hello en exécutant hello de commande suivante :

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

Utilisez `mym0wifi` en tant que valeur hello `{device id}` si vous n’avez modifié la valeur de hello.
## <a name="configure-hello-device-connection"></a>Configurer la connexion du périphérique hello
tooconfigure hello connexion du périphérique, procédez comme suit :

1. Obtenir le port série de hello du périphérique hello avec cli de découverte de périphérique hello :

   ```bash
   devdisco list --usb
   ```

   Vous devez voir une sortie similaire toohello suivant et trouver hello usb port COM de votre carte Arduino :

   ![Découverte de l’appareil][device-discovery]

2. Les fichiers ouverts hello `config.json` hello du dossier de la leçon et ajouter la valeur hello hello trouvé le numéro de port COM :

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > Pour le port COM de hello, sur la plateforme Windows, d’un format de hello `COM1, COM2, ...`. Sur macOS ou Ubuntu, il commence par `/dev/`.

3. Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. Fichier de configuration de périphérique ouvert hello `config-arduino.json` dans le Code de Visual Studio en exécutant hello de commande suivante :

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. Rendre hello suivant remplacements Bonjour `config-arduino.json` fichier :

   * Remplacez **[Wi-Fi SSID]** avec votre SSID Wi-Fi qui connectés toohello Internet.
   * Remplacez **[Wi-Fi password]** par votre mot de passe Wi-Fi. Supprimez la chaîne de hello si votre Wi-Fi ne nécessite pas un mot de passe.
   * Remplacez **[chaîne de connexion de périphérique IoT]** avec hello `device connection string` obtenues.
   * Remplacez **[chaîne de connexion de hub IoT]** avec hello `iot hub connection string` obtenues.

   > [!NOTE]
   > Vous n’avez pas besoin de `azure_storage_connection_string` dans cet article. Gardez-le tel quel.

## <a name="deploy-and-run-hello-sample-application"></a>Déployer et exécuter l’exemple d’application hello
Déployer et exécuter des application d’exemple hello sur votre carte mère Arduino en exécutant hello de commande suivante :

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> Hello par défaut gulp tâche s’exécute `install-tools` et `run` tâches séquentiellement. Lorsque vous [hello blink application déployée][deployed-the-blink-app], vous avez exécuté ces tâches séparément.

## <a name="verify-that-hello-sample-application-works"></a>Vérifiez que hello exemple application fonctionne
Vous devez voir hello GPIO #0 intégrée LED clignote toutes les deux secondes. Chaque fois que hello LED clignote, exemple d’application hello envoie un hub IoT de tooyour message et vérifie que ce message de type hello a été envoyé avec succès tooyour IoT hub. En outre, chaque message reçu par IoT hub de hello est imprimé dans la fenêtre de console hello. exemple d’application Hello se termine automatiquement après l’envoi des messages de 20.

![Exemple d’application avec des messages envoyés et reçus][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Résumé
Vous avez déployé et exécuter hello nouvelle blink exemple d’application sur votre IoT hub tooyour de messages appareil-à-cloud toosend Arduino du tableau. Vous surveillez maintenant vos messages qu’ils sont écrits de compte de stockage toohello.

## <a name="next-steps"></a>Étapes suivantes
[Lecture des messages conservés dans le stockage Azure][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md