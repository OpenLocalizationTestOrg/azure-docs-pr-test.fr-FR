---
title: "Connect Arduino (C) tooAzure IoT - leçon 4 : modifier l’application | Documents Microsoft"
description: "Personnaliser hello de toochange messages hello voyants du et désactiver le comportement."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "contrôle de la LED avec arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: d7a25430-450e-43c4-a3ed-1eed995b8b7e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8cc438650f01ae4335d91c94df6a29e0ffbdc508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Modifier hello et désactiver le comportement de hello DEL
## <a name="what-you-will-do"></a>Procédure à suivre
Personnaliser hello de toochange messages hello voyants du et désactiver le comportement. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) pour votre carte mère Adafruit estompe M0 Wi-Fi Arduino.

## <a name="what-you-will-learn"></a>Contenu
Utilisez hello toochange fonctions supplémentaire Arduino DEL d’et désactiver le comportement.

## <a name="what-you-need"></a>Ce dont vous avez besoin
Vous devez avoir terminé [exécuter un exemple d’application sur votre cloud de tooreceive tableau Arduino toodevice messages][receive-cloud-to-device-messages].

## <a name="add-functions-toomainc-and-gulpfilejs"></a>Ajouter des gulpfile.js et des fonctions toomain.c
1. Ouvrir l’exemple d’application hello dans le code de Visual Studio en exécutant hello suivant les commandes :

   ```bash
   cd Lesson4
   code .
   ```
2. Ouvrez hello `app.ino` et puis ajoutez hello suivant des fonctions après blinkLED() fonction :

   ```arduino
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![Fichier app.ino avec fonctions ajoutées][app-ino-file]
3. Ajouter hello conditions avant hello suivantes `else if` bloc Hello `receiveMessageCallback` fonction :

   ```arduino
   else if (strcmp((const char*)value, "\"on\"") == 0)
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\"") == 0)
   {
       turnOffLED();
   }
   ```

   Vous avez maintenant configuré instructions toomore de toorespond l’application exemple hello via des messages. Hello « sur « instruction active hello DEL et hello instruction « off » désactive hello DEL.
4. Ouvrez le fichier de gulpfile.js hello et puis ajoutez une nouvelle fonction avant la fonction hello `sendMessage`:

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   };
   ```

   ![Fichier Gulpfile.js avec fonction ajoutée][gulp-file-js]
5. Bonjour `sendMessage` de fonction, remplacez la ligne de hello `var message = buildMessage(sentMessageCount);` avec ligne hello illustré hello suivant extrait de code :

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Enregistrer toutes les modifications de hello.

### <a name="deploy-and-run-hello-sample-application"></a>Déployer et exécuter l’exemple d’application hello
Déployer et exécuter des application d’exemple hello sur votre carte mère Arduino en exécutant hello de commande suivante :

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

Vous devez voir hello DEL activer pendant deux secondes et puis désactivez l’option pour un autre deux secondes. dernier « arrêter » message Hello arrête l’application d’exemple hello de s’exécuter.

![activer et désactiver][on-and-off]

Félicitations ! Vous avez personnalisé correctement les messages hello envoyés tooyour Arduino tableau à partir de votre hub IoT.

### <a name="summary"></a>Résumé
Cette section montre comment toocustomize messages d’application d’exemple hello peut contrôler hello et désactiver le comportement de hello DEL d’une manière différente.

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png