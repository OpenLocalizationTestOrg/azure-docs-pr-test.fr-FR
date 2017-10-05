---
title: "Connecter Raspberry Pi (C) à Azure IoT - Leçon 4 : Cloud-à-appareil | Microsoft Docs"
description: "Un exemple d’application s’exécute sur Pi et surveille les messages entrants à partir de votre IoT Hub. Une nouvelle tâche gulp envoie des messages à Pi à partir de votre IoT Hub pour faire clignoter la LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "cloud-à-appareil, message du cloud"
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
ms.openlocfilehash: 86c7be931319d9995c2a7311267c7e7c03c3c1b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="9fe8c-105">Exécution d’un exemple d’application pour recevoir des messages cloud-à-appareil</span><span class="sxs-lookup"><span data-stu-id="9fe8c-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="9fe8c-106">Dans cet article, vous déployez un exemple d’application sur Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="9fe8c-107">L’exemple d’application surveille les messages entrants à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="9fe8c-108">Vous exécutez également une tâche gulp sur votre ordinateur pour envoyer des messages à Pi à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span></span> <span data-ttu-id="9fe8c-109">À la réception des messages, l’exemple d’application fait clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="9fe8c-110">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9fe8c-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9fe8c-111">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="9fe8c-111">What you will do</span></span>
* <span data-ttu-id="9fe8c-112">Connectez l’exemple d’application à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="9fe8c-113">Déployez et exécutez l'exemple d'application.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="9fe8c-114">Envoyez des messages à partir votre IoT Hub vers Pi pour faire clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-114">Send messages from your IoT hub to Pi to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9fe8c-115">Contenu</span><span class="sxs-lookup"><span data-stu-id="9fe8c-115">What you will learn</span></span>
<span data-ttu-id="9fe8c-116">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9fe8c-116">In this article, you will learn:</span></span>
* <span data-ttu-id="9fe8c-117">Surveillance des messages entrants à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="9fe8c-118">Envoi de messages cloud-à-appareil à partir de votre IoT Hub vers Pi.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-118">How to send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9fe8c-119">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="9fe8c-119">What you need</span></span>
* <span data-ttu-id="9fe8c-120">Raspberry Pi 3, configuré pour utilisation.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="9fe8c-121">Pour savoir comment configurer Pi, consultez [Configuration de votre appareil](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="9fe8c-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="9fe8c-122">Un IoT Hub créé dans le cadre de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="9fe8c-123">Pour savoir comment créer votre IoT Hub, consultez [Création de votre IoT Hub et inscription de Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="9fe8c-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="9fe8c-124">Connexion de l’exemple d’application à votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="9fe8c-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="9fe8c-125">Assurez-vous que vous êtes dans le dossier du référentiel `iot-hub-c-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-125">Make sure that you're in the repo folder `iot-hub-c-raspberrypi-getting-started`.</span></span> <span data-ttu-id="9fe8c-126">Ouvrez l’exemple d’application dans Visual Studio Code en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9fe8c-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="9fe8c-127">Notez la présence du fichier `app.c` dans le sous-dossier `app`.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-127">Notice the `app.c` file in the `app` subfolder.</span></span> <span data-ttu-id="9fe8c-128">Le fichier `app.c` est le fichier source clé qui contient le code permettant de surveiller les messages entrants à partir du IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-128">The `app.c` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="9fe8c-129">La fonction `blinkLED` fait clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-129">The `blinkLED` function blinks the LED.</span></span>

   ![Structure de référentiel dans l’exemple d’application](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. <span data-ttu-id="9fe8c-131">Initialisez le fichier de configuration en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9fe8c-131">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="9fe8c-132">Si vous avez effectué les étapes de la section [Créer une application de fonction Azure et un compte de stockage](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) sur cet ordinateur, toutes les configurations sont héritées, donc vous pouvez passer à la tâche de déploiement et d’exécution de l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="9fe8c-133">Si vous avez effectué les étapes de la section [Créer une application de fonction Azure et un compte de stockage](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) sur un autre ordinateur, vous devez remplacer les espaces réservés dans le fichier `config-raspberrypi.json`.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span></span> <span data-ttu-id="9fe8c-134">Le fichier `config-raspberrypi.json` se trouve dans le sous-dossier de votre dossier racine.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span></span>

   ![Contenu du fichier config-raspberrypi.json](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="9fe8c-136">Remplacez **[nom d’hôte du périphérique ou adresse IP]** par l’adresse IP ou le nom d’hôte de votre Pi, que vous obtenez en exécutant la commande `devdisco list --eth`.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running the `devdisco list --eth` command.</span></span>
* <span data-ttu-id="9fe8c-137">Remplacez **[chaîne de connexion d’appareil IoT]** par la chaîne de connexion d’appareil que vous obtenez en exécutant la commande `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="9fe8c-138">Remplacez **[chaîne de connexion d’IoT Hub]** par la chaîne de connexion IoT Hub que vous obtenez en exécutant la commande `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="9fe8c-139">Exécutez également **gulp install-tools**, si vous ne l’avez pas fait dans la leçon 1.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="9fe8c-140">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="9fe8c-140">Deploy and run the sample application</span></span>
<span data-ttu-id="9fe8c-141">Déployez et exécutez l’exemple d’application sur Pi en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9fe8c-141">Deploy and run the sample application on Pi by running the following commands:</span></span>

```
gulp deploy && gulp run
```

<span data-ttu-id="9fe8c-142">La commande gulp exécute d’abord la tâche d’installation des outils.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-142">The gulp command runs the install-tools task first.</span></span> <span data-ttu-id="9fe8c-143">Elle déploie ensuite l’exemple d’application sur Pi.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-143">Then it deploys the sample application to Pi.</span></span> <span data-ttu-id="9fe8c-144">Enfin, elle exécute l’application sur Pi et une tâche distincte sur votre ordinateur hôte afin d’envoyer 20 messages de clignotement à Pi à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-144">Finally, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span></span>

<span data-ttu-id="9fe8c-145">Une fois l’exemple d’application exécuté, il commence à écouter les messages à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-145">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="9fe8c-146">Pendant ce temps, la tâche gulp envoie plusieurs messages de « clignotement » à partir de votre IoT Hub vers Pi.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-146">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span></span> <span data-ttu-id="9fe8c-147">Pour chaque message de clignotement reçu par Pi, l’exemple d’application demande à la fonction `blinkLED` de faire clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-147">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="9fe8c-148">La LED doit clignoter toutes les deux secondes tandis que la tâche gulp envoie 20 messages de votre IoT Hub vers Pi.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-148">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span></span> <span data-ttu-id="9fe8c-149">Le dernier message est un message « stop » qui interrompt l’exécution de l’application.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-149">The last one is a "stop" message that stops the application from running.</span></span>

![Exemple d’application avec la commande gulp et les messages de clignotement](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a><span data-ttu-id="9fe8c-151">Résumé</span><span class="sxs-lookup"><span data-stu-id="9fe8c-151">Summary</span></span>
<span data-ttu-id="9fe8c-152">Vous avez correctement envoyé des messages à partir de votre IoT Hub vers Pi pour faire clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-152">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span></span> <span data-ttu-id="9fe8c-153">La tâche suivante est facultative : modifier le comportement activé/désactivé de la LED.</span><span class="sxs-lookup"><span data-stu-id="9fe8c-153">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fe8c-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9fe8c-154">Next steps</span></span>
[<span data-ttu-id="9fe8c-155">Modification du comportement activé/désactivé de la LED</span><span class="sxs-lookup"><span data-stu-id="9fe8c-155">Change the on and off behavior of the LED</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
