---
title: "Connecter Arduino (C) à Azure IoT - Leçon 3 : Exécuter les exemples | Microsoft Docs"
description: "Déployez et exécutez sur Adafruit Feather M0 WiFi un exemple d’application qui envoie des messages à votre IoT Hub et fait clignoter la LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "service cloud iot, envoi de données au cloud arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c17fe74dbd78abca955f7789a1674ed6333367f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="772eb-104">Exécution d’un exemple d’application pour envoyer des messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="772eb-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="772eb-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="772eb-105">What you will do</span></span>
<span data-ttu-id="772eb-106">Cet article vous explique comment déployer et exécuter sur votre carte Adafruit Feather M0 WiFi Arduino un exemple d’application qui envoie des messages à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="772eb-106">This article will show you how to deploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages to your IoT hub.</span></span>

<span data-ttu-id="772eb-107">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="772eb-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="772eb-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="772eb-108">What you will learn</span></span>
<span data-ttu-id="772eb-109">Vous apprendrez à utiliser l’outil gulp pour déployer et exécuter l’exemple d’application Arduino sur votre carte Arduino.</span><span class="sxs-lookup"><span data-stu-id="772eb-109">You will learn how to use the gulp tool to deploy and run the sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="772eb-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="772eb-110">What you need</span></span>
* <span data-ttu-id="772eb-111">Avant de commencer cette tâche, vous devez avoir correctement suivi la section [Création d’une application de fonction Azure et d’un compte de stockage pour traiter et stocker des messages du IoT Hub][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="772eb-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="772eb-112">Obtenir vos chaînes de connexion d’IoT Hub et d’appareil</span><span class="sxs-lookup"><span data-stu-id="772eb-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="772eb-113">La chaîne de connexion de l’appareil permet de connecter votre carte Arduino à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="772eb-113">The device connection string is used to connect your Arduino board to your IoT hub.</span></span> <span data-ttu-id="772eb-114">La chaîne de connexion de l’IoT Hub permet de connecter votre IoT Hub à l’identité d’appareil représentant votre carte Arduino dans l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="772eb-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents your Arduino board in the IoT hub.</span></span>

* <span data-ttu-id="772eb-115">Répertorier tous les IoT Hubs de votre groupe de ressources en exécutant la commande suivante de l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="772eb-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="772eb-116">Si vous n’avez pas modifié la valeur, utilisez `iot-sample` en tant que valeur de `{resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="772eb-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="772eb-117">Obtenez la chaîne de connexion de l’IoT Hub en exécutant la commande de l’interface de ligne de commande Azure suivante :</span><span class="sxs-lookup"><span data-stu-id="772eb-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="772eb-118">`{my hub name}` est le nom que vous avez spécifié lorsque vous avez créé votre IoT Hub et inscrit votre carte Arduino.</span><span class="sxs-lookup"><span data-stu-id="772eb-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="772eb-119">Obtenez la chaîne de connexion de l’appareil en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="772eb-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="772eb-120">Si vous n’avez pas modifié la valeur, utilisez `mym0wifi` en tant que valeur de `{device id}`.</span><span class="sxs-lookup"><span data-stu-id="772eb-120">Use `mym0wifi` as the value of `{device id}` if you didn't change the value.</span></span>
## <a name="configure-the-device-connection"></a><span data-ttu-id="772eb-121">Configuration de la connexion de l’appareil</span><span class="sxs-lookup"><span data-stu-id="772eb-121">Configure the device connection</span></span>
<span data-ttu-id="772eb-122">Procédez comme suit pour configurer la connexion de l’appareil :</span><span class="sxs-lookup"><span data-stu-id="772eb-122">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="772eb-123">Obtenez le port série de l'appareil à l'aide de l’interface de ligne de commande de découverte :</span><span class="sxs-lookup"><span data-stu-id="772eb-123">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="772eb-124">Vous devriez obtenir un résultat semblable à ce qui suit et identifier le port USB COM de votre carte Arduino :</span><span class="sxs-lookup"><span data-stu-id="772eb-124">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Découverte de l’appareil][device-discovery]

2. <span data-ttu-id="772eb-126">Ouvrez le fichier `config.json` dans le dossier de la leçon puis ajoutez la valeur du numéro de port COM trouvé :</span><span class="sxs-lookup"><span data-stu-id="772eb-126">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="772eb-128">Sur la plate-forme Windows, le port COM le format `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="772eb-128">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="772eb-129">Sur macOS ou Ubuntu, il commence par `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="772eb-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="772eb-130">Initialisez le fichier de configuration en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="772eb-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="772eb-131">Ouvrez le fichier de configuration de l’appareil `config-arduino.json` dans Visual Studio Code en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="772eb-131">Open the device configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="772eb-133">Dans le fichier `config-arduino.json`, effectuez les remplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="772eb-133">Make the following replacements in the `config-arduino.json` file:</span></span>

   * <span data-ttu-id="772eb-134">Remplacez **[Wi-Fi SSID]** avec votre SSID Wi-Fi connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="772eb-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="772eb-135">Remplacez **[Wi-Fi password]** par votre mot de passe Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="772eb-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="772eb-136">Supprimez la chaîne si votre réseau Wi-Fi ne requiert aucun mot de passe.</span><span class="sxs-lookup"><span data-stu-id="772eb-136">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="772eb-137">Remplacez **[chaîne de connexion de l’appareil IoT]** par la `device connection string` obtenue.</span><span class="sxs-lookup"><span data-stu-id="772eb-137">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="772eb-138">Remplacez **[chaîne de connexion d’IoT Hub]** par la `iot hub connection string` obtenue.</span><span class="sxs-lookup"><span data-stu-id="772eb-138">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="772eb-139">Vous n’avez pas besoin de `azure_storage_connection_string` dans cet article.</span><span class="sxs-lookup"><span data-stu-id="772eb-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="772eb-140">Gardez-le tel quel.</span><span class="sxs-lookup"><span data-stu-id="772eb-140">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="772eb-141">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="772eb-141">Deploy and run the sample application</span></span>
<span data-ttu-id="772eb-142">Déployez et exécutez l’exemple d’application sur votre carte Arduino en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="772eb-142">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="772eb-143">La tâche gulp par défaut exécute séquentiellement les tâches `install-tools` et `run`.</span><span class="sxs-lookup"><span data-stu-id="772eb-143">The default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="772eb-144">Lorsque vous [avez déployé l’application de clignotement (blink)][deployed-the-blink-app], vous avez exécuté ces tâches séparément.</span><span class="sxs-lookup"><span data-stu-id="772eb-144">When you [deployed the blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="772eb-145">Vérification du bon fonctionnement de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="772eb-145">Verify that the sample application works</span></span>
<span data-ttu-id="772eb-146">Vous devriez voir la LED embarquée GPIO #0 clignoter toutes les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="772eb-146">You should see the GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="772eb-147">Chaque fois que la LED clignote, l’exemple d’application envoie un message à votre IoT Hub et vérifie que le message a été correctement envoyé.</span><span class="sxs-lookup"><span data-stu-id="772eb-147">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="772eb-148">De plus, chaque message reçu par l’IoT Hub apparaît dans la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="772eb-148">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="772eb-149">L’exemple d’application se termine automatiquement après l’envoi de 20 messages.</span><span class="sxs-lookup"><span data-stu-id="772eb-149">The sample application terminates automatically after sending 20 messages.</span></span>

![Exemple d’application avec des messages envoyés et reçus][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="772eb-151">Résumé</span><span class="sxs-lookup"><span data-stu-id="772eb-151">Summary</span></span>
<span data-ttu-id="772eb-152">Vous avez déployé et exécuté le nouvel exemple d’application de clignotement sur votre carte Arduino pour l’envoi de messages appareil-à-cloud à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="772eb-152">You've deployed and run the new blink sample application on your Arduino board to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="772eb-153">Vous surveillez désormais les messages à mesure qu’ils sont écrits dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="772eb-153">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="772eb-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="772eb-154">Next steps</span></span>
<span data-ttu-id="772eb-155">[Lecture des messages conservés dans le stockage Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="772eb-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md