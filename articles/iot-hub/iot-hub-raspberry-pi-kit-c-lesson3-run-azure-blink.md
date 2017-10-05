---
title: "Connecter Raspberry Pi (C) à Azure IoT - Leçon 3 : Exécuter les exemples | Microsoft Docs"
description: "Déployez et exécutez sur Raspberry Pi 3 un exemple d’application qui envoie des messages à votre IoT Hub et fait clignoter la LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "led clignotante cloud pi, clignotement led à partir du cloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e583ba455a94f9afcc7b31e49425b518d7968919
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="d9209-104">Exécution d’un exemple d’application pour envoyer des messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="d9209-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d9209-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="d9209-105">What you will do</span></span>
<span data-ttu-id="d9209-106">Cet article vous explique comment déployer et exécuter sur Raspberry Pi 3 un exemple d’application qui envoie des messages à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d9209-106">This article will show you how to deploy and run a sample application on Raspberry Pi 3 that sends messages to your IoT hub.</span></span> <span data-ttu-id="d9209-107">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d9209-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d9209-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="d9209-108">What you will learn</span></span>
<span data-ttu-id="d9209-109">Vous apprendrez à utiliser l’outil gulp pour déployer et exécuter l’exemple d’application Node.js sur Pi.</span><span class="sxs-lookup"><span data-stu-id="d9209-109">You will learn how to use the gulp tool to deploy and run the sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d9209-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="d9209-110">What you need</span></span>
* <span data-ttu-id="d9209-111">Avant de commencer cette tâche, vous devez avoir correctement suivi la section [Création d’une application de fonction Azure et d’un compte de stockage pour traiter et stocker des messages du IoT Hub](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="d9209-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="d9209-112">Obtenir vos chaînes de connexion d’IoT Hub et d’appareil</span><span class="sxs-lookup"><span data-stu-id="d9209-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="d9209-113">La chaîne de connexion de l’appareil permet de connecter votre Pi à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d9209-113">The device connection string is used by your Pi to connect to your IoT hub.</span></span> <span data-ttu-id="d9209-114">La chaîne de connexion IoT Hub sert à se connecter au registre des identités de votre IoT Hub pour gérer les appareils autorisés à se connecter à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d9209-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span> 

* <span data-ttu-id="d9209-115">Répertorier tous les IoT Hubs de votre groupe de ressources en exécutant la commande suivante de l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="d9209-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="d9209-116">Si vous n’avez pas modifié la valeur, utilisez `iot-sample` en tant que valeur de `{resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="d9209-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="d9209-117">Obtenez la chaîne de connexion de l’IoT Hub en exécutant la commande de l’interface de ligne de commande Azure suivante :</span><span class="sxs-lookup"><span data-stu-id="d9209-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="d9209-118">`{my hub name}` est le nom que vous avez spécifié lorsque vous avez créé votre IoT Hub et inscrit Pi.</span><span class="sxs-lookup"><span data-stu-id="d9209-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="d9209-119">Obtenez la chaîne de connexion de l’appareil en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d9209-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="d9209-120">Si vous n’avez pas modifié la valeur, utilisez `myraspberrypi` en tant que valeur de `{device id}`.</span><span class="sxs-lookup"><span data-stu-id="d9209-120">Use `myraspberrypi` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="d9209-121">Configuration de la connexion de l’appareil</span><span class="sxs-lookup"><span data-stu-id="d9209-121">Configure the device connection</span></span>
1. <span data-ttu-id="d9209-122">Initialisez le fichier de configuration en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9209-122">Initialize the configuration file by running the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> <span data-ttu-id="d9209-123">Exécutez également **gulp install-tools**, si vous ne l’avez pas fait dans la leçon 1.</span><span class="sxs-lookup"><span data-stu-id="d9209-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="d9209-124">Ouvrez le fichier de configuration de l’appareil `config-raspberrypi.json` dans Visual Studio Code en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d9209-124">Open the device configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="d9209-126">Dans le fichier `config-raspberrypi.json`, effectuez les remplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="d9209-126">Make the following replacements in the `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="d9209-127">Remplacez **[nom d’hôte ou adresse IP de l’appareil]** par l’adresse IP ou le nom d’hôte d’appareil obtenu(e) à l’aide de la commande `device-discovery-cli`, ou par la valeur héritée lorsque vous avez configuré votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d9209-127">Replace **[device hostname or IP address]** with the device IP address or host name you got from `device-discovery-cli` or with the value inherited when you configured your device.</span></span>
   * <span data-ttu-id="d9209-128">Remplacez **[chaîne de connexion de l’appareil IoT]** par la `device connection string` obtenue.</span><span class="sxs-lookup"><span data-stu-id="d9209-128">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="d9209-129">Remplacez **[chaîne de connexion d’IoT Hub]** par la `iot hub connection string` obtenue.</span><span class="sxs-lookup"><span data-stu-id="d9209-129">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

> [!NOTE]
> <span data-ttu-id="d9209-130">Vous n’avez pas besoin de `azure_storage_connection_string` dans cet article.</span><span class="sxs-lookup"><span data-stu-id="d9209-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="d9209-131">Gardez-le tel quel.</span><span class="sxs-lookup"><span data-stu-id="d9209-131">Keep it as is.</span></span>

<span data-ttu-id="d9209-132">Mettez à jour le fichier `config-raspberrypi.json` afin de pouvoir déployer l’exemple d’application à partir de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d9209-132">Update the `config-raspberrypi.json` file so that you can deploy the sample application from your computer.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="d9209-133">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="d9209-133">Deploy and run the sample application</span></span>
<span data-ttu-id="d9209-134">Déployez et exécutez l’exemple d’application sur Pi en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d9209-134">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="d9209-135">Vérification du bon fonctionnement de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="d9209-135">Verify that the sample application works</span></span>
<span data-ttu-id="d9209-136">Vous devez voir la LED connectée à Pi clignoter toutes les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="d9209-136">You should see the LED that is connected to Pi blinking every two seconds.</span></span> <span data-ttu-id="d9209-137">Chaque fois que la LED clignote, l’exemple d’application envoie un message à votre IoT Hub et vérifie que le message a été correctement envoyé.</span><span class="sxs-lookup"><span data-stu-id="d9209-137">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="d9209-138">De plus, chaque message reçu par l’IoT Hub apparaît dans la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="d9209-138">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="d9209-139">L’exemple d’application se termine automatiquement après l’envoi de 20 messages.</span><span class="sxs-lookup"><span data-stu-id="d9209-139">The sample application terminates automatically after sending 20 messages.</span></span>

![Exemple d’application avec des messages envoyés et reçus](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a><span data-ttu-id="d9209-141">Résumé</span><span class="sxs-lookup"><span data-stu-id="d9209-141">Summary</span></span>
<span data-ttu-id="d9209-142">Vous avez déployé et exécuté le nouvel exemple d’application de clignotement sur Pi pour l’envoi de messages appareil-à-cloud à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d9209-142">You've deployed and run the new blink sample application on Pi to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="d9209-143">Vous surveillez désormais les messages à mesure qu’ils sont écrits dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d9209-143">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9209-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9209-144">Next steps</span></span>
[<span data-ttu-id="d9209-145">Lecture des messages conservés dans le Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="d9209-145">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

