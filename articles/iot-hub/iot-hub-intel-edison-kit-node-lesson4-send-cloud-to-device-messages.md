---
title: "Connecter Intel Edison (Node) à Azure IoT - Leçon 4 : Recevoir des messages | Microsoft Docs"
description: "Un exemple d’application s’exécute sur Edison et surveille les messages entrants à partir de votre IoT Hub. Une nouvelle tâche gulp envoie des messages à Edison à partir de votre IoT Hub pour faire clignoter la LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "contrôle de la led avec arduino à partir du web, contrôle de la led avec arduino via le web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 76ea59acd848f60663a0c821bff42166aac5823a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="a320e-105">Exécution d’un exemple d’application pour recevoir des messages cloud-à-appareil</span><span class="sxs-lookup"><span data-stu-id="a320e-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="a320e-106">Dans cet article, vous déployez un exemple d’application sur Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="a320e-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="a320e-107">L’exemple d’application surveille les messages entrants à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a320e-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="a320e-108">Vous exécutez également une tâche gulp sur votre ordinateur pour envoyer des messages à Edison à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a320e-108">You also run a gulp task on your computer to send messages to Edison from your IoT hub.</span></span> <span data-ttu-id="a320e-109">À la réception des messages, l’exemple d’application fait clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="a320e-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="a320e-110">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a320e-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a320e-111">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="a320e-111">What you will do</span></span>
* <span data-ttu-id="a320e-112">Connectez l’exemple d’application à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a320e-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="a320e-113">Déployez et exécutez l'exemple d'application.</span><span class="sxs-lookup"><span data-stu-id="a320e-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="a320e-114">Envoyez des messages à partir de votre IoT Hub vers Edison pour faire clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="a320e-114">Send messages from your IoT hub to Edison to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a320e-115">Contenu</span><span class="sxs-lookup"><span data-stu-id="a320e-115">What you will learn</span></span>
<span data-ttu-id="a320e-116">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a320e-116">In this article, you will learn:</span></span>
* <span data-ttu-id="a320e-117">Surveillance des messages entrants à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a320e-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="a320e-118">Envoi de messages cloud-à-appareil à partir de votre IoT Hub vers Edison.</span><span class="sxs-lookup"><span data-stu-id="a320e-118">How to send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a320e-119">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="a320e-119">What you need</span></span>
* <span data-ttu-id="a320e-120">Intel Edison, configuré et prêt à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="a320e-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="a320e-121">Pour savoir comment configurer Edison, consultez [Configuration de votre appareil][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="a320e-121">To learn how to set up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="a320e-122">Un IoT Hub créé dans le cadre de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a320e-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="a320e-123">Pour savoir comment créer votre Azure IoT Hub, consultez [Création de votre Azure IoT Hub][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="a320e-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="a320e-124">Connexion de l’exemple d’application à votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="a320e-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="a320e-125">Assurez-vous que vous êtes dans le dossier du référentiel `iot-hub-node-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="a320e-125">Make sure that you're in the repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="a320e-126">Ouvrez l’exemple d’application dans Visual Studio Code en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a320e-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="a320e-127">Le fichier du sous-dossier `app` est le fichier source clé qui contient le code permettant de surveiller les messages entrants à partir du IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a320e-127">The file in the `app` subfolder is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="a320e-128">La fonction `blinkLED` fait clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="a320e-128">The `blinkLED` function blinks the LED.</span></span>

   ![Structure de référentiel dans l’exemple d’application][repo-structure]
2. <span data-ttu-id="a320e-130">Initialisez le fichier de configuration en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a320e-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="a320e-131">Si vous avez effectué les étapes de la section [Créer une application de fonction Azure et un compte de stockage][create-an-azure-function-app-and-storage-account] sur cet ordinateur, toutes les configurations sont héritées, donc vous pouvez passer à la tâche de déploiement et d’exécution de l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="a320e-131">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="a320e-132">Si vous avez effectué les étapes de la section [Créer une application de fonction Azure et un compte de stockage][create-an-azure-function-app-and-storage-account] sur un autre ordinateur, vous devez remplacer les espaces réservés dans le fichier `config-edison.json`.</span><span class="sxs-lookup"><span data-stu-id="a320e-132">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-edison.json` file.</span></span> <span data-ttu-id="a320e-133">Le fichier `config-edison.json` se trouve dans le sous-dossier de votre dossier racine.</span><span class="sxs-lookup"><span data-stu-id="a320e-133">The `config-edison.json` file is in the subfolder of your home folder.</span></span>

   ![Contenu du fichier config-edison.json](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="a320e-135">Remplacez **[nom d’hôte ou adresse IP de l’appareil]** par l’adresse IP d’appareil obtenue lorsque vous avez configuré votre appareil.</span><span class="sxs-lookup"><span data-stu-id="a320e-135">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="a320e-136">Remplacez **[chaîne de connexion d’appareil IoT]** par la chaîne de connexion d’appareil que vous obtenez en exécutant la commande `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}`.</span><span class="sxs-lookup"><span data-stu-id="a320e-136">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="a320e-137">Remplacez **[chaîne de connexion d’IoT Hub]** par la chaîne de connexion IoT Hub que vous obtenez en exécutant la commande `az iot hub show-connection-string --name {my hub name}`.</span><span class="sxs-lookup"><span data-stu-id="a320e-137">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="a320e-138">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="a320e-138">Deploy and run the sample application</span></span>
<span data-ttu-id="a320e-139">Déployez et exécutez l’exemple d’application sur Edison en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a320e-139">Deploy and run the sample application on Edison by running the following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="a320e-140">La commande gulp déploie l’exemple d’application sur Edison.</span><span class="sxs-lookup"><span data-stu-id="a320e-140">The gulp command deploys the sample application to Edison.</span></span> <span data-ttu-id="a320e-141">Ensuite, elle exécute l’application sur Edison et une tâche distincte sur votre ordinateur hôte afin d’envoyer 20 messages de clignotement à Edison à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a320e-141">Then, it runs the application on Edison and a separate task on your host computer to send 20 blink messages to Edison from your IoT hub.</span></span>

<span data-ttu-id="a320e-142">Une fois l’exemple d’application exécuté, il commence à écouter les messages à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a320e-142">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="a320e-143">Pendant ce temps, la tâche gulp envoie plusieurs messages de « clignotement » à partir de votre IoT Hub vers Edison.</span><span class="sxs-lookup"><span data-stu-id="a320e-143">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Edison.</span></span> <span data-ttu-id="a320e-144">Pour chaque message de clignotement reçu par Edison, l’exemple d’application demande à la fonction `blinkLED` de faire clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="a320e-144">For each blink message that Edison receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="a320e-145">La LED doit clignoter toutes les deux secondes tandis que la tâche gulp envoie 20 messages de votre IoT Hub vers Edison.</span><span class="sxs-lookup"><span data-stu-id="a320e-145">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Edison.</span></span> <span data-ttu-id="a320e-146">Le dernier message est un message « stop » qui interrompt l’exécution de l’application.</span><span class="sxs-lookup"><span data-stu-id="a320e-146">The last one is a "stop" message that stops the application from running.</span></span>

![Exemple d’application avec la commande gulp et les messages de clignotement][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="a320e-148">Résumé</span><span class="sxs-lookup"><span data-stu-id="a320e-148">Summary</span></span>
<span data-ttu-id="a320e-149">Vous avez correctement envoyé des messages à partir de votre IoT Hub vers Edison pour faire clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="a320e-149">You’ve successfully sent messages from your IoT hub to Edison to blink the LED.</span></span> <span data-ttu-id="a320e-150">La tâche suivante est facultative : modifier le comportement activé/désactivé de la LED.</span><span class="sxs-lookup"><span data-stu-id="a320e-150">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a320e-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a320e-151">Next steps</span></span>
<span data-ttu-id="a320e-152">[Modification du comportement activé/désactivé de la LED][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="a320e-152">[Change the on and off behavior of the LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md