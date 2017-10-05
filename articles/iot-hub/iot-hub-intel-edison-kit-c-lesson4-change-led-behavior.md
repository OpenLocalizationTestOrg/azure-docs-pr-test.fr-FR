---
title: "Connecter Intel Edison (C) à Azure IoT - Leçon 4 : Faire clignoter la LED | Microsoft Docs"
description: "Personnalisez les messages pour modifier le comportement activé/désactivé de la LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "contrôle de la led avec arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 9826c55a-0e24-4296-ae54-29b7fe66436a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4852b1cca4c6186ef4857b903b771f76cc20adb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="1793a-104">Modification du comportement activé/désactivé de la LED</span><span class="sxs-lookup"><span data-stu-id="1793a-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="1793a-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="1793a-105">What you will do</span></span>
<span data-ttu-id="1793a-106">Personnalisez les messages pour modifier le comportement activé/désactivé de la LED.</span><span class="sxs-lookup"><span data-stu-id="1793a-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="1793a-107">Si vous rencontrez des problèmes, recherchez des solutions sur la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="1793a-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1793a-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="1793a-108">What you will learn</span></span>
<span data-ttu-id="1793a-109">Utiliser des fonctions supplémentaires pour modifier le comportement activé/désactivé de la LED.</span><span class="sxs-lookup"><span data-stu-id="1793a-109">Use additional functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1793a-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="1793a-110">What you need</span></span>
<span data-ttu-id="1793a-111">Vous devez avoir correctement suivi la section [Exécution d’un exemple d’application sur Intel Edison pour recevoir des messages cloud-à-appareil][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="1793a-111">You must have successfully completed [Run a sample application on Intel Edison to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="1793a-112">Ajouter des fonctions à main.c et gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="1793a-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="1793a-113">Ouvrez l’exemple d’application dans Visual Studio Code en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1793a-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="1793a-114">Ouvrez le fichier `main.c` et ajoutez les fonctions suivantes après la fonction blinkLED() :</span><span class="sxs-lookup"><span data-stu-id="1793a-114">Open the `main.c` file, and then add the following functions after blinkLED() function:</span></span>

   ```c
   static void turnOnLED()
   {
     mraa_gpio_write(context, 1);
   }

   static void turnOffLED()
   {
     mraa_gpio_write(context, 0);
   }
   ```

   ![Fichier main.c avec fonctions ajoutées](media/iot-hub-intel-edison-lessons/lesson4/updated_app_c.png)

3. <span data-ttu-id="1793a-116">Ajoutez les conditions suivantes avant d’effectuer le bloc `else if` de la fonction `receiveMessageCallback` :</span><span class="sxs-lookup"><span data-stu-id="1793a-116">Add the following conditions before the `else if` block of the `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="1793a-117">Vous avez maintenant configuré l’exemple d’application pour répondre à davantage d’instructions envoyées via des messages.</span><span class="sxs-lookup"><span data-stu-id="1793a-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="1793a-118">L’instruction « on » active la LED et l’instruction « off » la désactive.</span><span class="sxs-lookup"><span data-stu-id="1793a-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="1793a-119">Ouvrez le fichier gulpfile.js, puis ajoutez une nouvelle fonction devant la fonction `sendMessage` :</span><span class="sxs-lookup"><span data-stu-id="1793a-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

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
5. <span data-ttu-id="1793a-121">Dans la fonction `sendMessage`, remplacez la ligne `var message = buildMessage(sentMessageCount);` par la nouvelle ligne illustrée dans l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="1793a-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="1793a-122">Enregistrez toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="1793a-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="1793a-123">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="1793a-123">Deploy and run the sample application</span></span>
<span data-ttu-id="1793a-124">Déployez et exécutez l’exemple d’application sur Edison en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1793a-124">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="1793a-125">La LED doit s’allumer pendant deux secondes, puis s’éteindre pendant deux secondes.</span><span class="sxs-lookup"><span data-stu-id="1793a-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="1793a-126">Le dernier message de « stop » arrête l’exécution de l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="1793a-126">The last "stop" message stops the sample application from running.</span></span>

![activer et désactiver][on-and-off]

<span data-ttu-id="1793a-128">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="1793a-128">Congratulations!</span></span> <span data-ttu-id="1793a-129">Vous avez correctement personnalisé les messages qui sont envoyés à Edison à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1793a-129">You’ve successfully customized the messages that are sent to Edison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="1793a-130">Résumé</span><span class="sxs-lookup"><span data-stu-id="1793a-130">Summary</span></span>
<span data-ttu-id="1793a-131">Cette section facultative montre comment personnaliser les messages de sorte que l’exemple d’application puisse contrôler le comportement activé/désactivé de la LED d’une autre manière.</span><span class="sxs-lookup"><span data-stu-id="1793a-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
