---
title: "Connecter Intel Edison (Node) à Azure IoT - Leçon 1 : Déployer une application | Microsoft Docs"
description: "Clonez l’exemple d’application C à partir de GitHub et exécutez gulp pour déployer cette application sur votre carte Intel Edison. Avec cet exemple d’application, la LED connectée à la carte clignote toutes les deux secondes."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: projets de led arduino, clignotement de led arduino, code de clignotement de led arduino, programme de clignotement arduino, exemple de clignotement arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8490fbbf14183432c665165412f00955d6323580
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="adb17-105">Créer et déployer l’application blink</span><span class="sxs-lookup"><span data-stu-id="adb17-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="adb17-106">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="adb17-106">What you will do</span></span>
<span data-ttu-id="adb17-107">Clonez l’exemple d’application C à partir de GitHub et utilisez l’outil gulp pour le déployer sur Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="adb17-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span></span> <span data-ttu-id="adb17-108">Avec cet exemple d’application, la LED connectée à la carte clignote toutes les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="adb17-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="adb17-109">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="adb17-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="adb17-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="adb17-110">What you will learn</span></span>
* <span data-ttu-id="adb17-111">Déploiement et exécution de l’exemple d’application sur Edison.</span><span class="sxs-lookup"><span data-stu-id="adb17-111">How to deploy and run the sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="adb17-112">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="adb17-112">What you need</span></span>
<span data-ttu-id="adb17-113">Vous devez avoir terminé les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="adb17-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="adb17-114">[Configuration de votre appareil][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="adb17-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="adb17-115">[Obtenir les outils][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="adb17-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="adb17-116">Ouvrir l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="adb17-116">Open the sample application</span></span>
<span data-ttu-id="adb17-117">Procédez comme suit pour ouvrir l’exemple d’application :</span><span class="sxs-lookup"><span data-stu-id="adb17-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="adb17-118">Clonez l’exemple de référentiel à partir de GitHub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="adb17-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. <span data-ttu-id="adb17-119">Ouvrez l’exemple d’application dans Visual Studio Code en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="adb17-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Structure du référentiel][repo-structure]

<span data-ttu-id="adb17-121">Le fichier dans le sous-dossier `app` est le fichier source clé qui contient le code pour contrôler la LED.</span><span class="sxs-lookup"><span data-stu-id="adb17-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="adb17-122">Installation des dépendances de l’application</span><span class="sxs-lookup"><span data-stu-id="adb17-122">Install application dependencies</span></span>
<span data-ttu-id="adb17-123">Installez les bibliothèques et d’autres modules dont vous avez besoin pour l’exemple d’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="adb17-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="adb17-124">Configuration de la connexion de l’appareil</span><span class="sxs-lookup"><span data-stu-id="adb17-124">Configure the device connection</span></span>
<span data-ttu-id="adb17-125">Procédez comme suit pour configurer la connexion de l’appareil :</span><span class="sxs-lookup"><span data-stu-id="adb17-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="adb17-126">Générez le fichier de configuration de votre appareil en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="adb17-126">Generate the device configuration file by running the following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="adb17-127">Le fichier de configuration `config-edison.json` contient les informations d’identification utilisateur que vous utilisez pour vous connecter à Edison.</span><span class="sxs-lookup"><span data-stu-id="adb17-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span></span> <span data-ttu-id="adb17-128">Pour éviter la fuite d’informations d’identification de l’utilisateur, le fichier de configuration est généré dans le sous-dossier `.iot-hub-getting-started` du dossier de base de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="adb17-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="adb17-129">Ouvrez le fichier de configuration de votre appareil dans Visual Studio Code en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="adb17-129">Open the device configuration file in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="adb17-130">Remplacez les espaces réservés `[device hostname or IP address]` et `[device password]` par l’adresse IP et le mot de passe de la leçon précédente.</span><span class="sxs-lookup"><span data-stu-id="adb17-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="adb17-132">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="adb17-132">Congratulations!</span></span> <span data-ttu-id="adb17-133">Vous avez créé le premier exemple d’application pour Edison.</span><span class="sxs-lookup"><span data-stu-id="adb17-133">You've successfully created the first sample application for Edison.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="adb17-134">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="adb17-134">Deploy and run the sample application</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="adb17-135">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="adb17-135">Deploy and run the sample app</span></span>
<span data-ttu-id="adb17-136">Déployez et exécutez l’exemple d’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="adb17-136">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="adb17-137">Vérification du bon fonctionnement de l’application</span><span class="sxs-lookup"><span data-stu-id="adb17-137">Verify the app works</span></span>
<span data-ttu-id="adb17-138">L’exemple d’application se termine automatiquement une fois que la LED a clignoté 20 fois.</span><span class="sxs-lookup"><span data-stu-id="adb17-138">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="adb17-139">Si vous ne voyez pas la LED clignoter, consultez le [guide de dépannage][troubleshooting] des problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="adb17-139">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

![LED clignotante][led-blinking]

## <a name="summary"></a><span data-ttu-id="adb17-141">Résumé</span><span class="sxs-lookup"><span data-stu-id="adb17-141">Summary</span></span>
<span data-ttu-id="adb17-142">Vous avez installé les outils nécessaires pour travailler avec Edison et déployé un exemple d’application sur Edison pour faire clignoter la LED.</span><span class="sxs-lookup"><span data-stu-id="adb17-142">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span></span> <span data-ttu-id="adb17-143">Vous pouvez maintenant créer, déployer et exécuter un autre exemple d’application qui connecte Edison à Azure IoT Hub pour envoyer et recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="adb17-143">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adb17-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="adb17-144">Next steps</span></span>
<span data-ttu-id="adb17-145">[Obtenir les outils Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="adb17-145">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
