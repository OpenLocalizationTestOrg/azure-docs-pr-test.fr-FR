---
title: "Connecter Arduino à Azure IoT - Leçon 1 : Déployer une application | Microsoft Docs"
description: "Clonez l’exemple d’application Arduino à partir de GitHub et exécutez gulp pour déployer cette application sur votre carte Adafruit Feather M0 WiFi. Cet exemple d’application fait clignoter la LED GPIO"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: projets de led arduino, clignotement de led arduino, code de clignotement de led arduino, programme de clignotement arduino, exemple de clignotement arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4431808ac6182d194e841c087c8f89f1a12b1911
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="8d91d-105">Créer et déployer l’application blink</span><span class="sxs-lookup"><span data-stu-id="8d91d-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="8d91d-106">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="8d91d-106">What you will do</span></span>
<span data-ttu-id="8d91d-107">Clonez l’exemple d’application Arduino à partir de GitHub et utilisez l'outil gulp pour déployer l'exemple d'application sur votre carte Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="8d91d-107">Clone the sample Arduino application from GitHub, and use the gulp tool to deploy the sample application to your Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="8d91d-108">Avec l'exemple d’application, la LED embarquée GPIO #13 clignote toutes les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="8d91d-108">The sample application blinks the GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="8d91d-109">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="8d91d-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8d91d-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="8d91d-110">What you will learn</span></span>
* <span data-ttu-id="8d91d-111">Comment déployer et exécuter l’exemple d’application sur votre carte Arduino.</span><span class="sxs-lookup"><span data-stu-id="8d91d-111">How to deploy and run the sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8d91d-112">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="8d91d-112">What you need</span></span>
<span data-ttu-id="8d91d-113">Vous devez avoir terminé les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8d91d-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="8d91d-114">[Configuration de votre appareil][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="8d91d-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="8d91d-115">[Obtenir les outils][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="8d91d-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="8d91d-116">Ouvrir l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="8d91d-116">Open the sample application</span></span>
<span data-ttu-id="8d91d-117">Procédez comme suit pour ouvrir l’exemple d’application :</span><span class="sxs-lookup"><span data-stu-id="8d91d-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="8d91d-118">Clonez l’exemple de référentiel à partir de GitHub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8d91d-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="8d91d-119">Ouvrez l’exemple d’application dans Visual Studio Code en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8d91d-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Structure du référentiel][repo-structure]

<span data-ttu-id="8d91d-121">Le fichier `app.ino` dans le sous-dossier `app` est le fichier source clé qui contient le code pour contrôler la LED.</span><span class="sxs-lookup"><span data-stu-id="8d91d-121">The `app.ino` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="8d91d-122">Installation des dépendances de l’application</span><span class="sxs-lookup"><span data-stu-id="8d91d-122">Install application dependencies</span></span>
<span data-ttu-id="8d91d-123">Installez les bibliothèques et d’autres modules dont vous avez besoin pour l’exemple d’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8d91d-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="8d91d-124">Configuration de la connexion de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8d91d-124">Configure the device connection</span></span>
<span data-ttu-id="8d91d-125">Procédez comme suit pour configurer la connexion de l’appareil :</span><span class="sxs-lookup"><span data-stu-id="8d91d-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="8d91d-126">Obtenez le port série de l'appareil à l'aide de l’interface de ligne de commande de découverte :</span><span class="sxs-lookup"><span data-stu-id="8d91d-126">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="8d91d-127">Vous devriez obtenir un résultat semblable à ce qui suit et identifier le port USB COM de votre carte Arduino : ![Découverte de l’appareil][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="8d91d-127">You should see an output that is similar to the following and find the usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="8d91d-128">Ouvrez le fichier `config.json` dans le dossier de la leçon puis ajoutez la valeur du numéro de port COM trouvé :</span><span class="sxs-lookup"><span data-stu-id="8d91d-128">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > <span data-ttu-id="8d91d-130">Sur la plate-forme Windows, le port COM le format `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="8d91d-130">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="8d91d-131">Sur macOS ou Ubuntu, il commence par `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="8d91d-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="8d91d-132">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="8d91d-132">Deploy and run the sample application</span></span>
### <a name="install-the-required-tools-for-your-arduino-board"></a><span data-ttu-id="8d91d-133">Installation des outils requis pour votre carte Arduino</span><span class="sxs-lookup"><span data-stu-id="8d91d-133">Install the required tools for your Arduino board</span></span>

<span data-ttu-id="8d91d-134">Installez le kit de développement logiciel (SDK) Azure IoT Hub sur votre carte Arduino en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8d91d-134">Install the Azure IoT Hub SDK for your Arduino board by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="8d91d-135">Cette tâche peut prendre beaucoup de temps en fonction de votre connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="8d91d-135">This task might take a long time to complete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="8d91d-136">Veuillez quitter l’instance Arduino IDE en cours lors de l’exécution des tâches gulp : `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="8d91d-136">Please exit the running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="8d91d-137">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="8d91d-137">Deploy and run the sample app</span></span>
<span data-ttu-id="8d91d-138">Déployez et exécutez l’exemple d’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8d91d-138">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp run

# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-the-app-works"></a><span data-ttu-id="8d91d-139">Vérification du bon fonctionnement de l’application</span><span class="sxs-lookup"><span data-stu-id="8d91d-139">Verify the app works</span></span>
<span data-ttu-id="8d91d-140">Si vous ne voyez pas la LED clignoter, consultez le [guide de dépannage][troubleshooting-page] des problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="8d91d-140">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting-page] for solutions to common problems.</span></span>

![LED clignotante][led-blinking]

## <a name="summary"></a><span data-ttu-id="8d91d-142">Résumé</span><span class="sxs-lookup"><span data-stu-id="8d91d-142">Summary</span></span>
<span data-ttu-id="8d91d-143">Vous avez installé les outils nécessaires pour travailler avec votre carte Arduino et déployé un exemple d’application sur votre carte Arduino pour faire clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="8d91d-143">You've installed the required tools to work with your Arduino board and deployed a sample application to your Arduino board to blink the LED.</span></span> <span data-ttu-id="8d91d-144">Vous pouvez maintenant créer, déployer et exécuter un autre exemple d’application qui connecte votre carte Arduino à Azure IoT Hub pour envoyer et recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="8d91d-144">You can now create, deploy, and run another sample application that connects your Arduino board to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d91d-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8d91d-145">Next steps</span></span>
<span data-ttu-id="8d91d-146">[Obtenir les outils Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="8d91d-146">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md