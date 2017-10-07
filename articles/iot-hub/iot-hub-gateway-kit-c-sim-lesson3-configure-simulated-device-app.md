---
title: "Appareil simulé et passerelle Azure IoT - Leçon 3 : Exécuter un exemple d’application | Microsoft Docs"
description: "Exécuter un appareil simulé exemple application toosend température tooyour IoT concentrateur de données"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "toocloud de données"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a>Configurer et exécuter un exemple d’application d’appareil simulé

## <a name="what-you-will-do"></a>Procédure à suivre

- Dépôt d’exemples hello clone.
- Utilisez hello CLI d’Azure tooget votre IoT hub et les informations d’unité logique pour un exemple d’application appareil simulé. Configurer et exécuter l’application d’exemple hello simulée appareil.

Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu

Cet article portera sur les éléments suivants :

- Comment tooconfigure et exécution hello simulés application d’exemple de périphérique.

## <a name="what-you-need"></a>Ce dont vous avez besoin

Vous devez avoir accompli avec succès les étapes

- [Créer un hub IoT et enregistrer votre appareil](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Cloner l’ordinateur hôte toohello hello exemple référentiel

dépôt d’exemples tooclone hello, procédez comme suit sur l’ordinateur hôte hello :

1. Ouvrez une invite de commande dans Windows ou ouvrez une fenêtre de terminal dans macOS ou Ubuntu.
2. Exécutez hello suivant de commandes :

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a>Configurer les appareil simulé hello et votre NUC

1. Fichier de configuration Open hello `config.json` dans le Code de Visual Studio en exécutant hello de commande suivante :

   ```bash
   code config.json
   ```

2. Remplacer `"has_sensortag": true` par `"has_sensortag": false`

   ![Configuration si vous n’avez pas d'appareil TI SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. Ouvrez `config-gateway.json` dans le Code de Visual Studio en exécutant hello de commande suivante :

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. Recherchez hello ligne de code suivante et remplacez `[device hostname or IP address]` avec le nom d’hôte ou adresse IP Hello Intel NUC.
   ![capture d’écran de la passerelle de configuration](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a>Obtenir la chaîne de connexion hello du périphérique logique IoT hub

hello tooget chaîne de connexion Azure IoT hub de votre unité logique, exécutez hello commande sur l’ordinateur hôte hello suivante :

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`est le nom de hub IoT hello que vous avez utilisé. Utilisez iot-passerelle en tant que valeur hello `{resource group name}` et utiliser mydevice en tant que valeur hello `{device id}` si vous n’avez pas modifier la valeur hello dans la leçon 2.

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a>Configurez hello simulée appareil cloud téléchargement exemple d’application

tooconfigure et exécution hello simulée appareil cloud télécharger l’exemple d’application, procédez comme suit sur l’ordinateur hôte hello :

1. Ouvrez `config-sensortag.json` dans le Code de Visual Studio en exécutant hello de commande suivante :

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![capture d’écran de configuration sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. Rendre hello suivant des remplacements dans le code hello :
   - Remplacez `[IoT hub name]` avec le nom de hub IoT hello.
   - Remplacez `[IoT device connection string]` avec chaîne de connexion hello de votre unité logique de hub IoT.

3. Exécutez l’application hello.

   Déployer et exécuter l’application hello en exécutant hello de commande suivante :

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a>Vérifiez le fonctionnement de l’application exemple hello

Vous devez maintenant voir la sortie hello suivante :

![résultat de l'exemple d'application d'appareil simulé](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

application Hello envoie la température données tooyour IoT hub, qui dure 40 secondes.

## <a name="summary"></a>Résumé

Vous avez correctement configuré et exécution hello simulée appareil cloud téléchargement exemple d’application qui envoie le concentrateur de données tooyour IoT avec appareil simulé.

## <a name="next-steps"></a>Étapes suivantes
[Lire des messages à partir de votre IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)