---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 3 : Exécuter un exemple d’application | Microsoft Docs"
description: "Exécuter un exemple d’application BLE pour recevoir des données à partir du SensorTag BLE et de votre IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "application ble, application de surveillance de capteur, collecte des données de capteur, données de capteurs, données de capteur vers le cloud"
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
ms.openlocfilehash: f6fa158dbe1d48be7d493efa6217e1e0a759d2f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="194a4-104">Configurer et exécuter l’exemple d’application BLE</span><span class="sxs-lookup"><span data-stu-id="194a4-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="194a4-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="194a4-105">What you will do</span></span>

- <span data-ttu-id="194a4-106">Clonez l'exemple de référentiel.</span><span class="sxs-lookup"><span data-stu-id="194a4-106">Clone the sample repository.</span></span> 
- <span data-ttu-id="194a4-107">Configurez la connectivité entre SensorTag et Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="194a4-107">Set up the connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="194a4-108">Utilisez l’interface de ligne de commande Azure pour obtenir vos informations d’IoT Hub et de SensorTag pour un exemple d’application BLE (Bluetooth basse énergie).</span><span class="sxs-lookup"><span data-stu-id="194a4-108">Use the Azure CLI to get your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="194a4-109">Configuration et exécution de l’exemple d’application BLE.</span><span class="sxs-lookup"><span data-stu-id="194a4-109">And configure and run the BLE sample application.</span></span> 

<span data-ttu-id="194a4-110">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="194a4-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="194a4-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="194a4-111">What you will learn</span></span>

<span data-ttu-id="194a4-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="194a4-112">In this article, you will learn:</span></span>

- <span data-ttu-id="194a4-113">Configuration et exécution de l’exemple d’application BLE.</span><span class="sxs-lookup"><span data-stu-id="194a4-113">How to configure and run the BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="194a4-114">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="194a4-114">What you need</span></span>

<span data-ttu-id="194a4-115">Vous devez avoir accompli les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="194a4-115">You must have successfully completed</span></span>

- [<span data-ttu-id="194a4-116">Créer un IoT Hub et inscrire SensorTag</span><span class="sxs-lookup"><span data-stu-id="194a4-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="194a4-117">Cloner l'exemple de référentiel sur l’ordinateur hôte</span><span class="sxs-lookup"><span data-stu-id="194a4-117">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="194a4-118">Pour cloner l'exemple de référentiel, procédez comme suit sur l’ordinateur hôte :</span><span class="sxs-lookup"><span data-stu-id="194a4-118">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="194a4-119">Ouvrez une invite de commande dans Windows ou ouvrez une fenêtre de terminal dans macOS ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="194a4-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="194a4-120">Exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="194a4-120">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-the-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="194a4-121">Configurer la connectivité entre SensorTag et Intel NUC</span><span class="sxs-lookup"><span data-stu-id="194a4-121">Set up the connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="194a4-122">Pour configurer la connectivité, procédez comme suit sur l’ordinateur hôte :</span><span class="sxs-lookup"><span data-stu-id="194a4-122">To set up the connectivity, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="194a4-123">Initialisez le fichier de configuration en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="194a4-123">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="194a4-124">Ouvrez `config-gateway.json` dans Visual Studio Code en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="194a4-124">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="194a4-125">Recherchez la ligne de code suivante et remplacez `[device hostname or IP address]` par l’adresse IP ou le nom d'hôte de l’Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="194a4-125">Locate the following line of code and replace `[device hostname or IP address]` with the IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="194a4-126">![capture d’écran de la passerelle de configuration](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="194a4-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="194a4-127">Installez les outils d’assistance sur l’Intel NUC en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="194a4-127">Install helper tools on Intel NUC by running the following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="194a4-128">Activez SensorTag en appuyant sur le bouton d’alimentation comme indiqué sur l’image suivante, et le voyant vert clignote.</span><span class="sxs-lookup"><span data-stu-id="194a4-128">Turn on SensorTag by pressing the power button as the following picture, and the green LED should blink.</span></span>

   ![activer le SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="194a4-130">Analysez les appareils SensorTag en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="194a4-130">Scan SensorTag devices by running the following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="194a4-131">Testez la connectivité entre le SensorTag et l’Intel NUC en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="194a4-131">Test the connectivity between the SensorTag and Intel NUC by running the following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="194a4-132">Remplacez `{mac address}` par l’adresse MAC que vous avez obtenue à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="194a4-132">Replace `{mac address}` with the MAC address that you obtained in the previous step.</span></span>

## <a name="get-the-connection-string-of-sensortag"></a><span data-ttu-id="194a4-133">Obtention de la chaîne de connexion du SensorTag</span><span class="sxs-lookup"><span data-stu-id="194a4-133">Get the connection string of SensorTag</span></span>

<span data-ttu-id="194a4-134">Pour obtenir la chaîne de connexion Azure IoT Hub de SensorTag, exécutez la commande suivante sur l’ordinateur hôte :</span><span class="sxs-lookup"><span data-stu-id="194a4-134">To get the Azure IoT hub connection string of SensorTag, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="194a4-135">`{IoT hub name}` est le nom de l'IoT Hub que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="194a4-135">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="194a4-136">Utilisez iot-gateway en tant que valeur de `{resource group name}` et mydevice en tant que valeur de `{device id}` si vous n'avez pas modifié la valeur à la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="194a4-136">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-ble-sample-application"></a><span data-ttu-id="194a4-137">Configuration et exécution de l’exemple d’application BLE</span><span class="sxs-lookup"><span data-stu-id="194a4-137">Configure the BLE sample application</span></span>

<span data-ttu-id="194a4-138">Pour configurer et exécuter l’exemple d’application BLE, procédez comme suit sur l’ordinateur hôte :</span><span class="sxs-lookup"><span data-stu-id="194a4-138">To configure and run the BLE sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="194a4-139">Ouvrez `config-sensortag.json` dans Visual Studio Code en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="194a4-139">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![capture d’écran de configuration sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="194a4-141">Effectuez les remplacements suivants dans le code :</span><span class="sxs-lookup"><span data-stu-id="194a4-141">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="194a4-142">Remplacez `[IoT hub name]` par le nom de l'IoT Hub que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="194a4-142">Replace `[IoT hub name]` with the IoT hub name that you used.</span></span>
   - <span data-ttu-id="194a4-143">Remplacez `[IoT device connection string]` par la chaîne de connexion SensorTag que vous avez obtenue.</span><span class="sxs-lookup"><span data-stu-id="194a4-143">Replace `[IoT device connection string]` with the connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="194a4-144">Remplacez `[device_mac_address]` par l’adresse MAC de SensorTag que vous avez obtenue.</span><span class="sxs-lookup"><span data-stu-id="194a4-144">Replace `[device_mac_address]` with the MAC address of the SensorTag that you obtained.</span></span>

3. <span data-ttu-id="194a4-145">Exécutez l’exemple d’application BLE.</span><span class="sxs-lookup"><span data-stu-id="194a4-145">Run the BLE sample application.</span></span>

   <span data-ttu-id="194a4-146">Pour exécuter l’exemple d’application BLE, procédez comme suit sur l’ordinateur hôte :</span><span class="sxs-lookup"><span data-stu-id="194a4-146">To run the BLE sample application, follow these steps on the host computer:</span></span>

   1. <span data-ttu-id="194a4-147">Activez le SensorTag.</span><span class="sxs-lookup"><span data-stu-id="194a4-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="194a4-148">Déployez et exécutez l’exemple d’application BLE sur l’Intel NUC en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="194a4-148">Deploy and run the BLE sample application on Intel NUC by running the following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-the-ble-sample-application-works"></a><span data-ttu-id="194a4-149">Vérification du bon fonctionnement de l’exemple d’application BLE</span><span class="sxs-lookup"><span data-stu-id="194a4-149">Verify that the BLE sample application works</span></span>

<span data-ttu-id="194a4-150">Un résultat similaire à ce qui suit doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="194a4-150">You should now see an output like the following:</span></span>

![Résultats de l’exemple d’application BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="194a4-152">L’exemple d’application assure la collecte des données de température et les envoie à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="194a4-152">The sample application keeps collecting temperature data and sent it to your IoT hub.</span></span> <span data-ttu-id="194a4-153">L’exemple d’application se termine automatiquement après l’envoi pendant 40 secondes.</span><span class="sxs-lookup"><span data-stu-id="194a4-153">The sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="194a4-154">Résumé</span><span class="sxs-lookup"><span data-stu-id="194a4-154">Summary</span></span>

<span data-ttu-id="194a4-155">Vous avez correctement configuré la connectivité entre le SensorTag et l’Intel NUC et exécuté un exemple d’application BLE qui collecte et envoie des données à partir de SensorTag vers votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="194a4-155">You've successfully set up the connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag to your IoT hub.</span></span> <span data-ttu-id="194a4-156">Vous êtes prêt à apprendre à vérifier que votre IoT Hub a reçu les données.</span><span class="sxs-lookup"><span data-stu-id="194a4-156">You're ready to learn how to verify that your IoT hub has received the data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="194a4-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="194a4-157">Next steps</span></span>
[<span data-ttu-id="194a4-158">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="194a4-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)