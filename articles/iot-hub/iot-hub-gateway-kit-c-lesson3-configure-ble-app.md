---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 3 : Exécuter un exemple d’application | Microsoft Docs"
description: "Exécutez BLE exemples application tooreceive de données à partir de SensorTag d’activer et de votre hub IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "application de tableau, capteur analyser l’application, collecte de données de capteur, données depuis les capteurs, toocloud de données de capteur"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a>Configurer et exécuter l’exemple d’application BLE

## <a name="what-you-will-do"></a>Procédure à suivre

- Dépôt d’exemples hello clone. 
- Configurer une connectivité hello entre SensorTag et NUC d’Intel. 
- Utilisez hello CLI d’Azure tooget votre IoT hub et les informations de SensorTag pour un exemple d’application BLE (Bluetooth faible consommation d’énergie). Configurer et exécuter hello BLE exemple d’application. 

Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu

Cet article portera sur les éléments suivants :

- Comment tooconfigure et exécution hello BLE exemple d’application.

## <a name="what-you-need"></a>Ce dont vous avez besoin

Vous devez avoir accompli les étapes suivantes :

- [Créer un IoT Hub et inscrire SensorTag](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Cloner l’ordinateur hôte toohello hello exemple référentiel

dépôt d’exemples tooclone hello, procédez comme suit sur l’ordinateur hôte hello :

1. Ouvrez une invite de commande dans Windows ou ouvrez une fenêtre de terminal dans macOS ou Ubuntu.
2. Exécutez hello suivant de commandes :

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a>Configurer une connectivité hello entre SensorTag et Intel NUC

tooset la connectivité de hello, procédez comme suit sur l’ordinateur hôte hello :

1. Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. Ouvrez `config-gateway.json` dans le Code de Visual Studio en exécutant hello de commande suivante :

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. Recherchez hello ligne de code suivante et remplacez `[device hostname or IP address]` avec hello IP adresse nom d’hôte ou NUC d’Intel.
   ![capture d’écran de la passerelle de configuration](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

4. Installer les outils d’assistance sur Intel NUC en exécutant hello de commande suivante :

   ```bash
   gulp install-tools
   ```

5. SensorTag sous tension en appuyant sur bouton d’alimentation hello hello illustration suivante et hello que vert clignote.

   ![activer le SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. SensorTag de périphériques de numérisation en exécutant hello suivant de commandes :

   ```bash
   gulp discover-sensortag
   ```

7. Tester la connectivité de hello entre hello SensorTag et Intel NUC en exécutant hello de commande suivante :

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   Remplacez `{mac address}` par hello adresse MAC que vous avez obtenu à l’étape précédente de hello.

## <a name="get-hello-connection-string-of-sensortag"></a>Obtenir la chaîne de connexion hello de SensorTag

hello tooget chaîne de connexion Azure IoT hub de SensorTag, exécutez hello commande sur l’ordinateur hôte hello suivante :

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`est le nom de hub IoT hello que vous avez utilisé. Utilisez iot-passerelle en tant que valeur hello `{resource group name}` et utiliser mydevice en tant que valeur hello `{device id}` si vous n’avez pas modifier la valeur hello dans la leçon 2.

## <a name="configure-hello-ble-sample-application"></a>Configurez hello BLE exemple d’application

tooconfigure et exécution hello exemple d’application BLE, procédez comme suit sur l’ordinateur hôte hello :

1. Ouvrez `config-sensortag.json` dans le Code de Visual Studio en exécutant hello de commande suivante :

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![capture d’écran de configuration sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. Rendre hello suivant des remplacements dans le code hello :
   - Remplacez `[IoT hub name]` avec le nom de hub IoT hello que vous avez utilisé.
   - Remplacez `[IoT device connection string]` avec la chaîne de connexion hello de SensorTag que vous avez obtenu.
   - Remplacez `[device_mac_address]` par hello adresse MAC de hello SensorTag que vous avez obtenu.

3. Exécutez hello BLE exemple d’application.

   toorun hello exemple d’application BLE, procédez comme suit sur l’ordinateur hôte hello :

   1. Activez le SensorTag.

   2. Déployer et exécuter des application d’exemple hello BLE sur Intel NUC en exécutant hello de commande suivante :
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a>Vérifiez que hello BLE exemple d’application fonctionne

Vous devez maintenant voir une sortie semblable à hello suivante :

![Résultats de l’exemple d’application BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

exemple d’application Hello conserve la collecte de données de la température et envoyé tooyour IoT hub. exemple d’application Hello se termine automatiquement après l’envoi de 40 secondes.

## <a name="summary"></a>Résumé

Vous avez correctement défini la connectivité hello entre SensorTag et Intel NUC et exécuter un exemple d’application BLE qui collecte et envoie des données à partir de SensorTag tooyour IoT hub. Vous êtes prêt toolearn comment tooverify votre hub IoT a reçu hello des données.

## <a name="next-steps"></a>Étapes suivantes
[Lire des messages à partir de votre IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)