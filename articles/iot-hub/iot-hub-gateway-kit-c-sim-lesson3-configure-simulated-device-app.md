---
title: "Appareil simulé et passerelle Azure IoT - Leçon 3 : Exécuter un exemple d’application | Microsoft Docs"
description: "Exécuter un exemple d’application d'appareil simulé pour envoyer des données de température vers Azure IoT Hub"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "données vers le cloud"
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
ms.openlocfilehash: 7df2d730c38a9f715e0fd57b4d436724a5727760
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="410d1-104">Configurer et exécuter un exemple d’application d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="410d1-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="410d1-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="410d1-105">What you will do</span></span>

- <span data-ttu-id="410d1-106">Clonez l'exemple de référentiel.</span><span class="sxs-lookup"><span data-stu-id="410d1-106">Clone the sample repository.</span></span>
- <span data-ttu-id="410d1-107">Utilisez l’interface de ligne de commande Azure afin d'obtenir les informations sur votre IoT Hub et sur l'appareil logique pour l’exemple d’application d'appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="410d1-107">Use the Azure CLI to get your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="410d1-108">Configurez et exécutez l'exemple d’application d’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="410d1-108">Configure and run the simulated device sample application.</span></span>

<span data-ttu-id="410d1-109">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="410d1-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="410d1-110">Contenu</span><span class="sxs-lookup"><span data-stu-id="410d1-110">What you will learn</span></span>

<span data-ttu-id="410d1-111">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="410d1-111">In this article, you will learn:</span></span>

- <span data-ttu-id="410d1-112">Comment configurer et exécuter l'exemple d’application d’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="410d1-112">How to configure and run the simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="410d1-113">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="410d1-113">What you need</span></span>

<span data-ttu-id="410d1-114">Vous devez avoir accompli avec succès les étapes</span><span class="sxs-lookup"><span data-stu-id="410d1-114">You must have successfully completed</span></span>

- [<span data-ttu-id="410d1-115">Créer un hub IoT et enregistrer votre appareil</span><span class="sxs-lookup"><span data-stu-id="410d1-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="410d1-116">Cloner l'exemple de référentiel sur l’ordinateur hôte</span><span class="sxs-lookup"><span data-stu-id="410d1-116">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="410d1-117">Pour cloner l'exemple de référentiel, procédez comme suit sur l’ordinateur hôte :</span><span class="sxs-lookup"><span data-stu-id="410d1-117">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="410d1-118">Ouvrez une invite de commande dans Windows ou ouvrez une fenêtre de terminal dans macOS ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="410d1-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="410d1-119">Exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="410d1-119">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a><span data-ttu-id="410d1-120">Configurer l'appareil simulé et votre NUC</span><span class="sxs-lookup"><span data-stu-id="410d1-120">Configure the simulated device and your NUC</span></span>

1. <span data-ttu-id="410d1-121">Ouvrez le fichier de configuration `config.json` dans Visual Studio Code en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="410d1-121">Open the configuration file `config.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="410d1-122">Remplacer `"has_sensortag": true` par `"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="410d1-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Configuration si vous n’avez pas d'appareil TI SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="410d1-124">Initialisez le fichier de configuration en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="410d1-124">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="410d1-125">Ouvrez `config-gateway.json` dans Visual Studio Code en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="410d1-125">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="410d1-126">Recherchez la ligne de code suivante et remplacez `[device hostname or IP address]` par l’adresse IP ou le nom d'hôte de la NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="410d1-126">Locate the following line of code and replace `[device hostname or IP address]` with IP address or host name of the Intel NUC.</span></span>
   <span data-ttu-id="410d1-127">![capture d’écran de la passerelle de configuration](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="410d1-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="410d1-128">Obtenir la chaîne de connexion de l'appareil logique de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="410d1-128">Get the connection string of your IoT hub logical device</span></span>

<span data-ttu-id="410d1-129">Pour obtenir la chaîne de connexion Azure IoT Hub de votre appareil logique, exécutez la commande suivante sur l’ordinateur hôte :</span><span class="sxs-lookup"><span data-stu-id="410d1-129">To get the Azure IoT hub connection string of your logical device, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="410d1-130">`{IoT hub name}` est le nom de l'IoT Hub que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="410d1-130">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="410d1-131">Utilisez iot-gateway en tant que valeur de `{resource group name}` et mydevice en tant que valeur de `{device id}` si vous n'avez pas modifié la valeur à la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="410d1-131">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="410d1-132">Configurer l'exemple d’application de téléchargement cloud d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="410d1-132">Configure the simulated device cloud upload sample application</span></span>

<span data-ttu-id="410d1-133">Pour configurer et exécuter l’exemple d’application de téléchargement cloud d'appareil simulé, procédez comme suit sur l’ordinateur hôte :</span><span class="sxs-lookup"><span data-stu-id="410d1-133">To configure and run the simulated device cloud upload sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="410d1-134">Ouvrez `config-sensortag.json` dans Visual Studio Code en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="410d1-134">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![capture d’écran de configuration sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="410d1-136">Effectuez les remplacements suivants dans le code :</span><span class="sxs-lookup"><span data-stu-id="410d1-136">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="410d1-137">Remplacez `[IoT hub name]` par le nom de l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="410d1-137">Replace `[IoT hub name]` with the IoT hub name.</span></span>
   - <span data-ttu-id="410d1-138">Remplacez `[IoT device connection string]` par la chaîne de connexion de l'appareil logique de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="410d1-138">Replace `[IoT device connection string]` with the connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="410d1-139">Exécutez l'application.</span><span class="sxs-lookup"><span data-stu-id="410d1-139">Run the application.</span></span>

   <span data-ttu-id="410d1-140">Déployez et exécutez l’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="410d1-140">Deploy and run the application by running the following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a><span data-ttu-id="410d1-141">Vérifier le fonctionnement de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="410d1-141">Verify the sample application works</span></span>

<span data-ttu-id="410d1-142">Un résultat similaire à ce qui suit s’affiche normalement :</span><span class="sxs-lookup"><span data-stu-id="410d1-142">You should now see output like the following:</span></span>

![résultat de l'exemple d'application d'appareil simulé](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="410d1-144">L’application envoie les données de température à votre IoT Hub, opération qui dure 40 secondes.</span><span class="sxs-lookup"><span data-stu-id="410d1-144">The application sends temperature data to your IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="410d1-145">Résumé</span><span class="sxs-lookup"><span data-stu-id="410d1-145">Summary</span></span>

<span data-ttu-id="410d1-146">Vous avez correctement configuré et exécuté l'exemple d'application de téléchargement cloud d'appareil simulé qui envoie des données à votre IoT Hub avec appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="410d1-146">You've successfully configured and run the simulated device cloud upload sample application which sends data to your IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="410d1-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="410d1-147">Next steps</span></span>
[<span data-ttu-id="410d1-148">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="410d1-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)