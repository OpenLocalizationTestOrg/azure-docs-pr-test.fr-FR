---
title: "Connect Raspberry PI (C) tooAzure IoT - leçon 4 : Cloud-à-appareil | Documents Microsoft"
description: "Un exemple d’application s’exécute sur Pi et surveille les messages entrants à partir de votre IoT Hub. Une nouvelle tâche gulp envoie des messages tooPi à partir de votre hello tooblink du hub IoT DEL."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "toodevice cloud, le message à partir du cloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5596bf3a83c21f2bd54b2f83e2a8fdad7a608b94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Exécuter un tooreceive d’application exemple messages cloud-à-appareil
Dans cet article, vous déployez un exemple d’application sur Raspberry Pi 3. exemple d’application Hello surveille les messages entrants à partir de votre hub IoT. Aussi, vous exécutez une tâche de gulp sur votre tooPi de messages toosend ordinateur à partir de votre hub IoT. Lors de l’application d’exemple hello reçoit des messages hello, il clignote hello DEL. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-do"></a>Procédure à suivre
* Connectez le hub IoT tooyour hello exemple application.
* Déployer et exécuter l’exemple d’application hello.
* Envoyer des messages à partir de votre hello dans IoT hub tooPi tooblink DEL.

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :
* Comment les messages entrants de toomonitor à partir de votre hub IoT.
* Comment les messages à partir de votre tooPi de hub IoT toosend cloud-à-appareil.

## <a name="what-you-need"></a>Ce dont vous avez besoin
* Raspberry Pi 3, configuré pour utilisation. toolearn tooset de Pi, voir [configurer votre périphérique](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).
* Un IoT Hub créé dans le cadre de votre abonnement Azure. toolearn comment toocreate votre IoT hub, consultez [créez votre hub IoT et inscrire framboises Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Connecter le hub IoT tooyour hello exemple application
1. Assurez-vous que vous êtes dans le dossier de dépôt hello `iot-hub-c-raspberrypi-getting-started`. Ouvrir l’exemple d’application hello dans Visual Studio Code par hello suivant les commandes en cours d’exécution :

   ```bash
   cd Lesson4
   code .
   ```

   Hello d’avis `app.c` fichier Bonjour `app` sous-dossier. Hello `app.c` fichier est le fichier de source de la clé de hello qui contient les messages entrants toomonitor code hello à partir du hub IoT de hello. Hello `blinkLED` fonction clignote hello DEL.

   ![Structure de référentiel dans l’exemple d’application hello](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :

   ```bash
   npm install
   gulp init
   ```

   Si vous avez terminé les étapes de hello dans [créer un compte d’application et de stockage Azure fonction](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) sur cet ordinateur, toutes les configurations de hello sont héritées, vous pouvez sauter toostep toohello de tâche déploiement et l’application d’exemple hello en cours d’exécution. Si vous avez terminé les étapes de hello dans [créer un compte d’application et de stockage Azure fonction](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) sur un autre ordinateur, vous avez besoin des espaces réservés de hello tooreplace Bonjour `config-raspberrypi.json` fichier. Hello `config-raspberrypi.json` fichier se trouve dans le sous-dossier hello de votre dossier de base.

   ![Contenu du fichier de configuration-raspberrypi.json hello](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* Remplacez **[nom d’hôte du périphérique ou adresse IP]** avec Pi IP adresse ou nom d’hôte que vous obtenez en exécutant hello `devdisco list --eth` commande.
* Remplacez **[chaîne de connexion de périphérique IoT]** avec la chaîne de connexion de périphérique hello que vous obtenez en exécutant hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` commande.
* Remplacez **[chaîne de connexion de hub IoT]** avec hello chaîne de connexion de hub IoT que vous obtenez en exécutant hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` commande.

> [!NOTE]
> Exécutez également **gulp install-tools**, si vous ne l’avez pas fait dans la leçon 1.

## <a name="deploy-and-run-hello-sample-application"></a>Déployer et exécuter l’exemple d’application hello
Déployer et exécuter l’exemple d’application hello sur Pi en exécutant hello suivant les commandes :

```
gulp deploy && gulp run
```

exécution de la commande Hello gulp hello tâche d’installer les outils de tout d’abord. Il déploie ensuite tooPi d’application exemple hello. Enfin, elle s’exécute l’application hello sur Pi et une tâche distincte sur votre hôte ordinateur toosend 20 blink messages tooPi votre hub IoT.

Après l’exécution de l’exemple d’application hello, il commence à écouter toomessages à partir de votre hub IoT. Pendant ce temps, tâche de gulp hello envoie plusieurs messages « clignoter » à partir de votre tooPi de hub IoT. Pour chaque message blink qui reçoit de Pi, exemple d’application hello appelle hello `blinkLED` hello tooblink de fonction DEL.

Vous devez voir clignotement de LED hello toutes les deux secondes comme hello gulp la tâche envoie des messages à partir de votre tooPi de hub IoT 20. Hello dernier un est un message « arrêter » qui arrête l’application hello de s’exécuter.

![Exemple d’application avec la commande gulp et les messages de clignotement](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a>Résumé
Vous avez correctement envoyé des messages à partir de votre hello dans IoT hub tooPi tooblink DEL. la tâche suivante Hello est facultative : modifier hello et désactiver le comportement de hello DEL.

## <a name="next-steps"></a>Étapes suivantes
[Modifier hello et désactiver le comportement de hello DEL](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
