---
title: "Connect Arduino (C) tooAzure IoT - leçon 4 : Cloud-à-appareil | Documents Microsoft"
description: "Un exemple d’application s’exécute sur la carte Adafruit Feather M0 WiFi et surveille les messages entrants à partir de votre IoT Hub. Une nouvelle tâche gulp envoie des messages tooAdafruit estompe M0 WiFi à partir de votre hello tooblink du hub IoT DEL."
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
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="56fbd-105">Exécuter un tooreceive d’application exemple messages cloud-à-appareil</span><span class="sxs-lookup"><span data-stu-id="56fbd-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="56fbd-106">Dans cet article, vous déployez un exemple d’application sur votre carte Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="56fbd-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="56fbd-107">exemple d’application Hello surveille les messages entrants à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="56fbd-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="56fbd-108">Aussi, vous exécutez une tâche de gulp sur votre ordinateur ordinateur toosend messages tooyour Arduino tableau à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="56fbd-108">You also run a gulp task on your computer toosend messages tooyour Arduino board from your IoT hub.</span></span> <span data-ttu-id="56fbd-109">Lors de l’application d’exemple hello reçoit des messages hello, il clignote hello DEL.</span><span class="sxs-lookup"><span data-stu-id="56fbd-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="56fbd-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="56fbd-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="56fbd-111">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="56fbd-111">What you will do</span></span>
* <span data-ttu-id="56fbd-112">Connectez le hub IoT tooyour hello exemple application.</span><span class="sxs-lookup"><span data-stu-id="56fbd-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="56fbd-113">Déployer et exécuter l’exemple d’application hello.</span><span class="sxs-lookup"><span data-stu-id="56fbd-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="56fbd-114">Envoyer des messages à partir de votre hello IoT hub tooyour Arduino tableau tooblink DEL.</span><span class="sxs-lookup"><span data-stu-id="56fbd-114">Send messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="56fbd-115">Contenu</span><span class="sxs-lookup"><span data-stu-id="56fbd-115">What you will learn</span></span>
<span data-ttu-id="56fbd-116">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="56fbd-116">In this article, you will learn:</span></span>
* <span data-ttu-id="56fbd-117">Comment les messages entrants de toomonitor à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="56fbd-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="56fbd-118">Comment les messages à partir de votre tooyour de hub IoT Arduino tableau toosend cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="56fbd-118">How toosend cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="56fbd-119">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="56fbd-119">What you need</span></span>
* <span data-ttu-id="56fbd-120">Votre carte Arduino, configurée et prête à l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="56fbd-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="56fbd-121">toolearn tooset de votre tableau Arduino, voir [configurer votre périphérique][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="56fbd-121">toolearn how tooset up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="56fbd-122">Un IoT Hub créé dans le cadre de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="56fbd-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="56fbd-123">toolearn comment toocreate votre IoT hub, consultez [créer votre Azure IoT Hub][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="56fbd-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="56fbd-124">Connecter le hub IoT tooyour hello exemple application</span><span class="sxs-lookup"><span data-stu-id="56fbd-124">Connect hello sample application tooyour IoT hub</span></span>

1. <span data-ttu-id="56fbd-125">Assurez-vous que vous êtes dans le dossier de dépôt hello `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="56fbd-125">Make sure that you're in hello repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="56fbd-126">Ouvrir l’exemple d’application hello dans Visual Studio Code par hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="56fbd-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="56fbd-127">Hello d’avis `app.ino` fichier Bonjour `app` sous-dossier.</span><span class="sxs-lookup"><span data-stu-id="56fbd-127">Notice hello `app.ino` file in hello `app` subfolder.</span></span> <span data-ttu-id="56fbd-128">Hello `app.ino` fichier est le fichier de source de la clé de hello qui contient les messages entrants toomonitor code hello à partir du hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="56fbd-128">hello `app.ino` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="56fbd-129">Hello `blinkLED` fonction clignote hello DEL.</span><span class="sxs-lookup"><span data-stu-id="56fbd-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Structure de référentiel dans l’exemple d’application hello][repo-structure]

2. <span data-ttu-id="56fbd-131">Obtenir le port série de hello du périphérique hello avec cli de découverte de périphérique hello :</span><span class="sxs-lookup"><span data-stu-id="56fbd-131">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="56fbd-132">Vous devez voir une sortie similaire toohello suivant et trouver hello usb port COM de votre carte Arduino :</span><span class="sxs-lookup"><span data-stu-id="56fbd-132">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Découverte de l’appareil][device-discovery]

3. <span data-ttu-id="56fbd-134">Les fichiers ouverts hello `config.json` dans le dossier de leçon hello et valeur d’entrée hello hello trouvé le numéro de port COM :</span><span class="sxs-lookup"><span data-stu-id="56fbd-134">Open hello file `config.json` in hello lesson folder and input hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="56fbd-136">Pour le port COM de hello, sur la plateforme Windows, d’un format de hello `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="56fbd-136">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="56fbd-137">Sur macOS ou Ubuntu, il commence par `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="56fbd-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="56fbd-138">Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="56fbd-138">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="56fbd-139">Rendre hello suivant remplacements Bonjour `config-arduino.json` fichier :</span><span class="sxs-lookup"><span data-stu-id="56fbd-139">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   <span data-ttu-id="56fbd-140">Si vous avez terminé les étapes de hello dans [créer un compte d’application et de stockage Azure fonction] [ create-an-azure-function-app-and-storage-account] sur cet ordinateur, toutes les configurations de hello sont héritées, vous pouvez sauter des tâches de toohello hello étape du déploiement et exemple d’application hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="56fbd-140">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="56fbd-141">Si vous avez terminé les étapes de hello dans [créer un compte d’application et de stockage Azure fonction] [ create-an-azure-function-app-and-storage-account] sur un autre ordinateur, vous avez besoin des espaces réservés de hello tooreplace Bonjour `config-arduino.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="56fbd-141">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-arduino.json` file.</span></span> <span data-ttu-id="56fbd-142">Hello `config-arduino.json` fichier se trouve dans le sous-dossier hello de votre dossier de base.</span><span class="sxs-lookup"><span data-stu-id="56fbd-142">hello `config-arduino.json` file is in hello subfolder of your home folder.</span></span>

   ![Contenu du fichier de configuration-arduino.json hello][config-arduino-json]

   * <span data-ttu-id="56fbd-144">Remplacez **[Wi-Fi SSID]** avec votre SSID Wi-Fi qui connectés toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="56fbd-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="56fbd-145">Remplacez **[Wi-Fi password]** par votre mot de passe Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="56fbd-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="56fbd-146">Supprimez la chaîne de hello si votre Wi-Fi ne nécessite pas un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="56fbd-146">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="56fbd-147">Remplacez **[chaîne de connexion de périphérique IoT]** avec la chaîne de connexion de périphérique hello que vous obtenez en exécutant hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` commande.</span><span class="sxs-lookup"><span data-stu-id="56fbd-147">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="56fbd-148">Remplacez **[chaîne de connexion de hub IoT]** avec hello chaîne de connexion de hub IoT que vous obtenez en exécutant hello `az iot hub show-connection-string --name {my hub name}` commande.</span><span class="sxs-lookup"><span data-stu-id="56fbd-148">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="56fbd-149">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="56fbd-149">Deploy and run hello sample application</span></span>
<span data-ttu-id="56fbd-150">Déployer et exécuter des application d’exemple hello sur votre carte mère Arduino par hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="56fbd-150">Deploy and run hello sample application on your Arduino board by running hello following commands:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="56fbd-151">commande de gulp Hello déploie le tableau Arduino tooyour hello exemple application.</span><span class="sxs-lookup"><span data-stu-id="56fbd-151">hello gulp command deploys hello sample application tooyour Arduino board.</span></span> <span data-ttu-id="56fbd-152">Il exécute ensuite application hello sur votre carte mère Arduino et une tâche distincte sur votre hôte tooyour Arduino carte pour ordinateur toosend 20 blink messages à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="56fbd-152">Then, it runs hello application on your Arduino board and a separate task on your host computer toosend 20 blink messages tooyour Arduino board from your IoT hub.</span></span>

<span data-ttu-id="56fbd-153">Après l’exécution de l’exemple d’application hello, il commence à écouter toomessages à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="56fbd-153">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="56fbd-154">Pendant ce temps, tâche de gulp de hello envoie plusieurs messages « clignoter » à partir de votre tooyour de hub IoT Arduino carte.</span><span class="sxs-lookup"><span data-stu-id="56fbd-154">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="56fbd-155">Pour chaque message blink hello carte reçoit, exemple d’application hello appelle hello `blinkLED` hello tooblink de fonction DEL.</span><span class="sxs-lookup"><span data-stu-id="56fbd-155">For each blink message that hello board receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="56fbd-156">Vous devez voir hello LED clignote toutes les deux secondes comme tâche de gulp hello envoie des messages de 20 à partir de votre tooyour de hub IoT Arduino carte.</span><span class="sxs-lookup"><span data-stu-id="56fbd-156">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="56fbd-157">Hello dernier un est un message « arrêter » qui arrête l’application hello de s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="56fbd-157">hello last one is a "stop" message that stops hello application from running.</span></span>

![Exemple d’application avec la commande gulp et les messages de clignotement][sample-application]

## <a name="summary"></a><span data-ttu-id="56fbd-159">Résumé</span><span class="sxs-lookup"><span data-stu-id="56fbd-159">Summary</span></span>
<span data-ttu-id="56fbd-160">Vous avez correctement envoyé des messages à partir de votre hello IoT hub tooyour Arduino tableau tooblink DEL.</span><span class="sxs-lookup"><span data-stu-id="56fbd-160">You’ve successfully sent messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="56fbd-161">la tâche suivante Hello est facultative : modifier hello et désactiver le comportement de hello DEL.</span><span class="sxs-lookup"><span data-stu-id="56fbd-161">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56fbd-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56fbd-162">Next steps</span></span>
<span data-ttu-id="56fbd-163">[Modifier hello et désactiver le comportement de hello DEL][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="56fbd-163">[Change hello on and off behavior of hello LED][change-the-on-and-off-led-behavior]</span></span>


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