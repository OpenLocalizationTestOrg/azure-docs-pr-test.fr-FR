---
featureFlags: usabilla
title: "Connecter Raspberry Pi (Node) à Azure IoT - Leçon 1 : Déployer une application | Microsoft Docs"
description: "Clonez l’exemple d’application Node.js à partir de GitHub et utilisez gulp pour déployer cette application sur votre carte Raspberry Pi 3. Avec cet exemple d’application, la LED connectée à la carte clignote toutes les deux secondes."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: raspberry pi led clignotante, led clignotante avec raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: a5a03a57-fe86-416f-90ff-6eca17775842
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8b73000c166950172c07b8e188025dc9da5bc011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="b8974-105">Créer et déployer l’application blink</span><span class="sxs-lookup"><span data-stu-id="b8974-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="b8974-106">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="b8974-106">What you will do</span></span>
<span data-ttu-id="b8974-107">Clonez l’exemple d’application Node.js à partir de GitHub et utilisez l’outil gulp pour le déployer sur votre Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="b8974-107">Clone the sample Node.js application from GitHub and use the gulp tool to deploy the sample application to your Raspberry Pi 3.</span></span> <span data-ttu-id="b8974-108">Avec cet exemple d’application, la LED connectée à la carte clignote toutes les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="b8974-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="b8974-109">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b8974-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b8974-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="b8974-110">What you will learn</span></span>
<span data-ttu-id="b8974-111">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b8974-111">In this article, you will learn:</span></span>

* <span data-ttu-id="b8974-112">Utilisation de l’outil `device-discover-cli` pour récupérer des informations de mise en réseau sur Pi.</span><span class="sxs-lookup"><span data-stu-id="b8974-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span></span>
* <span data-ttu-id="b8974-113">Déploiement et exécution de l’exemple d’application sur Pi.</span><span class="sxs-lookup"><span data-stu-id="b8974-113">How to deploy and run the sample application on Pi.</span></span>
* <span data-ttu-id="b8974-114">Déploiement et débogage des applications en cours d’exécution à distance sur Pi.</span><span class="sxs-lookup"><span data-stu-id="b8974-114">How to deploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b8974-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="b8974-115">What you need</span></span>
<span data-ttu-id="b8974-116">Vous devez avoir terminé les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b8974-116">You must have successfully completed the following operations:</span></span>

* [<span data-ttu-id="b8974-117">Configuration de votre appareil</span><span class="sxs-lookup"><span data-stu-id="b8974-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [<span data-ttu-id="b8974-118">Obtention des outils</span><span class="sxs-lookup"><span data-stu-id="b8974-118">Get the tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a><span data-ttu-id="b8974-119">Obtention de l’adresse IP et du nom d’hôte de Pi</span><span class="sxs-lookup"><span data-stu-id="b8974-119">Obtain the IP address and host name of Pi</span></span>
<span data-ttu-id="b8974-120">Ouvrez une invite de commandes dans Windows ou une fenêtre de terminal dans Mac OS ou Ubuntu, puis exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b8974-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="b8974-121">Le résultat doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="b8974-121">You should see an output that is similar to the following:</span></span>

![Découverte de l’appareil](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="b8974-123">Notez l’`IP address` et le `hostname` de Pi.</span><span class="sxs-lookup"><span data-stu-id="b8974-123">Take note of the `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="b8974-124">Ces informations vous seront nécessaires plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="b8974-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="b8974-125">Assurez-vous que Pi est connecté au même réseau que votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b8974-125">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="b8974-126">Par exemple, si votre ordinateur est connecté à un réseau sans fil alors que Pi est connecté à un réseau câblé, il se peut que vous ne voyiez pas l’adresse IP dans la sortie devdisco.</span><span class="sxs-lookup"><span data-stu-id="b8974-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="b8974-127">Clonage de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="b8974-127">Clone the sample application</span></span>
<span data-ttu-id="b8974-128">Procédez comme suit pour ouvrir l’exemple de code :</span><span class="sxs-lookup"><span data-stu-id="b8974-128">To open the sample code, follow these steps:</span></span>

1. <span data-ttu-id="b8974-129">Clonez l’exemple de référentiel à partir de GitHub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b8974-129">Clone the sample repository from GitHub by running the following command:</span></span>
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. <span data-ttu-id="b8974-130">Ouvrez l’exemple d’application dans Visual Studio Code en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b8974-130">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Structure du référentiel](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

<span data-ttu-id="b8974-132">Le fichier `app.js` dans le sous-dossier `app` est le fichier source clé qui contient le code pour contrôler la LED.</span><span class="sxs-lookup"><span data-stu-id="b8974-132">The `app.js` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="b8974-133">Installation des dépendances de l’application</span><span class="sxs-lookup"><span data-stu-id="b8974-133">Install application dependencies</span></span>
<span data-ttu-id="b8974-134">Installez les bibliothèques et d’autres modules dont vous avez besoin pour l’exemple d’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b8974-134">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="b8974-135">Configuration de la connexion de l’appareil</span><span class="sxs-lookup"><span data-stu-id="b8974-135">Configure the device connection</span></span>
<span data-ttu-id="b8974-136">Procédez comme suit pour configurer la connexion de l’appareil :</span><span class="sxs-lookup"><span data-stu-id="b8974-136">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="b8974-137">Générez le fichier de configuration de votre appareil en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b8974-137">Generate the device configuration file by running the following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="b8974-138">Le fichier de configuration `config-raspberrypi.json` contient les informations d’identification utilisateur que vous utilisez pour vous connecter à Pi.</span><span class="sxs-lookup"><span data-stu-id="b8974-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span></span> <span data-ttu-id="b8974-139">Pour éviter la fuite d’informations d’identification de l’utilisateur, le fichier de configuration est généré dans le sous-dossier `.iot-hub-getting-started` du dossier de base de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b8974-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="b8974-140">Ouvrez le fichier de configuration de votre appareil dans Visual Studio Code en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b8974-140">Open the device configuration file in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. <span data-ttu-id="b8974-141">Remplacez l’espace réservé `[device hostname or IP address]` par l’adresse IP ou le nom d’hôte que vous avez obtenu précédemment dans « Obtention de l’adresse IP et du nom d’hôte de Pi ».</span><span class="sxs-lookup"><span data-stu-id="b8974-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span></span>
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="b8974-143">Lors de la connexion à Raspberry Pi, vous pouvez utiliser une clé SSH au lieu du nom d’utilisateur et du mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b8974-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span></span> <span data-ttu-id="b8974-144">Pour cela, vous devez générer la clé à l’aide **ssh-keygen** et **pi ssh-copy-id @\<adresse du périphérique\>**.</span><span class="sxs-lookup"><span data-stu-id="b8974-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="b8974-145">Sous Windows, ces commandes sont disponibles dans **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="b8974-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="b8974-146">Sous Mac OS, vous devez exécuter **brew install ssh-copy-id**.</span><span class="sxs-lookup"><span data-stu-id="b8974-146">On MacOS you need to run **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="b8974-147">Après avoir téléchargé la clé de Raspberry Pi, remplacez **device_password** par la propriété **device_key_path** dans **config-raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="b8974-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="b8974-148">Les lignes mises à jour doivent se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8974-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="b8974-149">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="b8974-149">Congratulations!</span></span> <span data-ttu-id="b8974-150">Vous avez créé le premier exemple d’application pour Pi.</span><span class="sxs-lookup"><span data-stu-id="b8974-150">You've successfully created the first sample application for Pi.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="b8974-151">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="b8974-151">Deploy and run the sample application</span></span>
### <a name="install-nodejs-and-npm-on-pi"></a><span data-ttu-id="b8974-152">Installez Node.js et NPM sur Pi</span><span class="sxs-lookup"><span data-stu-id="b8974-152">Install Node.js and NPM on Pi</span></span>
<span data-ttu-id="b8974-153">Installez Node.js et NPM sur Pi en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b8974-153">Install Node.js and NPM on Pi by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="b8974-154">La première exécution de cette tâche peut prendre jusqu’à 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="b8974-154">This task might take 10 minutes to complete the first time you run it.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="b8974-155">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="b8974-155">Deploy and run the sample app</span></span>
<span data-ttu-id="b8974-156">Déployez et exécutez l’exemple d’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b8974-156">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="b8974-157">Vérification du bon fonctionnement de l’application</span><span class="sxs-lookup"><span data-stu-id="b8974-157">Verify the app works</span></span>
<span data-ttu-id="b8974-158">Vous devez maintenant voir la LED sur Pi clignoter toutes les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="b8974-158">You should now see the LED on Pi blinking every two seconds.</span></span>  <span data-ttu-id="b8974-159">Si vous ne voyez pas la LED clignoter, consultez le [guide de dépannage](iot-hub-raspberry-pi-kit-node-troubleshooting.md) des problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="b8974-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>
<span data-ttu-id="b8974-160">![LED clignotante](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="b8974-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="b8974-161">Résumé</span><span class="sxs-lookup"><span data-stu-id="b8974-161">Summary</span></span>
<span data-ttu-id="b8974-162">Vous avez installé les outils nécessaires pour travailler avec Pi et déployé un exemple d’application sur Pi pour faire clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="b8974-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span></span> <span data-ttu-id="b8974-163">Vous pouvez maintenant créer, déployer et exécuter un autre exemple d’application qui connecte Pi à Azure IoT Hub pour envoyer et recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="b8974-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8974-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b8974-164">Next steps</span></span>
[<span data-ttu-id="b8974-165">Obtenir les outils Azure</span><span class="sxs-lookup"><span data-stu-id="b8974-165">Get the Azure tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

