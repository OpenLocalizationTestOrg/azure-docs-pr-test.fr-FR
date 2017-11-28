---
title: "Connecter Raspberry Pi (Node) à Azure IoT - Leçon 3 : Exécuter un exemple | Microsoft Docs"
description: "Déployez et exécutez sur Raspberry Pi 3 un exemple d’application qui envoie des messages à votre IoT Hub et fait clignoter la LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "led clignotante cloud pi, clignotement led à partir du cloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1c03283ee276a954f822d6eca5f0a3d5f93ec64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="d07da-104">Exécution d’un exemple d’application pour envoyer des messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="d07da-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d07da-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="d07da-105">What you will do</span></span>
<span data-ttu-id="d07da-106">Cet article vous explique comment déployer et exécuter sur Raspberry Pi 3 un exemple d’application qui envoie des messages à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d07da-106">This article will show you how to deploy and run a sample application on Raspberry Pi 3 that sends messages to your IoT hub.</span></span> <span data-ttu-id="d07da-107">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d07da-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d07da-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="d07da-108">What you will learn</span></span>
<span data-ttu-id="d07da-109">Vous apprendrez à utiliser l’outil gulp pour déployer et exécuter l’exemple d’application Node.js sur Pi.</span><span class="sxs-lookup"><span data-stu-id="d07da-109">You will learn how to use the gulp tool to deploy and run the sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d07da-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="d07da-110">What you need</span></span>
* <span data-ttu-id="d07da-111">Avant de commencer cette tâche, vous devez avoir correctement suivi la section [Création d’une application de fonction Azure et d’un compte de stockage pour traiter et stocker des messages du IoT Hub](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="d07da-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="d07da-112">Obtenir vos chaînes de connexion d’IoT Hub et d’appareil</span><span class="sxs-lookup"><span data-stu-id="d07da-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="d07da-113">La chaîne de connexion de l’appareil permet de connecter votre Pi à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d07da-113">The device connection string is used by your Pi to connect to your IoT hub.</span></span> <span data-ttu-id="d07da-114">La chaîne de connexion IoT Hub sert à se connecter au registre des identités de votre IoT Hub pour gérer les appareils autorisés à se connecter à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d07da-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span> 

* <span data-ttu-id="d07da-115">Répertorier tous les IoT Hubs de votre groupe de ressources en exécutant la commande suivante de l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="d07da-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="d07da-116">Si vous n’avez pas modifié la valeur, utilisez `iot-sample` en tant que valeur de `{resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="d07da-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="d07da-117">Obtenez la chaîne de connexion de l’IoT Hub en exécutant la commande de l’interface de ligne de commande Azure suivante :</span><span class="sxs-lookup"><span data-stu-id="d07da-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="d07da-118">`{my hub name}` est le nom que vous avez spécifié lorsque vous avez créé votre IoT Hub et inscrit Pi.</span><span class="sxs-lookup"><span data-stu-id="d07da-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="d07da-119">Obtenez la chaîne de connexion de l’appareil en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d07da-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="d07da-120">Si vous n’avez pas modifié la valeur, utilisez `myraspberrypi` en tant que valeur de `{device id}`.</span><span class="sxs-lookup"><span data-stu-id="d07da-120">Use `myraspberrypi` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="d07da-121">Configuration de la connexion de l’appareil</span><span class="sxs-lookup"><span data-stu-id="d07da-121">Configure the device connection</span></span>
1. <span data-ttu-id="d07da-122">Initialisez le fichier de configuration en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d07da-122">Initialize the configuration file by running the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
2. <span data-ttu-id="d07da-123">Ouvrez le fichier de configuration de l’appareil `config-raspberrypi.json` dans Visual Studio Code en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d07da-123">Open the device configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="d07da-125">Dans le fichier `config-raspberrypi.json`, effectuez les remplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="d07da-125">Make the following replacements in the `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="d07da-126">Remplacez **[nom d’hôte ou adresse IP de l’appareil]** par l’adresse IP ou le nom d’hôte d’appareil obtenu(e) à l’aide de la commande `device-discovery-cli`, ou par la valeur héritée lorsque vous avez configuré votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d07da-126">Replace **[device hostname or IP address]** with the device IP address or host name you got from `device-discovery-cli` or with the value inherited when you configured your device.</span></span>
   * <span data-ttu-id="d07da-127">Remplacez **[chaîne de connexion de l’appareil IoT]** par la `device connection string` obtenue.</span><span class="sxs-lookup"><span data-stu-id="d07da-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="d07da-128">Remplacez **[chaîne de connexion d’IoT Hub]** par la `iot hub connection string` obtenue.</span><span class="sxs-lookup"><span data-stu-id="d07da-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

<span data-ttu-id="d07da-129">Mettez à jour le fichier `config-raspberrypi.json` afin de pouvoir déployer l’exemple d’application à partir de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d07da-129">Update the `config-raspberrypi.json` file so that you can deploy the sample application from your computer.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="d07da-130">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="d07da-130">Deploy and run the sample application</span></span>
<span data-ttu-id="d07da-131">Déployez et exécutez l’exemple d’application sur Pi en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d07da-131">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="d07da-132">Vérification du bon fonctionnement de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="d07da-132">Verify that the sample application works</span></span>
<span data-ttu-id="d07da-133">Vous devez voir la LED connectée à Pi clignoter toutes les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="d07da-133">You should see the LED that is connected to Pi blinking every two seconds.</span></span> <span data-ttu-id="d07da-134">Chaque fois que la LED clignote, l’exemple d’application envoie un message à votre IoT Hub et vérifie que le message a été correctement envoyé.</span><span class="sxs-lookup"><span data-stu-id="d07da-134">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="d07da-135">De plus, chaque message reçu par l’IoT Hub apparaît dans la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="d07da-135">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="d07da-136">L’exemple d’application se termine automatiquement après l’envoi de 20 messages.</span><span class="sxs-lookup"><span data-stu-id="d07da-136">The sample application terminates automatically after sending 20 messages.</span></span>

![Exemple d’application avec des messages envoyés et reçus](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a><span data-ttu-id="d07da-138">Résumé</span><span class="sxs-lookup"><span data-stu-id="d07da-138">Summary</span></span>
<span data-ttu-id="d07da-139">Vous avez déployé et exécuté le nouvel exemple d’application de clignotement sur Pi pour l’envoi de messages appareil-à-cloud à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d07da-139">You've deployed and run the new blink sample application on Pi to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="d07da-140">Vous pouvez désormais surveiller les messages à mesure qu’ils sont écrits dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d07da-140">You can now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d07da-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d07da-141">Next steps</span></span>
[<span data-ttu-id="d07da-142">Lecture des messages conservés dans le Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="d07da-142">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

