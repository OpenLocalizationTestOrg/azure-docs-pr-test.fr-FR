---
title: "Connect Raspberry PI (C) tooAzure IoT - leçon 4 : Cloud-à-appareil | Documents Microsoft"
description: "Un exemple d’application s’exécute sur Pi et surveille les messages entrants à partir de votre IoT Hub. Une nouvelle tâche gulp envoie des messages tooPi à partir de votre hello tooblink du hub IoT DEL."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "toodevice cloud, le message à partir du cloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5596bf3a83c21f2bd54b2f83e2a8fdad7a608b94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="86daa-105">Exécuter un tooreceive d’application exemple messages cloud-à-appareil</span><span class="sxs-lookup"><span data-stu-id="86daa-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="86daa-106">Dans cet article, vous déployez un exemple d’application sur Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="86daa-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="86daa-107">exemple d’application Hello surveille les messages entrants à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="86daa-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="86daa-108">Aussi, vous exécutez une tâche de gulp sur votre tooPi de messages toosend ordinateur à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="86daa-108">You also run a gulp task on your computer toosend messages tooPi from your IoT hub.</span></span> <span data-ttu-id="86daa-109">Lors de l’application d’exemple hello reçoit des messages hello, il clignote hello DEL.</span><span class="sxs-lookup"><span data-stu-id="86daa-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="86daa-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="86daa-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="86daa-111">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="86daa-111">What you will do</span></span>
* <span data-ttu-id="86daa-112">Connectez le hub IoT tooyour hello exemple application.</span><span class="sxs-lookup"><span data-stu-id="86daa-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="86daa-113">Déployer et exécuter l’exemple d’application hello.</span><span class="sxs-lookup"><span data-stu-id="86daa-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="86daa-114">Envoyer des messages à partir de votre hello dans IoT hub tooPi tooblink DEL.</span><span class="sxs-lookup"><span data-stu-id="86daa-114">Send messages from your IoT hub tooPi tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="86daa-115">Contenu</span><span class="sxs-lookup"><span data-stu-id="86daa-115">What you will learn</span></span>
<span data-ttu-id="86daa-116">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="86daa-116">In this article, you will learn:</span></span>
* <span data-ttu-id="86daa-117">Comment les messages entrants de toomonitor à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="86daa-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="86daa-118">Comment les messages à partir de votre tooPi de hub IoT toosend cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="86daa-118">How toosend cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="86daa-119">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="86daa-119">What you need</span></span>
* <span data-ttu-id="86daa-120">Raspberry Pi 3, configuré pour utilisation.</span><span class="sxs-lookup"><span data-stu-id="86daa-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="86daa-121">toolearn tooset de Pi, voir [configurer votre périphérique](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="86daa-121">toolearn how tooset up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="86daa-122">Un IoT Hub créé dans le cadre de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="86daa-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="86daa-123">toolearn comment toocreate votre IoT hub, consultez [créez votre hub IoT et inscrire framboises Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="86daa-123">toolearn how toocreate your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="86daa-124">Connecter le hub IoT tooyour hello exemple application</span><span class="sxs-lookup"><span data-stu-id="86daa-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="86daa-125">Assurez-vous que vous êtes dans le dossier de dépôt hello `iot-hub-c-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="86daa-125">Make sure that you're in hello repo folder `iot-hub-c-raspberrypi-getting-started`.</span></span> <span data-ttu-id="86daa-126">Ouvrir l’exemple d’application hello dans Visual Studio Code par hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="86daa-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="86daa-127">Hello d’avis `app.c` fichier Bonjour `app` sous-dossier.</span><span class="sxs-lookup"><span data-stu-id="86daa-127">Notice hello `app.c` file in hello `app` subfolder.</span></span> <span data-ttu-id="86daa-128">Hello `app.c` fichier est le fichier de source de la clé de hello qui contient les messages entrants toomonitor code hello à partir du hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="86daa-128">hello `app.c` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="86daa-129">Hello `blinkLED` fonction clignote hello DEL.</span><span class="sxs-lookup"><span data-stu-id="86daa-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Structure de référentiel dans l’exemple d’application hello](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. <span data-ttu-id="86daa-131">Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="86daa-131">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="86daa-132">Si vous avez terminé les étapes de hello dans [créer un compte d’application et de stockage Azure fonction](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) sur cet ordinateur, toutes les configurations de hello sont héritées, vous pouvez sauter toostep toohello de tâche déploiement et l’application d’exemple hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="86daa-132">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all hello configurations are inherited, so you can skip toostep toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="86daa-133">Si vous avez terminé les étapes de hello dans [créer un compte d’application et de stockage Azure fonction](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) sur un autre ordinateur, vous avez besoin des espaces réservés de hello tooreplace Bonjour `config-raspberrypi.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="86daa-133">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need tooreplace hello placeholders in hello `config-raspberrypi.json` file.</span></span> <span data-ttu-id="86daa-134">Hello `config-raspberrypi.json` fichier se trouve dans le sous-dossier hello de votre dossier de base.</span><span class="sxs-lookup"><span data-stu-id="86daa-134">hello `config-raspberrypi.json` file is in hello subfolder of your home folder.</span></span>

   ![Contenu du fichier de configuration-raspberrypi.json hello](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="86daa-136">Remplacez **[nom d’hôte du périphérique ou adresse IP]** avec Pi IP adresse ou nom d’hôte que vous obtenez en exécutant hello `devdisco list --eth` commande.</span><span class="sxs-lookup"><span data-stu-id="86daa-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running hello `devdisco list --eth` command.</span></span>
* <span data-ttu-id="86daa-137">Remplacez **[chaîne de connexion de périphérique IoT]** avec la chaîne de connexion de périphérique hello que vous obtenez en exécutant hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` commande.</span><span class="sxs-lookup"><span data-stu-id="86daa-137">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="86daa-138">Remplacez **[chaîne de connexion de hub IoT]** avec hello chaîne de connexion de hub IoT que vous obtenez en exécutant hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` commande.</span><span class="sxs-lookup"><span data-stu-id="86daa-138">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="86daa-139">Exécutez également **gulp install-tools**, si vous ne l’avez pas fait dans la leçon 1.</span><span class="sxs-lookup"><span data-stu-id="86daa-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="86daa-140">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="86daa-140">Deploy and run hello sample application</span></span>
<span data-ttu-id="86daa-141">Déployer et exécuter l’exemple d’application hello sur Pi en exécutant hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="86daa-141">Deploy and run hello sample application on Pi by running hello following commands:</span></span>

```
gulp deploy && gulp run
```

<span data-ttu-id="86daa-142">exécution de la commande Hello gulp hello tâche d’installer les outils de tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="86daa-142">hello gulp command runs hello install-tools task first.</span></span> <span data-ttu-id="86daa-143">Il déploie ensuite tooPi d’application exemple hello.</span><span class="sxs-lookup"><span data-stu-id="86daa-143">Then it deploys hello sample application tooPi.</span></span> <span data-ttu-id="86daa-144">Enfin, elle s’exécute l’application hello sur Pi et une tâche distincte sur votre hôte ordinateur toosend 20 blink messages tooPi votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="86daa-144">Finally, it runs hello application on Pi and a separate task on your host computer toosend 20 blink messages tooPi from your IoT hub.</span></span>

<span data-ttu-id="86daa-145">Après l’exécution de l’exemple d’application hello, il commence à écouter toomessages à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="86daa-145">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="86daa-146">Pendant ce temps, tâche de gulp hello envoie plusieurs messages « clignoter » à partir de votre tooPi de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="86daa-146">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooPi.</span></span> <span data-ttu-id="86daa-147">Pour chaque message blink qui reçoit de Pi, exemple d’application hello appelle hello `blinkLED` hello tooblink de fonction DEL.</span><span class="sxs-lookup"><span data-stu-id="86daa-147">For each blink message that Pi receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="86daa-148">Vous devez voir clignotement de LED hello toutes les deux secondes comme hello gulp la tâche envoie des messages à partir de votre tooPi de hub IoT 20.</span><span class="sxs-lookup"><span data-stu-id="86daa-148">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooPi.</span></span> <span data-ttu-id="86daa-149">Hello dernier un est un message « arrêter » qui arrête l’application hello de s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="86daa-149">hello last one is a "stop" message that stops hello application from running.</span></span>

![Exemple d’application avec la commande gulp et les messages de clignotement](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a><span data-ttu-id="86daa-151">Résumé</span><span class="sxs-lookup"><span data-stu-id="86daa-151">Summary</span></span>
<span data-ttu-id="86daa-152">Vous avez correctement envoyé des messages à partir de votre hello dans IoT hub tooPi tooblink DEL.</span><span class="sxs-lookup"><span data-stu-id="86daa-152">You’ve successfully sent messages from your IoT hub tooPi tooblink hello LED.</span></span> <span data-ttu-id="86daa-153">la tâche suivante Hello est facultative : modifier hello et désactiver le comportement de hello DEL.</span><span class="sxs-lookup"><span data-stu-id="86daa-153">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86daa-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="86daa-154">Next steps</span></span>
[<span data-ttu-id="86daa-155">Modifier hello et désactiver le comportement de hello DEL</span><span class="sxs-lookup"><span data-stu-id="86daa-155">Change hello on and off behavior of hello LED</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
