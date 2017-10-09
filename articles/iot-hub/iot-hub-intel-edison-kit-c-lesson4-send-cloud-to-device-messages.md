---
title: "Connect Intel Edison (C) tooAzure IoT - leçon 4 : recevoir des messages | Documents Microsoft"
description: "Un exemple d’application s’exécute sur Edison et surveille les messages entrants à partir de votre IoT Hub. Une nouvelle tâche gulp envoie des messages tooEdison à partir de votre hello tooblink du hub IoT DEL."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "contrôle de la led avec arduino à partir du web, contrôle de la led avec arduino via le web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 820d38f3-d3b8-4249-9e2b-f1b9b771e62f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f0424506ff755e0b9514684787b37584d406d320
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="60e27-105">Exécuter un tooreceive d’application exemple messages cloud-à-appareil</span><span class="sxs-lookup"><span data-stu-id="60e27-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="60e27-106">Dans cet article, vous déployez un exemple d’application sur Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="60e27-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="60e27-107">exemple d’application Hello surveille les messages entrants à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="60e27-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="60e27-108">Aussi, vous exécutez une tâche de gulp sur votre tooEdison de messages toosend ordinateur à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="60e27-108">You also run a gulp task on your computer toosend messages tooEdison from your IoT hub.</span></span> <span data-ttu-id="60e27-109">Lors de l’application d’exemple hello reçoit des messages hello, il clignote hello DEL.</span><span class="sxs-lookup"><span data-stu-id="60e27-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="60e27-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="60e27-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="60e27-111">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="60e27-111">What you will do</span></span>
* <span data-ttu-id="60e27-112">Connectez le hub IoT tooyour hello exemple application.</span><span class="sxs-lookup"><span data-stu-id="60e27-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="60e27-113">Déployer et exécuter l’exemple d’application hello.</span><span class="sxs-lookup"><span data-stu-id="60e27-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="60e27-114">Envoyer des messages à partir de votre hello dans IoT hub tooEdison tooblink DEL.</span><span class="sxs-lookup"><span data-stu-id="60e27-114">Send messages from your IoT hub tooEdison tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="60e27-115">Contenu</span><span class="sxs-lookup"><span data-stu-id="60e27-115">What you will learn</span></span>
<span data-ttu-id="60e27-116">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="60e27-116">In this article, you will learn:</span></span>
* <span data-ttu-id="60e27-117">Comment les messages entrants de toomonitor à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="60e27-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="60e27-118">Comment les messages à partir de votre tooEdison de hub IoT toosend cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="60e27-118">How toosend cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="60e27-119">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="60e27-119">What you need</span></span>
* <span data-ttu-id="60e27-120">Intel Edison, configuré et prêt à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="60e27-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="60e27-121">toolearn tooset des Edison, voir [configurer votre périphérique][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="60e27-121">toolearn how tooset up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="60e27-122">Un IoT Hub créé dans le cadre de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="60e27-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="60e27-123">toolearn comment toocreate votre IoT hub, consultez [créer votre Azure IoT Hub][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="60e27-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="60e27-124">Connecter le hub IoT tooyour hello exemple application</span><span class="sxs-lookup"><span data-stu-id="60e27-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="60e27-125">Assurez-vous que vous êtes dans le dossier de dépôt hello `iot-hub-c-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="60e27-125">Make sure that you're in hello repo folder `iot-hub-c-edison-getting-started`.</span></span> <span data-ttu-id="60e27-126">Ouvrir l’exemple d’application hello dans Visual Studio Code par hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="60e27-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="60e27-127">fichier Hello Bonjour `app` sous-dossier est le fichier de source de la clé hello qui contient les messages entrants toomonitor code hello à partir du hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="60e27-127">hello file in hello `app` subfolder is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="60e27-128">Hello `blinkLED` fonction clignote hello DEL.</span><span class="sxs-lookup"><span data-stu-id="60e27-128">hello `blinkLED` function blinks hello LED.</span></span>

   ![Structure de référentiel dans l’exemple d’application hello][repo-structure]
2. <span data-ttu-id="60e27-130">Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="60e27-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="60e27-131">Si vous avez terminé les étapes de hello dans [créer un compte d’application et de stockage Azure fonction] [ create-an-azure-function-app-and-storage-account] sur cet ordinateur, toutes les configurations de hello sont héritées, vous pouvez sauter des tâches de toohello hello étape du déploiement et exemple d’application hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="60e27-131">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="60e27-132">Si vous avez terminé les étapes de hello dans [créer un compte d’application et de stockage Azure fonction] [ create-an-azure-function-app-and-storage-account] sur un autre ordinateur, vous avez besoin des espaces réservés de hello tooreplace Bonjour `config-edison.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="60e27-132">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-edison.json` file.</span></span> <span data-ttu-id="60e27-133">Hello `config-edison.json` fichier se trouve dans le sous-dossier hello de votre dossier de base.</span><span class="sxs-lookup"><span data-stu-id="60e27-133">hello `config-edison.json` file is in hello subfolder of your home folder.</span></span>

   ![Contenu du fichier de configuration-edison.json hello](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="60e27-135">Remplacez **[nom d’hôte du périphérique ou adresse IP]** avec l’adresse IP du périphérique hello démarquer lorsque vous avez configuré votre appareil.</span><span class="sxs-lookup"><span data-stu-id="60e27-135">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="60e27-136">Remplacez **[chaîne de connexion de périphérique IoT]** avec la chaîne de connexion de périphérique hello que vous obtenez en exécutant hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` commande.</span><span class="sxs-lookup"><span data-stu-id="60e27-136">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="60e27-137">Remplacez **[chaîne de connexion de hub IoT]** avec hello chaîne de connexion de hub IoT que vous obtenez en exécutant hello `az iot hub show-connection-string --name {my hub name}` commande.</span><span class="sxs-lookup"><span data-stu-id="60e27-137">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="60e27-138">Exécutez également **gulp install-tools**, si vous ne l’avez pas fait dans la leçon 1.</span><span class="sxs-lookup"><span data-stu-id="60e27-138">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="60e27-139">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="60e27-139">Deploy and run hello sample application</span></span>
<span data-ttu-id="60e27-140">Déployer et exécuter l’exemple d’application hello sur Edison en exécutant hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="60e27-140">Deploy and run hello sample application on Edison by running hello following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="60e27-141">commande de gulp Hello déploie tooEdison d’application exemple hello.</span><span class="sxs-lookup"><span data-stu-id="60e27-141">hello gulp command deploys hello sample application tooEdison.</span></span> <span data-ttu-id="60e27-142">Ensuite, elle s’exécute application hello sur Edison et une tâche distincte sur votre hôte ordinateur toosend 20 blink messages tooEdison à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="60e27-142">Then, it runs hello application on Edison and a separate task on your host computer toosend 20 blink messages tooEdison from your IoT hub.</span></span>

<span data-ttu-id="60e27-143">Après l’exécution de l’exemple d’application hello, il commence à écouter toomessages à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="60e27-143">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="60e27-144">Pendant ce temps, tâche de gulp hello envoie plusieurs messages « clignoter » à partir de votre tooEdison de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="60e27-144">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="60e27-145">Pour chaque message blink Edison reçoit, exemple d’application hello appelle hello `blinkLED` hello tooblink de fonction DEL.</span><span class="sxs-lookup"><span data-stu-id="60e27-145">For each blink message that Edison receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="60e27-146">Vous devez voir clignotement de LED hello toutes les deux secondes comme hello gulp la tâche envoie des messages à partir de votre tooEdison de hub IoT 20.</span><span class="sxs-lookup"><span data-stu-id="60e27-146">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="60e27-147">Hello dernier un est un message « arrêter » qui arrête l’application hello de s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="60e27-147">hello last one is a "stop" message that stops hello application from running.</span></span>

![Exemple d’application avec la commande gulp et les messages de clignotement][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="60e27-149">Résumé</span><span class="sxs-lookup"><span data-stu-id="60e27-149">Summary</span></span>
<span data-ttu-id="60e27-150">Vous avez correctement envoyé des messages à partir de votre hello dans IoT hub tooEdison tooblink DEL.</span><span class="sxs-lookup"><span data-stu-id="60e27-150">You’ve successfully sent messages from your IoT hub tooEdison tooblink hello LED.</span></span> <span data-ttu-id="60e27-151">la tâche suivante Hello est facultative : modifier hello et désactiver le comportement de hello DEL.</span><span class="sxs-lookup"><span data-stu-id="60e27-151">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60e27-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="60e27-152">Next steps</span></span>
<span data-ttu-id="60e27-153">[Modifier hello et désactiver le comportement de hello DEL][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="60e27-153">[Change hello on and off behavior of hello LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure_c.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink_c.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-c-lesson4-change-led-behavior.md