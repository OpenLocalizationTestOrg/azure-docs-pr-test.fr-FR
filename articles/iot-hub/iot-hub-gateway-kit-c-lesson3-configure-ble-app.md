---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 3 : Exécuter un exemple d’application | Microsoft Docs"
description: "Exécutez BLE exemples application tooreceive de données à partir de SensorTag d’activer et de votre hub IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "application de tableau, capteur analyser l’application, collecte de données de capteur, données depuis les capteurs, toocloud de données de capteur"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="7c0ed-104">Configurer et exécuter l’exemple d’application BLE</span><span class="sxs-lookup"><span data-stu-id="7c0ed-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="7c0ed-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="7c0ed-105">What you will do</span></span>

- <span data-ttu-id="7c0ed-106">Dépôt d’exemples hello clone.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-106">Clone hello sample repository.</span></span> 
- <span data-ttu-id="7c0ed-107">Configurer une connectivité hello entre SensorTag et NUC d’Intel.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-107">Set up hello connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="7c0ed-108">Utilisez hello CLI d’Azure tooget votre IoT hub et les informations de SensorTag pour un exemple d’application BLE (Bluetooth faible consommation d’énergie).</span><span class="sxs-lookup"><span data-stu-id="7c0ed-108">Use hello Azure CLI tooget your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="7c0ed-109">Configurer et exécuter hello BLE exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-109">And configure and run hello BLE sample application.</span></span> 

<span data-ttu-id="7c0ed-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7c0ed-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7c0ed-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="7c0ed-111">What you will learn</span></span>

<span data-ttu-id="7c0ed-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-112">In this article, you will learn:</span></span>

- <span data-ttu-id="7c0ed-113">Comment tooconfigure et exécution hello BLE exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-113">How tooconfigure and run hello BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7c0ed-114">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="7c0ed-114">What you need</span></span>

<span data-ttu-id="7c0ed-115">Vous devez avoir accompli les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-115">You must have successfully completed</span></span>

- [<span data-ttu-id="7c0ed-116">Créer un IoT Hub et inscrire SensorTag</span><span class="sxs-lookup"><span data-stu-id="7c0ed-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="7c0ed-117">Cloner l’ordinateur hôte toohello hello exemple référentiel</span><span class="sxs-lookup"><span data-stu-id="7c0ed-117">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="7c0ed-118">dépôt d’exemples tooclone hello, procédez comme suit sur l’ordinateur hôte hello :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-118">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="7c0ed-119">Ouvrez une invite de commande dans Windows ou ouvrez une fenêtre de terminal dans macOS ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="7c0ed-120">Exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-120">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="7c0ed-121">Configurer une connectivité hello entre SensorTag et Intel NUC</span><span class="sxs-lookup"><span data-stu-id="7c0ed-121">Set up hello connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="7c0ed-122">tooset la connectivité de hello, procédez comme suit sur l’ordinateur hôte hello :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-122">tooset up hello connectivity, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="7c0ed-123">Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-123">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="7c0ed-124">Ouvrez `config-gateway.json` dans le Code de Visual Studio en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-124">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="7c0ed-125">Recherchez hello ligne de code suivante et remplacez `[device hostname or IP address]` avec hello IP adresse nom d’hôte ou NUC d’Intel.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-125">Locate hello following line of code and replace `[device hostname or IP address]` with hello IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="7c0ed-126">![capture d’écran de la passerelle de configuration](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="7c0ed-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="7c0ed-127">Installer les outils d’assistance sur Intel NUC en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-127">Install helper tools on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="7c0ed-128">SensorTag sous tension en appuyant sur bouton d’alimentation hello hello illustration suivante et hello que vert clignote.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-128">Turn on SensorTag by pressing hello power button as hello following picture, and hello green LED should blink.</span></span>

   ![activer le SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="7c0ed-130">SensorTag de périphériques de numérisation en exécutant hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-130">Scan SensorTag devices by running hello following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="7c0ed-131">Tester la connectivité de hello entre hello SensorTag et Intel NUC en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-131">Test hello connectivity between hello SensorTag and Intel NUC by running hello following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="7c0ed-132">Remplacez `{mac address}` par hello adresse MAC que vous avez obtenu à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-132">Replace `{mac address}` with hello MAC address that you obtained in hello previous step.</span></span>

## <a name="get-hello-connection-string-of-sensortag"></a><span data-ttu-id="7c0ed-133">Obtenir la chaîne de connexion hello de SensorTag</span><span class="sxs-lookup"><span data-stu-id="7c0ed-133">Get hello connection string of SensorTag</span></span>

<span data-ttu-id="7c0ed-134">hello tooget chaîne de connexion Azure IoT hub de SensorTag, exécutez hello commande sur l’ordinateur hôte hello suivante :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-134">tooget hello Azure IoT hub connection string of SensorTag, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="7c0ed-135">`{IoT hub name}`est le nom de hub IoT hello que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-135">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="7c0ed-136">Utilisez iot-passerelle en tant que valeur hello `{resource group name}` et utiliser mydevice en tant que valeur hello `{device id}` si vous n’avez pas modifier la valeur hello dans la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-136">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-ble-sample-application"></a><span data-ttu-id="7c0ed-137">Configurez hello BLE exemple d’application</span><span class="sxs-lookup"><span data-stu-id="7c0ed-137">Configure hello BLE sample application</span></span>

<span data-ttu-id="7c0ed-138">tooconfigure et exécution hello exemple d’application BLE, procédez comme suit sur l’ordinateur hôte hello :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-138">tooconfigure and run hello BLE sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="7c0ed-139">Ouvrez `config-sensortag.json` dans le Code de Visual Studio en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-139">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![capture d’écran de configuration sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="7c0ed-141">Rendre hello suivant des remplacements dans le code hello :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-141">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="7c0ed-142">Remplacez `[IoT hub name]` avec le nom de hub IoT hello que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-142">Replace `[IoT hub name]` with hello IoT hub name that you used.</span></span>
   - <span data-ttu-id="7c0ed-143">Remplacez `[IoT device connection string]` avec la chaîne de connexion hello de SensorTag que vous avez obtenu.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-143">Replace `[IoT device connection string]` with hello connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="7c0ed-144">Remplacez `[device_mac_address]` par hello adresse MAC de hello SensorTag que vous avez obtenu.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-144">Replace `[device_mac_address]` with hello MAC address of hello SensorTag that you obtained.</span></span>

3. <span data-ttu-id="7c0ed-145">Exécutez hello BLE exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-145">Run hello BLE sample application.</span></span>

   <span data-ttu-id="7c0ed-146">toorun hello exemple d’application BLE, procédez comme suit sur l’ordinateur hôte hello :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-146">toorun hello BLE sample application, follow these steps on hello host computer:</span></span>

   1. <span data-ttu-id="7c0ed-147">Activez le SensorTag.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="7c0ed-148">Déployer et exécuter des application d’exemple hello BLE sur Intel NUC en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-148">Deploy and run hello BLE sample application on Intel NUC by running hello following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a><span data-ttu-id="7c0ed-149">Vérifiez que hello BLE exemple d’application fonctionne</span><span class="sxs-lookup"><span data-stu-id="7c0ed-149">Verify that hello BLE sample application works</span></span>

<span data-ttu-id="7c0ed-150">Vous devez maintenant voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="7c0ed-150">You should now see an output like hello following:</span></span>

![Résultats de l’exemple d’application BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="7c0ed-152">exemple d’application Hello conserve la collecte de données de la température et envoyé tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-152">hello sample application keeps collecting temperature data and sent it tooyour IoT hub.</span></span> <span data-ttu-id="7c0ed-153">exemple d’application Hello se termine automatiquement après l’envoi de 40 secondes.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-153">hello sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="7c0ed-154">Résumé</span><span class="sxs-lookup"><span data-stu-id="7c0ed-154">Summary</span></span>

<span data-ttu-id="7c0ed-155">Vous avez correctement défini la connectivité hello entre SensorTag et Intel NUC et exécuter un exemple d’application BLE qui collecte et envoie des données à partir de SensorTag tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-155">You've successfully set up hello connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag tooyour IoT hub.</span></span> <span data-ttu-id="7c0ed-156">Vous êtes prêt toolearn comment tooverify votre hub IoT a reçu hello des données.</span><span class="sxs-lookup"><span data-stu-id="7c0ed-156">You're ready toolearn how tooverify that your IoT hub has received hello data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c0ed-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c0ed-157">Next steps</span></span>
[<span data-ttu-id="7c0ed-158">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7c0ed-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)