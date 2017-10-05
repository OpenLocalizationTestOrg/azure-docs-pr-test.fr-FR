---
title: "Connecter Arduino Pi (C) à Azure IoT - Leçon 4 : Cloud-à-appareil | Microsoft Docs"
description: "Un exemple d’application s’exécute sur la carte Adafruit Feather M0 WiFi et surveille les messages entrants à partir de votre IoT Hub. Une nouvelle tâche gulp envoie des messages à la carte Adafruit Feather M0 WiFi à partir de votre IoT Hub pour faire clignoter la LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "contrôle de la led avec arduino à partir du web, contrôle de la led avec arduino via le web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f4c1d86b10b64c104ac812d1f650d723322be8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="07b03-105">Exécution d’un exemple d’application pour recevoir des messages cloud-à-appareil</span><span class="sxs-lookup"><span data-stu-id="07b03-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="07b03-106">Dans cet article, vous déployez un exemple d’application sur votre carte Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="07b03-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="07b03-107">L’exemple d’application surveille les messages entrants à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07b03-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="07b03-108">Vous exécutez également une tâche gulp sur votre ordinateur pour envoyer des messages à votre carte Arduino à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07b03-108">You also run a gulp task on your computer to send messages to your Arduino board from your IoT hub.</span></span> <span data-ttu-id="07b03-109">À la réception des messages, l’exemple d’application fait clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="07b03-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="07b03-110">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="07b03-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="07b03-111">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="07b03-111">What you will do</span></span>
* <span data-ttu-id="07b03-112">Connectez l’exemple d’application à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07b03-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="07b03-113">Déployez et exécutez l'exemple d'application.</span><span class="sxs-lookup"><span data-stu-id="07b03-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="07b03-114">Envoyez des messages depuis votre IoT Hub vers votre carte Arduino pour faire clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="07b03-114">Send messages from your IoT hub to your Arduino board to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="07b03-115">Contenu</span><span class="sxs-lookup"><span data-stu-id="07b03-115">What you will learn</span></span>
<span data-ttu-id="07b03-116">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="07b03-116">In this article, you will learn:</span></span>
* <span data-ttu-id="07b03-117">Surveillance des messages entrants à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07b03-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="07b03-118">Envoi de messages cloud-à-appareil depuis votre IoT Hub vers votre carte Arduino.</span><span class="sxs-lookup"><span data-stu-id="07b03-118">How to send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="07b03-119">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="07b03-119">What you need</span></span>
* <span data-ttu-id="07b03-120">Votre carte Arduino, configurée et prête à l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="07b03-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="07b03-121">Pour savoir comment configurer votre carte Arduino, consultez [Configuration de votre appareil][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="07b03-121">To learn how to set up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="07b03-122">Un IoT Hub créé dans le cadre de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="07b03-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="07b03-123">Pour savoir comment créer votre Azure IoT Hub, consultez [Création de votre Azure IoT Hub][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="07b03-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="07b03-124">Connexion de l’exemple d’application à votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="07b03-124">Connect the sample application to your IoT hub</span></span>

1. <span data-ttu-id="07b03-125">Assurez-vous que vous êtes dans le dossier du référentiel `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="07b03-125">Make sure that you're in the repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="07b03-126">Ouvrez l’exemple d’application dans Visual Studio Code en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="07b03-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="07b03-127">Notez la présence du fichier `app.ino` dans le sous-dossier `app`.</span><span class="sxs-lookup"><span data-stu-id="07b03-127">Notice the `app.ino` file in the `app` subfolder.</span></span> <span data-ttu-id="07b03-128">Le fichier `app.ino` est le fichier source clé qui contient le code permettant de surveiller les messages entrants à partir du IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07b03-128">The `app.ino` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="07b03-129">La fonction `blinkLED` fait clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="07b03-129">The `blinkLED` function blinks the LED.</span></span>

   ![Structure de référentiel dans l’exemple d’application][repo-structure]

2. <span data-ttu-id="07b03-131">Obtenez le port série de l’appareil à l’aide de l’interface de ligne de commande de découverte :</span><span class="sxs-lookup"><span data-stu-id="07b03-131">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="07b03-132">Vous devriez obtenir un résultat semblable à ce qui suit et identifier le port USB COM de votre carte Arduino :</span><span class="sxs-lookup"><span data-stu-id="07b03-132">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Découverte de l’appareil][device-discovery]

3. <span data-ttu-id="07b03-134">Ouvrez le fichier `config.json` dans le dossier de la leçon et entrez la valeur du numéro de port COM trouvé :</span><span class="sxs-lookup"><span data-stu-id="07b03-134">Open the file `config.json` in the lesson folder and input the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="07b03-136">Sur la plateforme Windows, le port COM a le format `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="07b03-136">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="07b03-137">Sur macOS ou Ubuntu, il commence par `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="07b03-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="07b03-138">Initialisez le fichier de configuration en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="07b03-138">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="07b03-139">Dans le fichier `config-arduino.json`, effectuez les remplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="07b03-139">Make the following replacements in the `config-arduino.json` file:</span></span>

   <span data-ttu-id="07b03-140">Si vous avez effectué les étapes de la section [Créer une application de fonction Azure et un compte de stockage][create-an-azure-function-app-and-storage-account] sur cet ordinateur, toutes les configurations sont héritées, donc vous pouvez passer à la tâche de déploiement et d’exécution de l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="07b03-140">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="07b03-141">Si vous avez effectué les étapes de la section [Créer une application de fonction Azure et un compte de stockage][create-an-azure-function-app-and-storage-account] sur un autre ordinateur, vous devez remplacer les espaces réservés dans le fichier `config-arduino.json`.</span><span class="sxs-lookup"><span data-stu-id="07b03-141">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-arduino.json` file.</span></span> <span data-ttu-id="07b03-142">Le fichier `config-arduino.json` se trouve dans le sous-dossier de votre dossier racine.</span><span class="sxs-lookup"><span data-stu-id="07b03-142">The `config-arduino.json` file is in the subfolder of your home folder.</span></span>

   ![Contenu du fichier config-arduino.json][config-arduino-json]

   * <span data-ttu-id="07b03-144">Remplacez **[Wi-Fi SSID]** avec votre SSID Wi-Fi connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="07b03-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="07b03-145">Remplacez **[Wi-Fi password]** par votre mot de passe Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="07b03-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="07b03-146">Supprimez la chaîne si votre réseau Wi-Fi ne requiert aucun mot de passe.</span><span class="sxs-lookup"><span data-stu-id="07b03-146">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="07b03-147">Remplacez **[chaîne de connexion d’appareil IoT]** par la chaîne de connexion d’appareil que vous obtenez en exécutant la commande `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}`.</span><span class="sxs-lookup"><span data-stu-id="07b03-147">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="07b03-148">Remplacez **[chaîne de connexion d’IoT Hub]** par la chaîne de connexion IoT Hub que vous obtenez en exécutant la commande `az iot hub show-connection-string --name {my hub name}`.</span><span class="sxs-lookup"><span data-stu-id="07b03-148">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="07b03-149">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="07b03-149">Deploy and run the sample application</span></span>
<span data-ttu-id="07b03-150">Déployez et exécutez l’exemple d’application sur votre carte Arduino en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="07b03-150">Deploy and run the sample application on your Arduino board by running the following commands:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="07b03-151">La commande gulp déploie l’exemple d’application sur votre carte Arduino.</span><span class="sxs-lookup"><span data-stu-id="07b03-151">The gulp command deploys the sample application to your Arduino board.</span></span> <span data-ttu-id="07b03-152">Ensuite, elle exécute l’application sur votre carte Arduino et une tâche distincte sur votre ordinateur hôte afin d’envoyer 20 messages de clignotement à votre carte Arduino à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07b03-152">Then, it runs the application on your Arduino board and a separate task on your host computer to send 20 blink messages to your Arduino board from your IoT hub.</span></span>

<span data-ttu-id="07b03-153">Une fois l’exemple d’application exécuté, il commence à écouter les messages à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07b03-153">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="07b03-154">Pendant ce temps, la tâche gulp envoie plusieurs messages de « clignotement » à partir de votre IoT Hub vers votre carte Arduino.</span><span class="sxs-lookup"><span data-stu-id="07b03-154">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="07b03-155">Pour chaque message de clignotement reçu par la carte, l’exemple d’application demande à la fonction `blinkLED` de faire clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="07b03-155">For each blink message that the board receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="07b03-156">La LED doit clignoter toutes les deux secondes tandis que la tâche gulp envoie 20 messages de votre IoT Hub vers votre carte Arduino.</span><span class="sxs-lookup"><span data-stu-id="07b03-156">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="07b03-157">Le dernier message est un message « stop » qui interrompt l’exécution de l’application.</span><span class="sxs-lookup"><span data-stu-id="07b03-157">The last one is a "stop" message that stops the application from running.</span></span>

![Exemple d’application avec la commande gulp et les messages de clignotement][sample-application]

## <a name="summary"></a><span data-ttu-id="07b03-159">Résumé</span><span class="sxs-lookup"><span data-stu-id="07b03-159">Summary</span></span>
<span data-ttu-id="07b03-160">Vous avez correctement envoyé des messages à partir de votre IoT Hub vers votre carte Arduino pour faire clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="07b03-160">You’ve successfully sent messages from your IoT hub to your Arduino board to blink the LED.</span></span> <span data-ttu-id="07b03-161">La tâche suivante est facultative : modifier le comportement activé/désactivé de la LED.</span><span class="sxs-lookup"><span data-stu-id="07b03-161">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07b03-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="07b03-162">Next steps</span></span>
<span data-ttu-id="07b03-163">[Modification du comportement activé/désactivé de la LED][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="07b03-163">[Change the on and off behavior of the LED][change-the-on-and-off-led-behavior]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md