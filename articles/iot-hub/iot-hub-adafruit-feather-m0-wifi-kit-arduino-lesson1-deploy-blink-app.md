---
title: "Se connecter Arduino tooAzure IoT - leçon 1 : déploiement d’une application | Documents Microsoft"
description: "Cloner hello exemple Arduino d’application à partir de GitHub et exécutez gulp toodeploy cette tooyour application Adafruit estompe M0 WiFi. Cet exemple d’application clignote hello GPIO"
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
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="4ad45-105">Créer et déployer des applications de clignotement hello</span><span class="sxs-lookup"><span data-stu-id="4ad45-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="4ad45-106">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="4ad45-106">What you will do</span></span>
<span data-ttu-id="4ad45-107">Cloner hello exemple Arduino d’application à partir de GitHub et utiliser hello gulp outil toodeploy hello exemple application tooyour Adafruit estompe M0 Wi-Fi Arduino tableau.</span><span class="sxs-lookup"><span data-stu-id="4ad45-107">Clone hello sample Arduino application from GitHub, and use hello gulp tool toodeploy hello sample application tooyour Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="4ad45-108">application d’exemple Hello hello clignote GPIO n° 13 sur barod LED toutes les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="4ad45-108">hello sample application blinks hello GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="4ad45-109">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="4ad45-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4ad45-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="4ad45-110">What you will learn</span></span>
* <span data-ttu-id="4ad45-111">Comment toodeploy et exécution hello exemple d’application dans votre tableau de Arduino.</span><span class="sxs-lookup"><span data-stu-id="4ad45-111">How toodeploy and run hello sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4ad45-112">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="4ad45-112">What you need</span></span>
<span data-ttu-id="4ad45-113">Vous devez avoir correctement terminé hello opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4ad45-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="4ad45-114">[Configuration de votre appareil][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="4ad45-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="4ad45-115">[Obtenir les outils de hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="4ad45-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="4ad45-116">Exemple d’application hello ouvert</span><span class="sxs-lookup"><span data-stu-id="4ad45-116">Open hello sample application</span></span>
<span data-ttu-id="4ad45-117">tooopen hello exemple d’application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4ad45-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="4ad45-118">Clonez le dépôt d’exemples hello à partir de GitHub en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4ad45-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="4ad45-119">Ouvrir l’exemple d’application hello dans Visual Studio Code par hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="4ad45-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Structure du référentiel][repo-structure]

<span data-ttu-id="4ad45-121">Hello `app.ino` fichier Bonjour `app` sous-dossier est le fichier de source de la clé de hello qui contient hello code toocontrol hello DEL.</span><span class="sxs-lookup"><span data-stu-id="4ad45-121">hello `app.ino` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="4ad45-122">Installation des dépendances de l’application</span><span class="sxs-lookup"><span data-stu-id="4ad45-122">Install application dependencies</span></span>
<span data-ttu-id="4ad45-123">Installer les bibliothèques hello et autres modules que vous avez besoin pour l’application d’exemple hello en exécutant hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4ad45-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="4ad45-124">Configurer la connexion du périphérique hello</span><span class="sxs-lookup"><span data-stu-id="4ad45-124">Configure hello device connection</span></span>
<span data-ttu-id="4ad45-125">tooconfigure hello connexion du périphérique, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4ad45-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="4ad45-126">Obtenir le port série de hello du périphérique hello avec cli de découverte de périphérique hello :</span><span class="sxs-lookup"><span data-stu-id="4ad45-126">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="4ad45-127">Vous devez voir une sortie similaire toohello suivant et trouver hello usb port COM de votre carte Arduino : ![la détection des périphériques][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="4ad45-127">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="4ad45-128">Les fichiers ouverts hello `config.json` hello du dossier de la leçon et ajouter la valeur hello hello trouvé le numéro de port COM :</span><span class="sxs-lookup"><span data-stu-id="4ad45-128">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > <span data-ttu-id="4ad45-130">Pour le port COM de hello, sur la plateforme Windows, d’un format de hello `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="4ad45-130">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="4ad45-131">Sur macOS ou Ubuntu, il commence par `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="4ad45-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="4ad45-132">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="4ad45-132">Deploy and run hello sample application</span></span>
### <a name="install-hello-required-tools-for-your-arduino-board"></a><span data-ttu-id="4ad45-133">Installer les outils de hello requis pour votre carte mère Arduino</span><span class="sxs-lookup"><span data-stu-id="4ad45-133">Install hello required tools for your Arduino board</span></span>

<span data-ttu-id="4ad45-134">Installer hello Kit de développement logiciel Azure IoT Hub pour votre carte mère Arduino en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4ad45-134">Install hello Azure IoT Hub SDK for your Arduino board by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="4ad45-135">Cette tâche peut prendre un toocomplete beaucoup de temps, en fonction de votre connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="4ad45-135">This task might take a long time toocomplete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="4ad45-136">Veuillez quitter hello instance Arduino IDE en cours d’exécution lors de l’exécution des tâches de gulp : `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="4ad45-136">Please exit hello running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="4ad45-137">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="4ad45-137">Deploy and run hello sample app</span></span>
<span data-ttu-id="4ad45-138">Déployer et exécuter l’exemple d’application hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4ad45-138">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="4ad45-139">Vérifiez que hello application fonctionne</span><span class="sxs-lookup"><span data-stu-id="4ad45-139">Verify hello app works</span></span>
<span data-ttu-id="4ad45-140">Si vous ne voyez pas hello LED clignote, consultez hello [guide de dépannage] [ troubleshooting-page] des problèmes de toocommon solutions.</span><span class="sxs-lookup"><span data-stu-id="4ad45-140">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting-page] for solutions toocommon problems.</span></span>

![LED clignotante][led-blinking]

## <a name="summary"></a><span data-ttu-id="4ad45-142">Résumé</span><span class="sxs-lookup"><span data-stu-id="4ad45-142">Summary</span></span>
<span data-ttu-id="4ad45-143">Vous avez installé des hello requis outils toowork avec votre carte mère Arduino et déployé un Bonjour exemple application tooyour Arduino tableau tooblink DEL.</span><span class="sxs-lookup"><span data-stu-id="4ad45-143">You've installed hello required tools toowork with your Arduino board and deployed a sample application tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="4ad45-144">Vous pouvez désormais créer, déployer et exécuter un autre exemple d’application qui se connecte à votre tooAzure de carte Arduino toosend d’IoT Hub et recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="4ad45-144">You can now create, deploy, and run another sample application that connects your Arduino board tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ad45-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ad45-145">Next steps</span></span>
<span data-ttu-id="4ad45-146">[Obtenir des outils Azure hello][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="4ad45-146">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md