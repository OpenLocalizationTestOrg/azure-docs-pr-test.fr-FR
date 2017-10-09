---
title: "Connect Arduino (C) tooAzure IoT - leçon 3 : stockage de Table | Documents Microsoft"
description: "Surveiller les messages appareil-à-cloud hello qu’ils sont écrits de stockage de Table Azure tooyour."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "données dans le cloud de hello, collecte de données de cloud, le service cloud iot, iot données"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fef18bc9e780e78d95f0c643a5f193125130a5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Lecture des messages conservés dans le stockage Azure
## <a name="what-you-will-do"></a>Procédure à suivre
Moniteur hello appareil-à-cloud les messages sont envoyés à partir de votre concentrateur de IoT tooyour Adafruit estompe M0 Wi-Fi Arduino du tableau en tant que messages hello sont écrits stockage de Table Azure tooyour.

Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].

## <a name="what-you-will-learn"></a>Contenu
Dans cet article, vous allez apprendre le mode de conservation des messages de tooread toouse hello gulp tâche de lecture du message dans votre stockage de Table Azure.

## <a name="what-you-need"></a>Ce dont vous avez besoin
Avant de commencer ce processus, vous devez avoir terminé avec succès [exécuter hello blink Azure exemple d’application sur votre carte mère Arduino][run-blink-application].

## <a name="read-new-messages-from-your-storage-account"></a>Lecture des nouveaux messages à partir de votre compte de stockage
Dans l’article précédent de hello, vous avez exécuté un exemple d’application dans votre tableau de Arduino. exemple d’application Hello envoyé concentrateur de messages tooyour Azure IoT. messages d’appel envoyés tooyour IoT hub sont stockés dans votre stockage de Table Azure via l’application de fonction Azure hello. Vous devez les messages tooread chaîne hello stockage Azure connexion à partir de votre stockage de Table Azure.

les messages tooread stockés dans votre stockage de Table Azure, procédez comme suit :

1. Obtenir la chaîne de connexion hello en exécutant hello suivant les commandes :

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Hello première commande extrait hello `storage name` qui est utilisée dans la chaîne de connexion hello deuxième commande tooget hello. Utilisez `iot-sample` en tant que valeur hello `{resource group name}` si vous n’avez modifié la valeur de hello.
2. Fichier de configuration Open hello `config-arduino.json` dans le Code de Visual Studio en exécutant hello de commande suivante :

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. Remplacez `[Azure storage connection string]` avec la chaîne de connexion hello que vous avez obtenu à l’étape 1.
4. Enregistrer hello `config-arduino.json` fichier.
5. Envoyer des messages à nouveau et les lire à partir de votre stockage de Table Azure en exécutant hello de commande suivante :

   ```bash
   gulp run --read-storage

   # You can monitor hello serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   Bonjour logique pour la lecture à partir du stockage de Table Azure est Bonjour `azure-table.js` fichier.

   ![exécutez gulp --lire-stockage][gulp-run]

## <a name="summary"></a>Résumé
Vous avez correctement connecté votre Arduino tableau tooyour IoT hub dans le cloud de hello et utilisé hello blink exemples application toosend appareil-à-cloud de messages. Vous avez également utilisé hello fonction Azure application toostore entrant IoT hub messages tooyour stockage de Table Azure. Vous pouvez maintenant envoyer des messages cloud-à-appareil de votre tooyour de hub IoT Arduino carte.

## <a name="next-steps"></a>Étapes suivantes
[Envoyer des messages Cloud vers appareil][send-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md