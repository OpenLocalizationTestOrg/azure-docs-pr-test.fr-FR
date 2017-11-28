---
title: "Appareil simulé et passerelle Azure IoT - Leçon 3 : Exécuter un exemple d’application | Microsoft Docs"
description: "Exécuter un appareil simulé exemple application toosend température tooyour IoT concentrateur de données"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "toocloud de données"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="79e9f-104">Configurer et exécuter un exemple d’application d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="79e9f-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="79e9f-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="79e9f-105">What you will do</span></span>

- <span data-ttu-id="79e9f-106">Dépôt d’exemples hello clone.</span><span class="sxs-lookup"><span data-stu-id="79e9f-106">Clone hello sample repository.</span></span>
- <span data-ttu-id="79e9f-107">Utilisez hello CLI d’Azure tooget votre IoT hub et les informations d’unité logique pour un exemple d’application appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="79e9f-107">Use hello Azure CLI tooget your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="79e9f-108">Configurer et exécuter l’application d’exemple hello simulée appareil.</span><span class="sxs-lookup"><span data-stu-id="79e9f-108">Configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="79e9f-109">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="79e9f-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="79e9f-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="79e9f-110">What you will learn</span></span>

<span data-ttu-id="79e9f-111">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="79e9f-111">In this article, you will learn:</span></span>

- <span data-ttu-id="79e9f-112">Comment tooconfigure et exécution hello simulés application d’exemple de périphérique.</span><span class="sxs-lookup"><span data-stu-id="79e9f-112">How tooconfigure and run hello simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="79e9f-113">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="79e9f-113">What you need</span></span>

<span data-ttu-id="79e9f-114">Vous devez avoir accompli avec succès les étapes</span><span class="sxs-lookup"><span data-stu-id="79e9f-114">You must have successfully completed</span></span>

- [<span data-ttu-id="79e9f-115">Créer un hub IoT et enregistrer votre appareil</span><span class="sxs-lookup"><span data-stu-id="79e9f-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="79e9f-116">Cloner l’ordinateur hôte toohello hello exemple référentiel</span><span class="sxs-lookup"><span data-stu-id="79e9f-116">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="79e9f-117">dépôt d’exemples tooclone hello, procédez comme suit sur l’ordinateur hôte hello :</span><span class="sxs-lookup"><span data-stu-id="79e9f-117">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="79e9f-118">Ouvrez une invite de commande dans Windows ou ouvrez une fenêtre de terminal dans macOS ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="79e9f-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="79e9f-119">Exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="79e9f-119">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a><span data-ttu-id="79e9f-120">Configurer les appareil simulé hello et votre NUC</span><span class="sxs-lookup"><span data-stu-id="79e9f-120">Configure hello simulated device and your NUC</span></span>

1. <span data-ttu-id="79e9f-121">Fichier de configuration Open hello `config.json` dans le Code de Visual Studio en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="79e9f-121">Open hello configuration file `config.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="79e9f-122">Remplacer `"has_sensortag": true` par `"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="79e9f-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Configuration si vous n’avez pas d'appareil TI SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="79e9f-124">Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="79e9f-124">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="79e9f-125">Ouvrez `config-gateway.json` dans le Code de Visual Studio en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="79e9f-125">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="79e9f-126">Recherchez hello ligne de code suivante et remplacez `[device hostname or IP address]` avec le nom d’hôte ou adresse IP Hello Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="79e9f-126">Locate hello following line of code and replace `[device hostname or IP address]` with IP address or host name of hello Intel NUC.</span></span>
   <span data-ttu-id="79e9f-127">![capture d’écran de la passerelle de configuration](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="79e9f-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="79e9f-128">Obtenir la chaîne de connexion hello du périphérique logique IoT hub</span><span class="sxs-lookup"><span data-stu-id="79e9f-128">Get hello connection string of your IoT hub logical device</span></span>

<span data-ttu-id="79e9f-129">hello tooget chaîne de connexion Azure IoT hub de votre unité logique, exécutez hello commande sur l’ordinateur hôte hello suivante :</span><span class="sxs-lookup"><span data-stu-id="79e9f-129">tooget hello Azure IoT hub connection string of your logical device, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="79e9f-130">`{IoT hub name}`est le nom de hub IoT hello que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="79e9f-130">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="79e9f-131">Utilisez iot-passerelle en tant que valeur hello `{resource group name}` et utiliser mydevice en tant que valeur hello `{device id}` si vous n’avez pas modifier la valeur hello dans la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="79e9f-131">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="79e9f-132">Configurez hello simulée appareil cloud téléchargement exemple d’application</span><span class="sxs-lookup"><span data-stu-id="79e9f-132">Configure hello simulated device cloud upload sample application</span></span>

<span data-ttu-id="79e9f-133">tooconfigure et exécution hello simulée appareil cloud télécharger l’exemple d’application, procédez comme suit sur l’ordinateur hôte hello :</span><span class="sxs-lookup"><span data-stu-id="79e9f-133">tooconfigure and run hello simulated device cloud upload sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="79e9f-134">Ouvrez `config-sensortag.json` dans le Code de Visual Studio en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="79e9f-134">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![capture d’écran de configuration sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="79e9f-136">Rendre hello suivant des remplacements dans le code hello :</span><span class="sxs-lookup"><span data-stu-id="79e9f-136">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="79e9f-137">Remplacez `[IoT hub name]` avec le nom de hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="79e9f-137">Replace `[IoT hub name]` with hello IoT hub name.</span></span>
   - <span data-ttu-id="79e9f-138">Remplacez `[IoT device connection string]` avec chaîne de connexion hello de votre unité logique de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="79e9f-138">Replace `[IoT device connection string]` with hello connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="79e9f-139">Exécutez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="79e9f-139">Run hello application.</span></span>

   <span data-ttu-id="79e9f-140">Déployer et exécuter l’application hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="79e9f-140">Deploy and run hello application by running hello following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a><span data-ttu-id="79e9f-141">Vérifiez le fonctionnement de l’application exemple hello</span><span class="sxs-lookup"><span data-stu-id="79e9f-141">Verify hello sample application works</span></span>

<span data-ttu-id="79e9f-142">Vous devez maintenant voir la sortie hello suivante :</span><span class="sxs-lookup"><span data-stu-id="79e9f-142">You should now see output like hello following:</span></span>

![résultat de l'exemple d'application d'appareil simulé](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="79e9f-144">application Hello envoie la température données tooyour IoT hub, qui dure 40 secondes.</span><span class="sxs-lookup"><span data-stu-id="79e9f-144">hello application sends temperature data tooyour IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="79e9f-145">Résumé</span><span class="sxs-lookup"><span data-stu-id="79e9f-145">Summary</span></span>

<span data-ttu-id="79e9f-146">Vous avez correctement configuré et exécution hello simulée appareil cloud téléchargement exemple d’application qui envoie le concentrateur de données tooyour IoT avec appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="79e9f-146">You've successfully configured and run hello simulated device cloud upload sample application which sends data tooyour IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79e9f-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="79e9f-147">Next steps</span></span>
[<span data-ttu-id="79e9f-148">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="79e9f-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)