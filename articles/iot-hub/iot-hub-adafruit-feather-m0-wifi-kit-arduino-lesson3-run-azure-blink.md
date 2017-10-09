---
title: "Connect Arduino (C) tooAzure IoT - leçon 3 : exécuter l’exemple | Documents Microsoft"
description: "Déployer et exécuter un tooAdafruit d’application exemple estompe M0 Wi-Fi qui envoie l’IoT hub tooyour de messages et clignote hello DEL."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "service de cloud IOT, arduino envoyer des données toocloud"
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
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="50b6e-104">Exécuter un toosend d’application exemple messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="50b6e-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="50b6e-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="50b6e-105">What you will do</span></span>
<span data-ttu-id="50b6e-106">Cet article vous explique comment toodeploy et exécuter un exemple d’application sur votre Arduino de Wi-Fi Adafruit estompe M0 board qui envoie les messages tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="50b6e-106">This article will show you how toodeploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages tooyour IoT hub.</span></span>

<span data-ttu-id="50b6e-107">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="50b6e-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="50b6e-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="50b6e-108">What you will learn</span></span>
<span data-ttu-id="50b6e-109">Vous allez apprendre comment toouse hello gulp outil toodeploy et exécuter l’exemple d’application de Arduino hello dans votre tableau de Arduino.</span><span class="sxs-lookup"><span data-stu-id="50b6e-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="50b6e-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="50b6e-110">What you need</span></span>
* <span data-ttu-id="50b6e-111">Avant de commencer cette tâche, vous devez avoir terminé avec succès [créer une application de la fonction Azure et un stockage compte tooprocess et magasin IoT hub messages][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="50b6e-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="50b6e-112">Obtenir vos chaînes de connexion d’IoT Hub et d’appareil</span><span class="sxs-lookup"><span data-stu-id="50b6e-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="50b6e-113">Hello la chaîne de connexion de périphérique est tooconnect utilisé votre concentrateur de IoT tooyour Arduino du tableau.</span><span class="sxs-lookup"><span data-stu-id="50b6e-113">hello device connection string is used tooconnect your Arduino board tooyour IoT hub.</span></span> <span data-ttu-id="50b6e-114">chaîne de connexion de hub IoT Hello est tooconnect utilisé votre identité d’appareil IoT hub toohello qui représente votre Arduino board dans le hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="50b6e-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents your Arduino board in hello IoT hub.</span></span>

* <span data-ttu-id="50b6e-115">Liste de tous vos hubs IoT dans votre groupe de ressources en exécutant hello suivant commande CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="50b6e-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="50b6e-116">Utilisez `iot-sample` en tant que valeur hello `{resource group name}` si vous n’avez modifié la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="50b6e-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="50b6e-117">Obtenir la chaîne de connexion de hub IoT hello en exécutant hello suivant commande CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="50b6e-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="50b6e-118">`{my hub name}`est le nom hello que vous avez spécifié lorsque vous créez votre hub IoT et inscrit votre tableau Arduino.</span><span class="sxs-lookup"><span data-stu-id="50b6e-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="50b6e-119">Obtenir la chaîne de connexion de périphérique de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="50b6e-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="50b6e-120">Utilisez `mym0wifi` en tant que valeur hello `{device id}` si vous n’avez modifié la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="50b6e-120">Use `mym0wifi` as hello value of `{device id}` if you didn't change hello value.</span></span>
## <a name="configure-hello-device-connection"></a><span data-ttu-id="50b6e-121">Configurer la connexion du périphérique hello</span><span class="sxs-lookup"><span data-stu-id="50b6e-121">Configure hello device connection</span></span>
<span data-ttu-id="50b6e-122">tooconfigure hello connexion du périphérique, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="50b6e-122">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="50b6e-123">Obtenir le port série de hello du périphérique hello avec cli de découverte de périphérique hello :</span><span class="sxs-lookup"><span data-stu-id="50b6e-123">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="50b6e-124">Vous devez voir une sortie similaire toohello suivant et trouver hello usb port COM de votre carte Arduino :</span><span class="sxs-lookup"><span data-stu-id="50b6e-124">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Découverte de l’appareil][device-discovery]

2. <span data-ttu-id="50b6e-126">Les fichiers ouverts hello `config.json` hello du dossier de la leçon et ajouter la valeur hello hello trouvé le numéro de port COM :</span><span class="sxs-lookup"><span data-stu-id="50b6e-126">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="50b6e-128">Pour le port COM de hello, sur la plateforme Windows, d’un format de hello `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="50b6e-128">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="50b6e-129">Sur macOS ou Ubuntu, il commence par `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="50b6e-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="50b6e-130">Initialisation du fichier de configuration de hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="50b6e-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="50b6e-131">Fichier de configuration de périphérique ouvert hello `config-arduino.json` dans le Code de Visual Studio en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="50b6e-131">Open hello device configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="50b6e-133">Rendre hello suivant remplacements Bonjour `config-arduino.json` fichier :</span><span class="sxs-lookup"><span data-stu-id="50b6e-133">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   * <span data-ttu-id="50b6e-134">Remplacez **[Wi-Fi SSID]** avec votre SSID Wi-Fi qui connectés toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="50b6e-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="50b6e-135">Remplacez **[Wi-Fi password]** par votre mot de passe Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="50b6e-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="50b6e-136">Supprimez la chaîne de hello si votre Wi-Fi ne nécessite pas un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="50b6e-136">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="50b6e-137">Remplacez **[chaîne de connexion de périphérique IoT]** avec hello `device connection string` obtenues.</span><span class="sxs-lookup"><span data-stu-id="50b6e-137">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="50b6e-138">Remplacez **[chaîne de connexion de hub IoT]** avec hello `iot hub connection string` obtenues.</span><span class="sxs-lookup"><span data-stu-id="50b6e-138">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="50b6e-139">Vous n’avez pas besoin de `azure_storage_connection_string` dans cet article.</span><span class="sxs-lookup"><span data-stu-id="50b6e-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="50b6e-140">Gardez-le tel quel.</span><span class="sxs-lookup"><span data-stu-id="50b6e-140">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="50b6e-141">Déployer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="50b6e-141">Deploy and run hello sample application</span></span>
<span data-ttu-id="50b6e-142">Déployer et exécuter des application d’exemple hello sur votre carte mère Arduino en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="50b6e-142">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="50b6e-143">Hello par défaut gulp tâche s’exécute `install-tools` et `run` tâches séquentiellement.</span><span class="sxs-lookup"><span data-stu-id="50b6e-143">hello default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="50b6e-144">Lorsque vous [hello blink application déployée][deployed-the-blink-app], vous avez exécuté ces tâches séparément.</span><span class="sxs-lookup"><span data-stu-id="50b6e-144">When you [deployed hello blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="50b6e-145">Vérifiez que hello exemple application fonctionne</span><span class="sxs-lookup"><span data-stu-id="50b6e-145">Verify that hello sample application works</span></span>
<span data-ttu-id="50b6e-146">Vous devez voir hello GPIO #0 intégrée LED clignote toutes les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="50b6e-146">You should see hello GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="50b6e-147">Chaque fois que hello LED clignote, exemple d’application hello envoie un hub IoT de tooyour message et vérifie que ce message de type hello a été envoyé avec succès tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="50b6e-147">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="50b6e-148">En outre, chaque message reçu par IoT hub de hello est imprimé dans la fenêtre de console hello.</span><span class="sxs-lookup"><span data-stu-id="50b6e-148">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="50b6e-149">exemple d’application Hello se termine automatiquement après l’envoi des messages de 20.</span><span class="sxs-lookup"><span data-stu-id="50b6e-149">hello sample application terminates automatically after sending 20 messages.</span></span>

![Exemple d’application avec des messages envoyés et reçus][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="50b6e-151">Résumé</span><span class="sxs-lookup"><span data-stu-id="50b6e-151">Summary</span></span>
<span data-ttu-id="50b6e-152">Vous avez déployé et exécuter hello nouvelle blink exemple d’application sur votre IoT hub tooyour de messages appareil-à-cloud toosend Arduino du tableau.</span><span class="sxs-lookup"><span data-stu-id="50b6e-152">You've deployed and run hello new blink sample application on your Arduino board toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="50b6e-153">Vous surveillez maintenant vos messages qu’ils sont écrits de compte de stockage toohello.</span><span class="sxs-lookup"><span data-stu-id="50b6e-153">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50b6e-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="50b6e-154">Next steps</span></span>
<span data-ttu-id="50b6e-155">[Lecture des messages conservés dans le stockage Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="50b6e-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md