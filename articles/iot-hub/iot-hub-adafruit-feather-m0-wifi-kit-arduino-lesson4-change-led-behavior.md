---
title: "Connecter Arduino (C) à Azure IoT - Leçon 4 : Modifier une application | Microsoft Docs"
description: "Personnalisez les messages pour modifier le comportement activé/désactivé de la LED."
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
ms.openlocfilehash: 5009a0466f2c5689b8ab426049f4c4f02272512b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="95fb5-104">Modification du comportement activé/désactivé de la LED</span><span class="sxs-lookup"><span data-stu-id="95fb5-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="95fb5-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="95fb5-105">What you will do</span></span>
<span data-ttu-id="95fb5-106">Personnalisez les messages pour modifier le comportement activé/désactivé de la LED.</span><span class="sxs-lookup"><span data-stu-id="95fb5-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="95fb5-107">Si vous rencontrez des problèmes, recherchez une solution sur la [page de résolution des problèmes](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) pour la carte Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="95fb5-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="95fb5-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="95fb5-108">What you will learn</span></span>
<span data-ttu-id="95fb5-109">Utiliser des fonctions supplémentaires Arduino pour modifier le comportement activé/désactivé de la LED.</span><span class="sxs-lookup"><span data-stu-id="95fb5-109">Use additional Arduino functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="95fb5-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="95fb5-110">What you need</span></span>
<span data-ttu-id="95fb5-111">Vous devez avoir correctement suivi la section [Exécution d’un exemple d’application sur votre carte Arduino pour recevoir des messages cloud-à-appareil][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="95fb5-111">You must have successfully completed [Run a sample application on your Arduino board to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="95fb5-112">Ajouter des fonctions à main.c et gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="95fb5-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="95fb5-113">Ouvrez l’exemple d’application dans Visual Studio Code en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="95fb5-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="95fb5-114">Ouvrez le fichier `app.ino` et ajoutez les fonctions suivantes après la fonction blinkLED() :</span><span class="sxs-lookup"><span data-stu-id="95fb5-114">Open the `app.ino` file, and then add the following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="95fb5-116">Ajoutez les conditions suivantes avant d’effectuer le bloc `else if` de la fonction `receiveMessageCallback` :</span><span class="sxs-lookup"><span data-stu-id="95fb5-116">Add the following conditions before the `else if` block of the `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="95fb5-117">Vous avez maintenant configuré l’exemple d’application pour répondre à davantage d’instructions envoyées via des messages.</span><span class="sxs-lookup"><span data-stu-id="95fb5-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="95fb5-118">L’instruction « on » active la LED et l’instruction « off » la désactive.</span><span class="sxs-lookup"><span data-stu-id="95fb5-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="95fb5-119">Ouvrez le fichier gulpfile.js, puis ajoutez une nouvelle fonction devant la fonction `sendMessage` :</span><span class="sxs-lookup"><span data-stu-id="95fb5-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

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
5. <span data-ttu-id="95fb5-121">Dans la fonction `sendMessage`, remplacez la ligne `var message = buildMessage(sentMessageCount);` par la nouvelle ligne illustrée dans l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="95fb5-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="95fb5-122">Enregistrez toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="95fb5-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="95fb5-123">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="95fb5-123">Deploy and run the sample application</span></span>
<span data-ttu-id="95fb5-124">Déployez et exécutez l’exemple d’application sur votre carte Arduino en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="95fb5-124">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="95fb5-125">La LED doit s’allumer pendant deux secondes, puis s’éteindre pendant deux secondes.</span><span class="sxs-lookup"><span data-stu-id="95fb5-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="95fb5-126">Le dernier message de « stop » arrête l’exécution de l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="95fb5-126">The last "stop" message stops the sample application from running.</span></span>

![activer et désactiver][on-and-off]

<span data-ttu-id="95fb5-128">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="95fb5-128">Congratulations!</span></span> <span data-ttu-id="95fb5-129">Vous avez correctement personnalisé les messages qui sont envoyés à votre carte Arduino à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="95fb5-129">You’ve successfully customized the messages that are sent to your Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="95fb5-130">Résumé</span><span class="sxs-lookup"><span data-stu-id="95fb5-130">Summary</span></span>
<span data-ttu-id="95fb5-131">Cette section facultative montre comment personnaliser les messages de sorte que l’exemple d’application puisse contrôler le comportement activé/désactivé de la LED d’une autre manière.</span><span class="sxs-lookup"><span data-stu-id="95fb5-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png