---
title: "Se connecter framboises Pi (nœud) tooAzure IoT - leçon 4 : modifier l’application | Documents Microsoft"
description: "Personnaliser hello de toochange messages hello voyants du et désactiver le comportement."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "contrôler la led avec raspberry pi, contrôle de la led raspberry pi, raspberry pi contrôle de la led"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 3b42a4ad-0197-42f6-8ca9-04c883e879e8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 99b542fcb8639add0f5a0f7a49dd8abd0e224a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Modifier hello et désactiver le comportement de hello DEL
## <a name="what-you-will-do"></a>Procédure à suivre
Personnaliser hello de toochange messages hello voyants du et désactiver le comportement. Si vous rencontrez des problèmes, rechercher des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu
Utilisez hello toochange fonctions supplémentaire Node.js voyants du et désactiver le comportement.

## <a name="what-you-need"></a>Ce dont vous avez besoin
Vous devez avoir terminé [exécuter un exemple d’application sur framboises Pi tooreceive messages cloud-à-appareil](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).

## <a name="add-nodejs-functions"></a>Ajout de fonctions Node.js
1. Ouvrir l’exemple d’application hello dans le code de Visual Studio en exécutant hello suivant les commandes :
   
   ```bash
   cd Lesson4
   code .
   ```
2. Ouvrez hello `app.js` et puis ajoutez hello suivant des fonctions à la fin de hello :
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![Fichier App.js avec fonctions ajoutées](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. Ajouter hello suivant avant hello par défaut dans un bloc switch case de hello Hello `receiveMessageCallback` fonction :
   
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
   
   ![Fichier Gulpfile.js avec fonction ajoutée](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile.png)
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

![Exemple d’application messages d’activation et de désactivation](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

Félicitations ! Vous avez personnalisé correctement les messages hello tooPi envoyés à partir de votre hub IoT.

### <a name="summary"></a>Résumé
Cette section montre comment toocustomize messages d’application d’exemple hello peut contrôler hello et désactiver le comportement de hello DEL d’une manière différente.

