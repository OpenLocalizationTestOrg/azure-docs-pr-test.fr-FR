---
title: "Connect Intel Edison (C) tooAzure IoT - leçon 1 : déploiement d’application | Documents Microsoft"
description: "Cloner l’application d’exemple C hello à partir de GitHub et exécutez gulp toodeploy cette tooyour application du tableau de Edison d’Intel. Cet exemple d’application clignote hello LED connecté toohello tableau toutes les deux secondes."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: projets de led arduino, clignotement de led arduino, code de clignotement de led arduino, programme de clignotement arduino, exemple de clignotement arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: fa84fae812dd742a2ad4997a5e213c8e40e6fcf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="d86ca-105">Créer et déployer des applications de clignotement hello</span><span class="sxs-lookup"><span data-stu-id="d86ca-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d86ca-106">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="d86ca-106">What you will do</span></span>
<span data-ttu-id="d86ca-107">Cloner l’application d’exemple C hello à partir de GitHub et utiliser l’exemple hello gulp outil toodeploy hello application tooIntel Edison.</span><span class="sxs-lookup"><span data-stu-id="d86ca-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooIntel Edison.</span></span> <span data-ttu-id="d86ca-108">exemple d’application Hello clignote hello LED connecté toohello tableau toutes les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="d86ca-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="d86ca-109">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="d86ca-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d86ca-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="d86ca-110">What you will learn</span></span>
* <span data-ttu-id="d86ca-111">Comment toodeploy et exécution hello exemple d’application sur Edison.</span><span class="sxs-lookup"><span data-stu-id="d86ca-111">How toodeploy and run hello sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d86ca-112">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="d86ca-112">What you need</span></span>
<span data-ttu-id="d86ca-113">Vous devez avoir correctement terminé hello opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d86ca-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="d86ca-114">[Configuration de votre appareil][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="d86ca-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="d86ca-115">[Obtenir les outils de hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="d86ca-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="d86ca-116">Exemple d’application hello ouvert</span><span class="sxs-lookup"><span data-stu-id="d86ca-116">Open hello sample application</span></span>
<span data-ttu-id="d86ca-117">tooopen hello exemple d’application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d86ca-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="d86ca-118">Clonez le dépôt d’exemples hello à partir de GitHub en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d86ca-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="d86ca-119">Ouvrir l’exemple d’application hello dans Visual Studio Code par hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="d86ca-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Structure du référentiel][repo-structure]

<span data-ttu-id="d86ca-121">fichier Hello Bonjour `app` sous-dossier est le fichier de source de la clé de hello qui contient hello code toocontrol hello DEL.</span><span class="sxs-lookup"><span data-stu-id="d86ca-121">hello file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="d86ca-122">Installation des dépendances de l’application</span><span class="sxs-lookup"><span data-stu-id="d86ca-122">Install application dependencies</span></span>
<span data-ttu-id="d86ca-123">Installer les bibliothèques hello et autres modules que vous avez besoin pour l’application d’exemple hello en exécutant hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d86ca-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="d86ca-124">Configurer la connexion du périphérique hello</span><span class="sxs-lookup"><span data-stu-id="d86ca-124">Configure hello device connection</span></span>
<span data-ttu-id="d86ca-125">tooconfigure hello connexion du périphérique, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d86ca-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="d86ca-126">Générer le fichier de configuration de périphérique de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d86ca-126">Generate hello device configuration file by running hello following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="d86ca-127">fichier de configuration Hello `config-edison.json` contient des informations d’identification de l’utilisateur hello vous utilisez toolog dans tooEdison.</span><span class="sxs-lookup"><span data-stu-id="d86ca-127">hello configuration file `config-edison.json` contains hello user credentials you use toolog in tooEdison.</span></span> <span data-ttu-id="d86ca-128">fuite de hello tooavoid des informations d’identification de l’utilisateur, le fichier de configuration de hello est généré dans le sous-dossier de hello `.iot-hub-getting-started` du dossier de base hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d86ca-128">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="d86ca-129">Ouvrez le fichier de configuration de périphérique de hello dans le Code de Visual Studio en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d86ca-129">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="d86ca-130">Remplacez l’espace réservé de hello `[device hostname or IP address]` et `[device password]` avec l’adresse IP de hello et un mot de passe que vous avez marqués vers le bas dans la leçon précédente.</span><span class="sxs-lookup"><span data-stu-id="d86ca-130">Replace hello placeholder `[device hostname or IP address]` and `[device password]` with hello IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="d86ca-132">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="d86ca-132">Congratulations!</span></span> <span data-ttu-id="d86ca-133">Vous venez de créer hello premier exemple d’application pour Edison.</span><span class="sxs-lookup"><span data-stu-id="d86ca-133">You've successfully created hello first sample application for Edison.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="d86ca-134">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="d86ca-134">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="d86ca-135">Installer hello Azure IoT Hub SDK sur Edison</span><span class="sxs-lookup"><span data-stu-id="d86ca-135">Install hello Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="d86ca-136">Installer hello Azure IoT Hub SDK sur Edison en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d86ca-136">Install hello Azure IoT Hub SDK on Edison by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="d86ca-137">Cette tâche peut prendre un toocomplete beaucoup de temps, en fonction de votre connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="d86ca-137">This task might take a long time toocomplete, depending on your network connection.</span></span> <span data-ttu-id="d86ca-138">Elle a besoin toobe s’exécute qu’une seule fois pour un seul Edison.</span><span class="sxs-lookup"><span data-stu-id="d86ca-138">It needs toobe run only once for one Edison.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="d86ca-139">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="d86ca-139">Deploy and run hello sample app</span></span>
<span data-ttu-id="d86ca-140">Déployer et exécuter l’exemple d’application hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d86ca-140">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="d86ca-141">Vérifiez que hello application fonctionne</span><span class="sxs-lookup"><span data-stu-id="d86ca-141">Verify hello app works</span></span>
<span data-ttu-id="d86ca-142">exemple d’application Hello se termine automatiquement après que hello LED clignote pour 20 fois.</span><span class="sxs-lookup"><span data-stu-id="d86ca-142">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="d86ca-143">Si vous ne voyez pas hello LED clignote, consultez hello [guide de dépannage] [ troubleshooting] des problèmes de toocommon solutions.</span><span class="sxs-lookup"><span data-stu-id="d86ca-143">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

![LED clignotante][led-blinking]

## <a name="summary"></a><span data-ttu-id="d86ca-145">Résumé</span><span class="sxs-lookup"><span data-stu-id="d86ca-145">Summary</span></span>
<span data-ttu-id="d86ca-146">Vous avez installé des hello requis outils toowork avec Edison et déployé un Bonjour de tooblink exemple application tooEdison DEL.</span><span class="sxs-lookup"><span data-stu-id="d86ca-146">You've installed hello required tools toowork with Edison and deployed a sample application tooEdison tooblink hello LED.</span></span> <span data-ttu-id="d86ca-147">Vous pouvez désormais créer, déployer et exécuter un autre exemple d’application qui se connecte Edison tooAzure toosend d’IoT Hub et recevoir des messages.</span><span class="sxs-lookup"><span data-stu-id="d86ca-147">You can now create, deploy, and run another sample application that connects Edison tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d86ca-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d86ca-148">Next steps</span></span>
<span data-ttu-id="d86ca-149">[Obtenir des outils Azure hello][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="d86ca-149">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
