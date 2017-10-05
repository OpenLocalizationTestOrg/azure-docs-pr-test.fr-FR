---
title: "Connecter Raspberry Pi (Node) à Azure IoT - Leçon 4 : Modifier une application | Microsoft Docs"
description: "Personnalisez les messages pour modifier le comportement activé/désactivé de la LED."
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
ms.openlocfilehash: b2ae23ac9cc1723936c4b4e1900b95cdcde744df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="43fd8-104">Modification du comportement activé/désactivé de la LED</span><span class="sxs-lookup"><span data-stu-id="43fd8-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="43fd8-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="43fd8-105">What you will do</span></span>
<span data-ttu-id="43fd8-106">Personnalisez les messages pour modifier le comportement activé/désactivé de la LED.</span><span class="sxs-lookup"><span data-stu-id="43fd8-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="43fd8-107">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="43fd8-107">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="43fd8-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="43fd8-108">What you will learn</span></span>
<span data-ttu-id="43fd8-109">Utiliser des fonctions supplémentaires de Node.js pour modifier le comportement activé/désactivé de la LED.</span><span class="sxs-lookup"><span data-stu-id="43fd8-109">Use additional Node.js functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="43fd8-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="43fd8-110">What you need</span></span>
<span data-ttu-id="43fd8-111">Vous devez avoir correctement suivi la section [Exécution d’un exemple d’application sur Raspberry Pi pour recevoir des messages cloud-à-appareil](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="43fd8-111">You must have successfully completed [Run a sample application on Raspberry Pi to receive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-nodejs-functions"></a><span data-ttu-id="43fd8-112">Ajout de fonctions Node.js</span><span class="sxs-lookup"><span data-stu-id="43fd8-112">Add Node.js functions</span></span>
1. <span data-ttu-id="43fd8-113">Ouvrez l’exemple d’application dans Visual Studio Code en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="43fd8-113">Open the sample application in Visual Studio code by running the following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="43fd8-114">Ouvrez le fichier `app.js`, puis ajoutez les fonctions suivantes à la fin :</span><span class="sxs-lookup"><span data-stu-id="43fd8-114">Open the `app.js` file, and then add the following functions at the end:</span></span>
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![Fichier App.js avec fonctions ajoutées](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. <span data-ttu-id="43fd8-116">Ajouter les conditions suivantes avant la condition par défaut dans le bloc switch-case de la fonction `receiveMessageCallback` :</span><span class="sxs-lookup"><span data-stu-id="43fd8-116">Add the following conditions before the default one in the switch-case block of the `receiveMessageCallback` function:</span></span>
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   <span data-ttu-id="43fd8-117">Vous avez maintenant configuré l’exemple d’application pour répondre à davantage d’instructions envoyées via des messages.</span><span class="sxs-lookup"><span data-stu-id="43fd8-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="43fd8-118">L’instruction « on » active la LED et l’instruction « off » la désactive.</span><span class="sxs-lookup"><span data-stu-id="43fd8-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="43fd8-119">Ouvrez le fichier gulpfile.js, puis ajoutez une nouvelle fonction devant la fonction `sendMessage` :</span><span class="sxs-lookup"><span data-stu-id="43fd8-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>
   
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
5. <span data-ttu-id="43fd8-121">Dans la fonction `sendMessage`, remplacez la ligne `var message = buildMessage(sentMessageCount);` par la nouvelle ligne illustrée dans l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="43fd8-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="43fd8-122">Enregistrez toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="43fd8-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="43fd8-123">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="43fd8-123">Deploy and run the sample application</span></span>
<span data-ttu-id="43fd8-124">Déployez et exécutez l’exemple d’application sur Pi en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="43fd8-124">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="43fd8-125">La LED doit s’allumer pendant deux secondes, puis s’éteindre pendant deux secondes.</span><span class="sxs-lookup"><span data-stu-id="43fd8-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="43fd8-126">Le dernier message de « stop » arrête l’exécution de l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="43fd8-126">The last "stop" message stops the sample application from running.</span></span>

![Exemple d’application messages d’activation et de désactivation](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

<span data-ttu-id="43fd8-128">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="43fd8-128">Congratulations!</span></span> <span data-ttu-id="43fd8-129">Vous avez correctement personnalisé les messages qui sont envoyés à Pi à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="43fd8-129">You’ve successfully customized the messages that are sent to Pi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="43fd8-130">Résumé</span><span class="sxs-lookup"><span data-stu-id="43fd8-130">Summary</span></span>
<span data-ttu-id="43fd8-131">Cette section facultative montre comment personnaliser les messages de sorte que l’exemple d’application puisse contrôler le comportement activé/désactivé de la LED d’une autre manière.</span><span class="sxs-lookup"><span data-stu-id="43fd8-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

