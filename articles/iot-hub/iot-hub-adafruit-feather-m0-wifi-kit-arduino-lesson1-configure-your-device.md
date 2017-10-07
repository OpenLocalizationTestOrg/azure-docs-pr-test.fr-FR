---
title: "Connect Arduino (C) tooAzure IoT - leçon 1 : configurer l’appareil | Documents Microsoft"
description: "Configurez Adafruit Feather M0 WiFi pour une première utilisation."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino configuré, connectez-vous arduino toopc, le programme d’installation arduino, arduino carte"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>Configurer votre appareil
## <a name="what-you-will-do"></a>Procédure à suivre
Configurer votre tableau Adafruit estompe M0 Wi-Fi Arduino pour la première utilisation en assemblant tableau hello, il sous tension. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-you-need"></a>Ce dont vous avez besoin
toocomplete cette opération, vous devez hello composants suivants de votre Starter Kit pour Adafruit estompe M0 Wi-Fi :

* Hello Adafruit estompe M0 WiFi tableau
* Un câble USB d’un de tooType Micro B

![kit][kit]

Vous aurez également besoin des éléments suivants :

* Un ordinateur exécutant Windows, Mac ou Linux.
* Une connexion sans fil pour votre tooconnect de carte Arduino à.
* Un outil de configuration toodownload de connexion Internet.

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :

* Comment tooassemble votre Arduino carte et l’alimentation pour hello suivant leçons.
* Comment tooadd les autorisations de port série sur Ubuntu.

## <a name="connect-your-arduino-board-tooyour-computer"></a>Connectez votre ordinateur de tooyour Arduino du tableau

1. Branchez les câbles USB micro hello le port USB supérieur micro hello.

   ![Port micro USB du haut][top-micro-usb-port]

2. Plug hello l’autre extrémité du câble USB à votre ordinateur.

   ![USB de l’ordinateur][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a>Ajouter des autorisations de port série sous Ubuntu

Vous pouvez ignorer cette section si vous utilisez Windows ou macOS. Ubuntu, vous devez hello suivant toomake étapes qu’utilisateur linux normal de hello a hello autorisations toooperate sur le port USB hello de votre tableau Arduino.

1. À présent, en tant qu’utilisateur normal à partir du terminal :

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   Vous obtenez le résultat suivant :

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   Hello « 0 » peut être un nombre différent, ou plusieurs entrées peuvent être retournées. Dans les premières données hello cas hello, nous devons est `uucp`, Bonjour ensuite est `dialout`, qui est propriétaire du groupe de fichiers de hello hello.

2. Ajouter un groupe d’utilisateurs toohello toohello :

   ```bash
   sudo usermod -a -G group-name username
   ```

   Où `group-name` est trouvées dans la première étape de hello, les données de salutation et `username` est votre nom d’utilisateur linux.

3. Vous devez toolog extraction et à nouveau pour cette modification tootake effet et du programme d’installation complète hello.

## <a name="summary"></a>Résumé
Dans cet article, vous avez appris comment tooconfigure votre tableau Arduino. la tâche suivante Hello est tooinstall hello outils et nécessaires logiciel en vue d’un exemple d’application en cours d’exécution sur votre tableau de Arduino.

![Le matériel est prêt.][hardware-is-ready]

## <a name="next-steps"></a>Étapes suivantes
[Obtenir les outils de hello][get-the-tools]
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md