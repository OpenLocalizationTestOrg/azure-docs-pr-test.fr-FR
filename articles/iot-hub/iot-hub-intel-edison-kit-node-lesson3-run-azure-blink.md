---
title: "Connecter Intel Edison (Node) à Azure IoT - Leçon 3 : Envoyer des messages | Microsoft Docs"
description: "Déployez et exécutez sur Intel Edison un exemple d’application qui envoie des messages à votre IoT Hub et fait clignoter la LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "service cloud iot, envoi de données au cloud arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d4b520b9a1852a285b1e10b5b35447a54313af9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="c613f-104">Exécution d’un exemple d’application pour envoyer des messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="c613f-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c613f-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="c613f-105">What you will do</span></span>
<span data-ttu-id="c613f-106">Cet article vous explique comment déployer et exécuter sur Intel Edison un exemple d’application qui envoie des messages à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c613f-106">This article will show you how to deploy and run a sample application on Intel Edison that sends messages to your IoT hub.</span></span> <span data-ttu-id="c613f-107">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c613f-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c613f-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="c613f-108">What you will learn</span></span>
<span data-ttu-id="c613f-109">Vous apprendrez à utiliser l’outil gulp pour déployer et exécuter l’exemple d’application C sur Edison.</span><span class="sxs-lookup"><span data-stu-id="c613f-109">You will learn how to use the gulp tool to deploy and run the sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c613f-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="c613f-110">What you need</span></span>
* <span data-ttu-id="c613f-111">Avant de commencer cette tâche, vous devez avoir correctement suivi la section [Création d’une application de fonction Azure et d’un compte de stockage pour traiter et stocker des messages du IoT Hub][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="c613f-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="c613f-112">Obtenir vos chaînes de connexion d’IoT Hub et d’appareil</span><span class="sxs-lookup"><span data-stu-id="c613f-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="c613f-113">La chaîne de connexion de l’appareil permet de connecter Edison à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c613f-113">The device connection string is used to connect Edison to your IoT hub.</span></span> <span data-ttu-id="c613f-114">La chaîne de connexion de l’IoT Hub permet de connecter votre IoT Hub à l’identité d’appareil représentant Edison dans l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c613f-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents Edison in the IoT hub.</span></span>

* <span data-ttu-id="c613f-115">Répertorier tous les IoT Hubs de votre groupe de ressources en exécutant la commande suivante de l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="c613f-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="c613f-116">Si vous n’avez pas modifié la valeur, utilisez `iot-sample` en tant que valeur de `{resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="c613f-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="c613f-117">Obtenez la chaîne de connexion de l’IoT Hub en exécutant la commande de l’interface de ligne de commande Azure suivante :</span><span class="sxs-lookup"><span data-stu-id="c613f-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="c613f-118">`{my hub name}` est le nom que vous avez spécifié lorsque vous avez créé votre IoT Hub et inscrit Edison.</span><span class="sxs-lookup"><span data-stu-id="c613f-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="c613f-119">Obtenez la chaîne de connexion de l’appareil en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c613f-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="c613f-120">Si vous n’avez pas modifié la valeur, utilisez `myinteledison` en tant que valeur de `{device id}`.</span><span class="sxs-lookup"><span data-stu-id="c613f-120">Use `myinteledison` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="c613f-121">Configuration de la connexion de l’appareil</span><span class="sxs-lookup"><span data-stu-id="c613f-121">Configure the device connection</span></span>
1. <span data-ttu-id="c613f-122">Initialisez le fichier de configuration en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c613f-122">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

2. <span data-ttu-id="c613f-123">Ouvrez le fichier de configuration de l’appareil `config-edison.json` dans Visual Studio Code en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c613f-123">Open the device configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. <span data-ttu-id="c613f-125">Dans le fichier `config-edison.json`, effectuez les remplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="c613f-125">Make the following replacements in the `config-edison.json` file:</span></span>

   * <span data-ttu-id="c613f-126">Remplacez **[nom d’hôte ou adresse IP de l’appareil]** par l’adresse IP d’appareil obtenue lorsque vous avez configuré votre appareil.</span><span class="sxs-lookup"><span data-stu-id="c613f-126">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="c613f-127">Remplacez **[chaîne de connexion de l’appareil IoT]** par la `device connection string` obtenue.</span><span class="sxs-lookup"><span data-stu-id="c613f-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="c613f-128">Remplacez **[chaîne de connexion d’IoT Hub]** par la `iot hub connection string` obtenue.</span><span class="sxs-lookup"><span data-stu-id="c613f-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c613f-129">Vous n’avez pas besoin de `azure_storage_connection_string` dans cet article.</span><span class="sxs-lookup"><span data-stu-id="c613f-129">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="c613f-130">Gardez-le tel quel.</span><span class="sxs-lookup"><span data-stu-id="c613f-130">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="c613f-131">Déploiement et exécution de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="c613f-131">Deploy and run the sample application</span></span>
<span data-ttu-id="c613f-132">Déployez et exécutez l’exemple d’application sur Edison en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c613f-132">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="c613f-133">Vérification du bon fonctionnement de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="c613f-133">Verify that the sample application works</span></span>
<span data-ttu-id="c613f-134">Vous devez voir la LED connectée à Edison clignoter toutes les deux secondes.</span><span class="sxs-lookup"><span data-stu-id="c613f-134">You should see the LED that is connected to Edison blinking every two seconds.</span></span> <span data-ttu-id="c613f-135">Chaque fois que la LED clignote, l’exemple d’application envoie un message à votre IoT Hub et vérifie que le message a été correctement envoyé.</span><span class="sxs-lookup"><span data-stu-id="c613f-135">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="c613f-136">De plus, chaque message reçu par l’IoT Hub apparaît dans la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="c613f-136">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="c613f-137">L’exemple d’application se termine automatiquement après l’envoi de 20 messages.</span><span class="sxs-lookup"><span data-stu-id="c613f-137">The sample application terminates automatically after sending 20 messages.</span></span>

![Exemple d’application avec des messages envoyés et reçus][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="c613f-139">Résumé</span><span class="sxs-lookup"><span data-stu-id="c613f-139">Summary</span></span>
<span data-ttu-id="c613f-140">Vous avez déployé et exécuté le nouvel exemple d’application de clignotement sur Edison pour l’envoi de messages appareil-à-cloud à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c613f-140">You've deployed and run the new blink sample application on Edison to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="c613f-141">Vous surveillez désormais les messages à mesure qu’ils sont écrits dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c613f-141">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c613f-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c613f-142">Next steps</span></span>
<span data-ttu-id="c613f-143">[Lecture des messages conservés dans le stockage Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="c613f-143">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md