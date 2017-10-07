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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="f96ed-104">Modifier hello et désactiver le comportement de hello DEL</span><span class="sxs-lookup"><span data-stu-id="f96ed-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="f96ed-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="f96ed-105">What you will do</span></span>
<span data-ttu-id="f96ed-106">Personnaliser hello de toochange messages hello voyants du et désactiver le comportement.</span><span class="sxs-lookup"><span data-stu-id="f96ed-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="f96ed-107">Si vous rencontrez des problèmes, rechercher des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f96ed-107">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f96ed-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="f96ed-108">What you will learn</span></span>
<span data-ttu-id="f96ed-109">Utilisez hello toochange fonctions supplémentaire Node.js voyants du et désactiver le comportement.</span><span class="sxs-lookup"><span data-stu-id="f96ed-109">Use additional Node.js functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f96ed-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="f96ed-110">What you need</span></span>
<span data-ttu-id="f96ed-111">Vous devez avoir terminé [exécuter un exemple d’application sur framboises Pi tooreceive messages cloud-à-appareil](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="f96ed-111">You must have successfully completed [Run a sample application on Raspberry Pi tooreceive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-nodejs-functions"></a><span data-ttu-id="f96ed-112">Ajout de fonctions Node.js</span><span class="sxs-lookup"><span data-stu-id="f96ed-112">Add Node.js functions</span></span>
1. <span data-ttu-id="f96ed-113">Ouvrir l’exemple d’application hello dans le code de Visual Studio en exécutant hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="f96ed-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="f96ed-114">Ouvrez hello `app.js` et puis ajoutez hello suivant des fonctions à la fin de hello :</span><span class="sxs-lookup"><span data-stu-id="f96ed-114">Open hello `app.js` file, and then add hello following functions at hello end:</span></span>
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![Fichier App.js avec fonctions ajoutées](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. <span data-ttu-id="f96ed-116">Ajouter hello suivant avant hello par défaut dans un bloc switch case de hello Hello `receiveMessageCallback` fonction :</span><span class="sxs-lookup"><span data-stu-id="f96ed-116">Add hello following conditions before hello default one in hello switch-case block of hello `receiveMessageCallback` function:</span></span>
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   <span data-ttu-id="f96ed-117">Vous avez maintenant configuré instructions toomore de toorespond l’application exemple hello via des messages.</span><span class="sxs-lookup"><span data-stu-id="f96ed-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="f96ed-118">Hello « sur « instruction active hello DEL et hello instruction « off » désactive hello DEL.</span><span class="sxs-lookup"><span data-stu-id="f96ed-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="f96ed-119">Ouvrez le fichier de gulpfile.js hello et puis ajoutez une nouvelle fonction avant la fonction hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="f96ed-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>
   
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
5. <span data-ttu-id="f96ed-121">Bonjour `sendMessage` de fonction, remplacez la ligne de hello `var message = buildMessage(sentMessageCount);` avec ligne hello illustré hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="f96ed-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="f96ed-122">Enregistrer toutes les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="f96ed-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="f96ed-123">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="f96ed-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="f96ed-124">Déployer et exécuter l’exemple d’application hello sur Pi en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f96ed-124">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="f96ed-125">Vous devez voir hello DEL activer pendant deux secondes et puis désactivez l’option pour un autre deux secondes.</span><span class="sxs-lookup"><span data-stu-id="f96ed-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="f96ed-126">dernier « arrêter » message Hello arrête l’application d’exemple hello de s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="f96ed-126">hello last "stop" message stops hello sample application from running.</span></span>

![Exemple d’application messages d’activation et de désactivation](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

<span data-ttu-id="f96ed-128">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="f96ed-128">Congratulations!</span></span> <span data-ttu-id="f96ed-129">Vous avez personnalisé correctement les messages hello tooPi envoyés à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f96ed-129">You’ve successfully customized hello messages that are sent tooPi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="f96ed-130">Résumé</span><span class="sxs-lookup"><span data-stu-id="f96ed-130">Summary</span></span>
<span data-ttu-id="f96ed-131">Cette section montre comment toocustomize messages d’application d’exemple hello peut contrôler hello et désactiver le comportement de hello DEL d’une manière différente.</span><span class="sxs-lookup"><span data-stu-id="f96ed-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

