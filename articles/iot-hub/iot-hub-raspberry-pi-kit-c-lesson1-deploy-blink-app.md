---
title: "Connect Raspberry PI (C) tooAzure IoT - leçon 1 : déploiement d’une application | Documents Microsoft"
description: "Cloner l’application d’exemple C hello à partir de GitHub et gulp toodeploy ce tableau de tooyour framboises Pi 3 d’application. Cet exemple d’application clignote hello LED connecté toohello tableau toutes les deux secondes."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: raspberry pi led clignotante, led clignotante avec raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e90c3360c4de1873313db19561c781eb21dbf1d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="5172a-105">Créer et déployer des applications de clignotement hello</span><span class="sxs-lookup"><span data-stu-id="5172a-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5172a-106">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="5172a-106">What you will do</span></span>
<span data-ttu-id="5172a-107">Cloner hello exemple C d’application à partir de GitHub et utiliser l’exemple hello gulp outil toodeploy hello application tooRaspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="5172a-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooRaspberry Pi 3.</span></span> <span data-ttu-id="5172a-108">exemple d’application Hello clignote hello LED connecté toohello tableau toutes les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="5172a-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="5172a-109">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5172a-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5172a-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="5172a-110">What you will learn</span></span>
<span data-ttu-id="5172a-111">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5172a-111">In this article, you will learn:</span></span>

* <span data-ttu-id="5172a-112">Comment toouse hello `device-discover-cli` tooretrieve outil mise en réseau des informations sur Pi.</span><span class="sxs-lookup"><span data-stu-id="5172a-112">How toouse hello `device-discover-cli` tool tooretrieve networking information about Pi.</span></span>
* <span data-ttu-id="5172a-113">Comment toodeploy et exécution hello exemple d’application sur Pi.</span><span class="sxs-lookup"><span data-stu-id="5172a-113">How toodeploy and run hello sample application on Pi.</span></span>
* <span data-ttu-id="5172a-114">Comment toodeploy et débogage des applications en cours d’exécution à distance sur Pi.</span><span class="sxs-lookup"><span data-stu-id="5172a-114">How toodeploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5172a-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="5172a-115">What you need</span></span>
<span data-ttu-id="5172a-116">Vous devez avoir correctement terminé hello opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="5172a-116">You must have successfully completed hello following operations:</span></span>

* [<span data-ttu-id="5172a-117">Configuration de votre appareil</span><span class="sxs-lookup"><span data-stu-id="5172a-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [<span data-ttu-id="5172a-118">Obtenir les outils de hello</span><span class="sxs-lookup"><span data-stu-id="5172a-118">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a><span data-ttu-id="5172a-119">Obtenir hello IP adresse et nom d’hôte de Pi</span><span class="sxs-lookup"><span data-stu-id="5172a-119">Obtain hello IP address and host name of Pi</span></span>
<span data-ttu-id="5172a-120">Ouvrez une invite de commandes dans Windows ou d’un terminal dans macOS ou Ubuntu, puis exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5172a-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run hello following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="5172a-121">Vous devez voir une sortie similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="5172a-121">You should see an output that is similar toohello following:</span></span>

![Découverte de l’appareil](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="5172a-123">Prenez note de hello `IP address` et `hostname` de Pi.</span><span class="sxs-lookup"><span data-stu-id="5172a-123">Take note of hello `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="5172a-124">Ces informations vous seront nécessaires plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="5172a-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="5172a-125">Assurez-vous que Pi est connecté toohello même réseau que votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5172a-125">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="5172a-126">Par exemple, si votre ordinateur est connecté tooa les réseau sans fil pendant que Pi est connecté tooa réseau câblé, vous verrez ne peut-être pas hello IP adresse dans la sortie de devdisco hello.</span><span class="sxs-lookup"><span data-stu-id="5172a-126">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="5172a-127">Exemple d’application hello ouvert</span><span class="sxs-lookup"><span data-stu-id="5172a-127">Open hello sample application</span></span>
<span data-ttu-id="5172a-128">tooopen hello exemple d’application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5172a-128">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="5172a-129">Clonez le dépôt d’exemples hello à partir de GitHub en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5172a-129">Clone hello sample repository from GitHub by running hello following command:</span></span>
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. <span data-ttu-id="5172a-130">Ouvrir l’exemple d’application hello dans Visual Studio Code par hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="5172a-130">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Structure du référentiel](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

<span data-ttu-id="5172a-132">Hello `main.c` fichier Bonjour `app` sous-dossier est le fichier de source de la clé de hello qui contient hello code toocontrol hello DEL.</span><span class="sxs-lookup"><span data-stu-id="5172a-132">hello `main.c` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="5172a-133">Installation des dépendances de l’application</span><span class="sxs-lookup"><span data-stu-id="5172a-133">Install application dependencies</span></span>
<span data-ttu-id="5172a-134">Installer les bibliothèques hello et autres modules que vous avez besoin pour l’application d’exemple hello en exécutant hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5172a-134">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="5172a-135">Configurer la connexion du périphérique hello</span><span class="sxs-lookup"><span data-stu-id="5172a-135">Configure hello device connection</span></span>
<span data-ttu-id="5172a-136">tooconfigure hello connexion du périphérique, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5172a-136">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="5172a-137">Générer le fichier de configuration de périphérique de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5172a-137">Generate hello device configuration file by running hello following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="5172a-138">fichier de configuration Hello `config-raspberrypi.json` contient des informations d’identification de l’utilisateur hello vous utilisez toolog dans tooPi.</span><span class="sxs-lookup"><span data-stu-id="5172a-138">hello configuration file `config-raspberrypi.json` contains hello user credentials you use toolog in tooPi.</span></span> <span data-ttu-id="5172a-139">fuite de hello tooavoid des informations d’identification de l’utilisateur, le fichier de configuration de hello est généré dans le sous-dossier de hello `.iot-hub-getting-started` du dossier de base hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5172a-139">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="5172a-140">Ouvrez le fichier de configuration de périphérique de hello dans le Code de Visual Studio en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5172a-140">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. <span data-ttu-id="5172a-141">Remplacez l’espace réservé de hello `[device hostname or IP address]` avec l’adresse IP de hello ou nom d’hôte hello que vous avez obtenu précédemment dans « Obtention hello IP adresse et nom d’hôte de Pi. »</span><span class="sxs-lookup"><span data-stu-id="5172a-141">Replace hello placeholder `[device hostname or IP address]` with hello IP address or hello host name that you got previously in "Obtain hello IP address and host name of Pi."</span></span>
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="5172a-143">Vous pouvez utiliser la clé SSH au lieu de nom d’utilisateur et mot de passe lors de la connexion tooRaspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="5172a-143">You can use SSH key instead of user name and password when connecting tooRaspberry Pi.</span></span> <span data-ttu-id="5172a-144">Dans commande toodo cela avoir toogenerate hello clé à l’aide **ssh-keygen** et **pi ssh-copy-id @\<adresse du périphérique\>**.</span><span class="sxs-lookup"><span data-stu-id="5172a-144">In order toodo this you will have toogenerate hello key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="5172a-145">Sous Windows, ces commandes sont disponibles dans **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="5172a-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="5172a-146">Sur Mac OS, vous devez toorun **brew installer ssh-copy-id**.</span><span class="sxs-lookup"><span data-stu-id="5172a-146">On MacOS you need toorun **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="5172a-147">Après avoir téléchargé avec succès les toohello de clé hello framboises Pi, remplacez **device_password** avec **device_key_path** propriété dans **raspberrypi.json de configuration**.</span><span class="sxs-lookup"><span data-stu-id="5172a-147">After successfully uploading hello key toohello Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="5172a-148">Les lignes mises à jour doivent se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="5172a-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="5172a-149">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="5172a-149">Congratulations!</span></span> <span data-ttu-id="5172a-150">Vous venez de créer hello premier exemple d’application de Pi.</span><span class="sxs-lookup"><span data-stu-id="5172a-150">You've successfully created hello first sample application for Pi.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="5172a-151">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="5172a-151">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-pi"></a><span data-ttu-id="5172a-152">Installer hello Azure IoT Hub SDK sur Pi</span><span class="sxs-lookup"><span data-stu-id="5172a-152">Install hello Azure IoT Hub SDK on Pi</span></span>
<span data-ttu-id="5172a-153">Installer hello Azure IoT Hub SDK sur Pi en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5172a-153">Install hello Azure IoT Hub SDK on Pi by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="5172a-154">Cette tâche peut prendre quelques hello de toocomplete minutes première fois que vous l’exécutez.</span><span class="sxs-lookup"><span data-stu-id="5172a-154">This task might take a few minutes toocomplete hello first time you run it.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="5172a-155">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="5172a-155">Deploy and run hello sample app</span></span>
<span data-ttu-id="5172a-156">Déployer et exécuter l’exemple d’application hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5172a-156">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="5172a-157">Vérifiez que hello application fonctionne</span><span class="sxs-lookup"><span data-stu-id="5172a-157">Verify hello app works</span></span>
<span data-ttu-id="5172a-158">exemple d’application Hello se termine automatiquement après que hello LED clignote pour 20 fois.</span><span class="sxs-lookup"><span data-stu-id="5172a-158">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="5172a-159">Si vous ne voyez pas hello LED clignote, consultez hello [guide de dépannage](iot-hub-raspberry-pi-kit-c-troubleshooting.md) pour les problèmes de toocommon solutions.</span><span class="sxs-lookup"><span data-stu-id="5172a-159">If you don’t see hello LED blinking, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>
<span data-ttu-id="5172a-160">![LED clignotante](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="5172a-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="5172a-161">Résumé</span><span class="sxs-lookup"><span data-stu-id="5172a-161">Summary</span></span>
<span data-ttu-id="5172a-162">Vous avez installé des hello requis outils toowork avec Pi et déployé un Bonjour de tooblink exemple application tooPi DEL.</span><span class="sxs-lookup"><span data-stu-id="5172a-162">You've installed hello required tools toowork with Pi and deployed a sample application tooPi tooblink hello LED.</span></span> <span data-ttu-id="5172a-163">Vous pouvez désormais créer, déployer et exécuter un autre exemple d’application qui se connecte Pi tooAzure toosend d’IoT Hub et recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="5172a-163">You can now create, deploy, and run another sample application that connects Pi tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5172a-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5172a-164">Next steps</span></span>
[<span data-ttu-id="5172a-165">Obtenir les outils Azure</span><span class="sxs-lookup"><span data-stu-id="5172a-165">Get Azure tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

