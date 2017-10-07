---
title: "Se connecter tooAzure Intel Edison (nœud) IoT - leçon 4 : Blink hello DEL | Documents Microsoft"
description: "Personnaliser hello de toochange messages hello voyants du et désactiver le comportement."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "contrôle de la LED avec arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 387cd97e-b05e-43c4-b252-f68ad45d524a
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: caeabe311fd1698f298c6d2b4a203ecad80ef7df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Modifier hello et désactiver le comportement de hello DEL
## <a name="what-you-will-do"></a>Procédure à suivre
Personnaliser hello de toochange messages hello voyants du et désactiver le comportement. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].

## <a name="what-you-will-learn"></a>Contenu
Utilisez hello toochange de fonctions supplémentaires voyants du et désactiver le comportement.

## <a name="what-you-need"></a>Ce dont vous avez besoin
Vous devez avoir terminé [exécuter un exemple d’application sur le cloud de tooreceive Intel Edison toodevice messages][receive-cloud-to-device-messages].

## <a name="add-functions-tooappjs-and-gulpfilejs"></a>Ajouter des gulpfile.js et des fonctions tooapp.js
1. Ouvrir l’exemple d’application hello dans le code de Visual Studio en exécutant hello suivant les commandes :

   ```bash
   cd Lesson4
   code .
   ```
2. Ouvrez hello `app.js` et puis ajoutez hello suivant des fonctions après blinkLED() fonction :

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![Fichier app.js avec fonctions ajoutées](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. Ajouter hello des conditions suivantes avant de hello 'blink' cas dans un bloc switch case de hello Hello `receiveMessageCallback` fonction :

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
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

   ![Fichier Gulpfile.js avec fonction ajoutée][gulpfile]
5. Bonjour `sendMessage` de fonction, remplacez la ligne de hello `var message = buildMessage(sentMessageCount);` avec ligne hello illustré hello suivant extrait de code :

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Enregistrer toutes les modifications de hello.

### <a name="deploy-and-run-hello-sample-application"></a>Déployer et exécuter l’exemple d’application hello
Déployer et exécuter l’exemple d’application hello sur Edison en exécutant hello de commande suivante :

```bash
gulp deploy && gulp run
```

Vous devez voir hello DEL activer pendant deux secondes et puis désactivez l’option pour un autre deux secondes. dernier « arrêter » message Hello arrête l’application d’exemple hello de s’exécuter.

![activer et désactiver][on-and-off]

Félicitations ! Vous avez personnalisé correctement les messages hello tooEdison envoyés à partir de votre hub IoT.

### <a name="summary"></a>Résumé
Cette section montre comment toocustomize messages d’application d’exemple hello peut contrôler hello et désactiver le comportement de hello DEL d’une manière différente.

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
