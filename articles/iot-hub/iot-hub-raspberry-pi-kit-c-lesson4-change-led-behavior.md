---
title: "Connect Raspberry PI (C) tooAzure IoT - leçon 4 : modifier l’application | Documents Microsoft"
description: "Personnaliser hello de toochange messages hello voyants du et désactiver le comportement."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "contrôler la led avec raspberry pi, contrôle de la led raspberry pi, raspberry pi contrôle de la led"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 0201b8ed-d5e6-4445-9a4d-1305003d1eff
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f4739c4e9a58b4b0fe964b5c3c81e5918982099f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Modifier hello et désactiver le comportement de hello DEL
## <a name="what-you-will-do"></a>Procédure à suivre
Personnaliser hello de toochange messages hello voyants du et désactiver le comportement. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu
Utilisez hello toochange fonctions supplémentaire Node.js voyants du et désactiver le comportement.

## <a name="what-you-need"></a>Ce dont vous avez besoin
Vous devez avoir terminé [exécuter un exemple d’application sur le cloud de tooreceive framboises Pi toodevice messages](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).

## <a name="add-functions-toomainc-and-gulpfilejs"></a>Ajouter des gulpfile.js et des fonctions toomain.c
1. Ouvrir l’exemple d’application hello dans le code de Visual Studio en exécutant hello suivant les commandes :

   ```bash
   cd Lesson4
   code .
   ```
2. Ouvrez hello `main.c` et puis ajoutez hello suivant des fonctions après blinkLED() fonction :

   ```c
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![Fichier main.c avec fonctions ajoutées](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_c.png)
3. Ajouter hello suivant les conditions avant hello par défaut hello `if` bloc Hello `receiveMessageCallback` fonction :

   ```c
   else if (0 == strcmp((const char*)value, "\"on\""))
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\""))
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
   }
   ```

   ![Fichier Gulpfile.js avec fonction ajoutée](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile_c.png)
5. Bonjour `sendMessage` de fonction, remplacez la ligne de hello `var message = buildMessage(sentMessageCount);` avec ligne hello illustré hello suivant extrait de code :

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Enregistrer toutes les modifications de hello.

### <a name="deploy-and-run-hello-sample-application"></a>Déployer et exécuter l’exemple d’application hello
Déployer et exécuter l’exemple d’application hello sur Pi en exécutant hello de commande suivante :

```bash
gulp deploy && gulp run
```

Vous devez voir hello DEL activer pendant deux secondes et puis désactivez l’option pour un autre deux secondes. dernier « arrêter » message Hello arrête l’application d’exemple hello de s’exécuter.

![Exemple d’application messages d’activation et de désactivation](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

Félicitations ! Vous avez personnalisé correctement les messages hello tooPi envoyés à partir de votre hub IoT.

### <a name="summary"></a>Résumé
Cette section montre comment toocustomize messages d’application d’exemple hello peut contrôler hello et désactiver le comportement de hello DEL d’une manière différente.
