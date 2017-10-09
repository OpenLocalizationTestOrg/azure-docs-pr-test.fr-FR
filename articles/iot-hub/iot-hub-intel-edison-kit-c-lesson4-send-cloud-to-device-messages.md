---
title: "Connect Intel Edison (C) tooAzure IoT - leçon 4 : recevoir des messages | Documents Microsoft"
description: "Un exemple d’application s’exécute sur Edison et surveille les messages entrants à partir de votre IoT Hub. Une nouvelle tâche gulp envoie des messages tooEdison à partir de votre hello tooblink du hub IoT DEL."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "contrôle de la led avec arduino à partir du web, contrôle de la led avec arduino via le web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 820d38f3-d3b8-4249-9e2b-f1b9b771e62f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f0424506ff755e0b9514684787b37584d406d320
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Exécuter un tooreceive d’application exemple messages cloud-à-appareil
Dans cet article, vous déployez un exemple d’application sur Intel Edison. exemple d’application Hello surveille les messages entrants à partir de votre hub IoT. Aussi, vous exécutez une tâche de gulp sur votre tooEdison de messages toosend ordinateur à partir de votre hub IoT. Lors de l’application d’exemple hello reçoit des messages hello, il clignote hello DEL. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].

## <a name="what-you-will-do"></a>Procédure à suivre
* Connectez le hub IoT tooyour hello exemple application.
* Déployer et exécuter l’exemple d’application hello.
* Envoyer des messages à partir de votre hello dans IoT hub tooEdison tooblink DEL.

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :
* Comment les messages entrants de toomonitor à partir de votre hub IoT.
* Comment les messages à partir de votre tooEdison de hub IoT toosend cloud-à-appareil.

## <a name="what-you-need"></a>Ce dont vous avez besoin
* Intel Edison, configuré et prêt à l’emploi. toolearn tooset des Edison, voir [configurer votre périphérique][configure-your-device].
* Un IoT Hub créé dans le cadre de votre abonnement Azure. toolearn comment toocreate votre IoT hub, consultez [créer votre Azure IoT Hub][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Connecter le hub IoT tooyour hello exemple application
1. Assurez-vous que vous êtes dans le dossier de dépôt hello `iot-hub-c-edison-getting-started`. Ouvrir l’exemple d’application hello dans Visual Studio Code par hello suivant les commandes en cours d’exécution :

   ```bash
   cd Lesson4
   code .
   ```

   fichier Hello Bonjour `app` sous-dossier est le fichier de source de la clé hello qui contient les messages entrants toomonitor code hello à partir du hub IoT de hello. Hello `blinkLED` fonction clignote hello DEL.

   ![Structure de référentiel dans l’exemple d’application hello][repo-structure]
2. Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :

   ```bash
   npm install
   gulp init
   ```

   Si vous avez terminé les étapes de hello dans [créer un compte d’application et de stockage Azure fonction] [ create-an-azure-function-app-and-storage-account] sur cet ordinateur, toutes les configurations de hello sont héritées, vous pouvez sauter des tâches de toohello hello étape du déploiement et exemple d’application hello en cours d’exécution. Si vous avez terminé les étapes de hello dans [créer un compte d’application et de stockage Azure fonction] [ create-an-azure-function-app-and-storage-account] sur un autre ordinateur, vous avez besoin des espaces réservés de hello tooreplace Bonjour `config-edison.json` fichier. Hello `config-edison.json` fichier se trouve dans le sous-dossier hello de votre dossier de base.

   ![Contenu du fichier de configuration-edison.json hello](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * Remplacez **[nom d’hôte du périphérique ou adresse IP]** avec l’adresse IP du périphérique hello démarquer lorsque vous avez configuré votre appareil.
   * Remplacez **[chaîne de connexion de périphérique IoT]** avec la chaîne de connexion de périphérique hello que vous obtenez en exécutant hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` commande.
   * Remplacez **[chaîne de connexion de hub IoT]** avec hello chaîne de connexion de hub IoT que vous obtenez en exécutant hello `az iot hub show-connection-string --name {my hub name}` commande.

   > [!NOTE]
   > Exécutez également **gulp install-tools**, si vous ne l’avez pas fait dans la leçon 1.

## <a name="deploy-and-run-hello-sample-application"></a>Déployer et exécuter l’exemple d’application hello
Déployer et exécuter l’exemple d’application hello sur Edison en exécutant hello suivant les commandes :

```bash
gulp deploy && gulp run
```

commande de gulp Hello déploie tooEdison d’application exemple hello. Ensuite, elle s’exécute application hello sur Edison et une tâche distincte sur votre hôte ordinateur toosend 20 blink messages tooEdison à partir de votre hub IoT.

Après l’exécution de l’exemple d’application hello, il commence à écouter toomessages à partir de votre hub IoT. Pendant ce temps, tâche de gulp hello envoie plusieurs messages « clignoter » à partir de votre tooEdison de hub IoT. Pour chaque message blink Edison reçoit, exemple d’application hello appelle hello `blinkLED` hello tooblink de fonction DEL.

Vous devez voir clignotement de LED hello toutes les deux secondes comme hello gulp la tâche envoie des messages à partir de votre tooEdison de hub IoT 20. Hello dernier un est un message « arrêter » qui arrête l’application hello de s’exécuter.

![Exemple d’application avec la commande gulp et les messages de clignotement][gulp-command-and-blink-messages]

## <a name="summary"></a>Résumé
Vous avez correctement envoyé des messages à partir de votre hello dans IoT hub tooEdison tooblink DEL. la tâche suivante Hello est facultative : modifier hello et désactiver le comportement de hello DEL.

## <a name="next-steps"></a>Étapes suivantes
[Modifier hello et désactiver le comportement de hello DEL][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure_c.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink_c.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-c-lesson4-change-led-behavior.md