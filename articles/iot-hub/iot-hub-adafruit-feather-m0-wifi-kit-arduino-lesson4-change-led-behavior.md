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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="92cde-104">Modifier hello et désactiver le comportement de hello DEL</span><span class="sxs-lookup"><span data-stu-id="92cde-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="92cde-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="92cde-105">What you will do</span></span>
<span data-ttu-id="92cde-106">Personnaliser hello de toochange messages hello voyants du et désactiver le comportement.</span><span class="sxs-lookup"><span data-stu-id="92cde-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="92cde-107">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) pour votre carte mère Adafruit estompe M0 Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="92cde-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="92cde-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="92cde-108">What you will learn</span></span>
<span data-ttu-id="92cde-109">Utilisez hello toochange fonctions supplémentaire Arduino DEL d’et désactiver le comportement.</span><span class="sxs-lookup"><span data-stu-id="92cde-109">Use additional Arduino functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="92cde-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="92cde-110">What you need</span></span>
<span data-ttu-id="92cde-111">Vous devez avoir terminé [exécuter un exemple d’application sur votre cloud de tooreceive tableau Arduino toodevice messages][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="92cde-111">You must have successfully completed [Run a sample application on your Arduino board tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="92cde-112">Ajouter des gulpfile.js et des fonctions toomain.c</span><span class="sxs-lookup"><span data-stu-id="92cde-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="92cde-113">Ouvrir l’exemple d’application hello dans le code de Visual Studio en exécutant hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="92cde-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="92cde-114">Ouvrez hello `app.ino` et puis ajoutez hello suivant des fonctions après blinkLED() fonction :</span><span class="sxs-lookup"><span data-stu-id="92cde-114">Open hello `app.ino` file, and then add hello following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="92cde-116">Ajouter hello conditions avant hello suivantes `else if` bloc Hello `receiveMessageCallback` fonction :</span><span class="sxs-lookup"><span data-stu-id="92cde-116">Add hello following conditions before hello `else if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="92cde-117">Vous avez maintenant configuré instructions toomore de toorespond l’application exemple hello via des messages.</span><span class="sxs-lookup"><span data-stu-id="92cde-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="92cde-118">Hello « sur « instruction active hello DEL et hello instruction « off » désactive hello DEL.</span><span class="sxs-lookup"><span data-stu-id="92cde-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="92cde-119">Ouvrez le fichier de gulpfile.js hello et puis ajoutez une nouvelle fonction avant la fonction hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="92cde-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="92cde-121">Bonjour `sendMessage` de fonction, remplacez la ligne de hello `var message = buildMessage(sentMessageCount);` avec ligne hello illustré hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="92cde-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="92cde-122">Enregistrer toutes les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="92cde-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="92cde-123">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="92cde-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="92cde-124">Déployer et exécuter des application d’exemple hello sur votre carte mère Arduino en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="92cde-124">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="92cde-125">Vous devez voir hello DEL activer pendant deux secondes et puis désactivez l’option pour un autre deux secondes.</span><span class="sxs-lookup"><span data-stu-id="92cde-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="92cde-126">dernier « arrêter » message Hello arrête l’application d’exemple hello de s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="92cde-126">hello last "stop" message stops hello sample application from running.</span></span>

![activer et désactiver][on-and-off]

<span data-ttu-id="92cde-128">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="92cde-128">Congratulations!</span></span> <span data-ttu-id="92cde-129">Vous avez personnalisé correctement les messages hello envoyés tooyour Arduino tableau à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="92cde-129">You’ve successfully customized hello messages that are sent tooyour Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="92cde-130">Résumé</span><span class="sxs-lookup"><span data-stu-id="92cde-130">Summary</span></span>
<span data-ttu-id="92cde-131">Cette section montre comment toocustomize messages d’application d’exemple hello peut contrôler hello et désactiver le comportement de hello DEL d’une manière différente.</span><span class="sxs-lookup"><span data-stu-id="92cde-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png