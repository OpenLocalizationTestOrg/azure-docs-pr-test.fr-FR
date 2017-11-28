---
title: "Connect Intel Edison (C) tooAzure IoT - leçon 4 : Blink hello DEL | Documents Microsoft"
description: "Personnaliser hello de toochange messages hello voyants du et désactiver le comportement."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "contrôle de la LED avec arduino"
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
ms.openlocfilehash: c51acb42aa297ca91cfe76d7b0361ad95e2fb2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="5fbd2-104">Modifier hello et désactiver le comportement de hello DEL</span><span class="sxs-lookup"><span data-stu-id="5fbd2-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5fbd2-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="5fbd2-105">What you will do</span></span>
<span data-ttu-id="5fbd2-106">Personnaliser hello de toochange messages hello voyants du et désactiver le comportement.</span><span class="sxs-lookup"><span data-stu-id="5fbd2-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="5fbd2-107">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="5fbd2-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5fbd2-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="5fbd2-108">What you will learn</span></span>
<span data-ttu-id="5fbd2-109">Utilisez hello toochange de fonctions supplémentaires voyants du et désactiver le comportement.</span><span class="sxs-lookup"><span data-stu-id="5fbd2-109">Use additional functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5fbd2-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="5fbd2-110">What you need</span></span>
<span data-ttu-id="5fbd2-111">Vous devez avoir terminé [exécuter un exemple d’application sur le cloud de tooreceive Intel Edison toodevice messages][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="5fbd2-111">You must have successfully completed [Run a sample application on Intel Edison tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="5fbd2-112">Ajouter des gulpfile.js et des fonctions toomain.c</span><span class="sxs-lookup"><span data-stu-id="5fbd2-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="5fbd2-113">Ouvrir l’exemple d’application hello dans le code de Visual Studio en exécutant hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="5fbd2-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="5fbd2-114">Ouvrez hello `main.c` et puis ajoutez hello suivant des fonctions après blinkLED() fonction :</span><span class="sxs-lookup"><span data-stu-id="5fbd2-114">Open hello `main.c` file, and then add hello following functions after blinkLED() function:</span></span>

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

3. <span data-ttu-id="5fbd2-116">Ajouter hello conditions avant hello suivantes `else if` bloc Hello `receiveMessageCallback` fonction :</span><span class="sxs-lookup"><span data-stu-id="5fbd2-116">Add hello following conditions before hello `else if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="5fbd2-117">Vous avez maintenant configuré instructions toomore de toorespond l’application exemple hello via des messages.</span><span class="sxs-lookup"><span data-stu-id="5fbd2-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="5fbd2-118">Hello « sur « instruction active hello DEL et hello instruction « off » désactive hello DEL.</span><span class="sxs-lookup"><span data-stu-id="5fbd2-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="5fbd2-119">Ouvrez le fichier de gulpfile.js hello et puis ajoutez une nouvelle fonction avant la fonction hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="5fbd2-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="5fbd2-121">Bonjour `sendMessage` de fonction, remplacez la ligne de hello `var message = buildMessage(sentMessageCount);` avec ligne hello illustré hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="5fbd2-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="5fbd2-122">Enregistrer toutes les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="5fbd2-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="5fbd2-123">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="5fbd2-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="5fbd2-124">Déployer et exécuter l’exemple d’application hello sur Edison en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5fbd2-124">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="5fbd2-125">Vous devez voir hello DEL activer pendant deux secondes et puis désactivez l’option pour un autre deux secondes.</span><span class="sxs-lookup"><span data-stu-id="5fbd2-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="5fbd2-126">dernier « arrêter » message Hello arrête l’application d’exemple hello de s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="5fbd2-126">hello last "stop" message stops hello sample application from running.</span></span>

![activer et désactiver][on-and-off]

<span data-ttu-id="5fbd2-128">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="5fbd2-128">Congratulations!</span></span> <span data-ttu-id="5fbd2-129">Vous avez personnalisé correctement les messages hello tooEdison envoyés à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5fbd2-129">You’ve successfully customized hello messages that are sent tooEdison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="5fbd2-130">Résumé</span><span class="sxs-lookup"><span data-stu-id="5fbd2-130">Summary</span></span>
<span data-ttu-id="5fbd2-131">Cette section montre comment toocustomize messages d’application d’exemple hello peut contrôler hello et désactiver le comportement de hello DEL d’une manière différente.</span><span class="sxs-lookup"><span data-stu-id="5fbd2-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
