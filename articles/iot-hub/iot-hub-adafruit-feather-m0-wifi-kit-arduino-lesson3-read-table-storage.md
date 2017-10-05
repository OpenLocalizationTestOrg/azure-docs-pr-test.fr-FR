---
title: "Connecter Arduino (C) à Azure IoT - Leçon 3 : Stockage de tables | Microsoft Docs"
description: "Surveillez les messages appareil-à-cloud alors qu’ils sont écrits dans votre stockage Table Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "données dans le cloud, collecte de données cloud, service cloud iot, données iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 29fb97f5cf0669acb9e68d8a829294ee64c9cf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="f9bbe-104">Lecture des messages conservés dans le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="f9bbe-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="f9bbe-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="f9bbe-105">What you will do</span></span>
<span data-ttu-id="f9bbe-106">Surveillez les messages appareil-cloud qui sont envoyés à partir de votre carte Adafruit Feather M0 WiFi Arduino à votre IoT Hub, à mesure que les messages sont écrits dans le Stockage de table Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bbe-106">Monitor the device-to-cloud messages that are sent from your Adafruit Feather M0 WiFi Arduino board to your IoT hub as the messages are written to your Azure Table storage.</span></span>

<span data-ttu-id="f9bbe-107">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="f9bbe-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f9bbe-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="f9bbe-108">What you will learn</span></span>
<span data-ttu-id="f9bbe-109">Dans cet article, vous allez apprendre à utiliser la tâche de lecture de message gulp pour lire les messages conservés dans votre stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bbe-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f9bbe-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="f9bbe-110">What you need</span></span>
<span data-ttu-id="f9bbe-111">Avant de commencer, vous devez avoir correctement suivi la section [Exécution de l’exemple d’application de clignotement Azure sur votre carte Arduino][run-blink-application].</span><span class="sxs-lookup"><span data-stu-id="f9bbe-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on your Arduino board][run-blink-application].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="f9bbe-112">Lecture des nouveaux messages à partir de votre compte de stockage</span><span class="sxs-lookup"><span data-stu-id="f9bbe-112">Read new messages from your storage account</span></span>
<span data-ttu-id="f9bbe-113">Dans l’article précédent, vous avez exécuté un exemple d’application sur votre carte Arduino.</span><span class="sxs-lookup"><span data-stu-id="f9bbe-113">In the previous article, you ran a sample application on your Arduino board.</span></span> <span data-ttu-id="f9bbe-114">L’exemple d’application a envoyé des messages à votre Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f9bbe-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="f9bbe-115">Les messages envoyés à votre IoT Hub sont stockés dans votre stockage Table Azure via l’application de fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bbe-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="f9bbe-116">Pour lire les messages à partir de votre stockage Table Azure, vous avez besoin de la chaîne de connexion du Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bbe-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="f9bbe-117">Pour lire les messages stockés dans votre stockage Table Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f9bbe-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="f9bbe-118">Obtenez la chaîne de connexion en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f9bbe-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="f9bbe-119">La première commande récupère le `storage name` utilisé dans la deuxième commande pour obtenir la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="f9bbe-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="f9bbe-120">Si vous n’avez pas modifié la valeur, utilisez `iot-sample` en tant que valeur de `{resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="f9bbe-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="f9bbe-121">Ouvrez le fichier de configuration `config-arduino.json` dans Visual Studio Code en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f9bbe-121">Open the configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. <span data-ttu-id="f9bbe-122">Remplacez `[Azure storage connection string]` par la chaîne de connexion que vous avez obtenue à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="f9bbe-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="f9bbe-123">Enregistrez le fichier `config-arduino.json`.</span><span class="sxs-lookup"><span data-stu-id="f9bbe-123">Save the `config-arduino.json` file.</span></span>
5. <span data-ttu-id="f9bbe-124">Envoyez de nouveau des messages et lisez-les à partir de votre stockage Table Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f9bbe-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>

   ```bash
   gulp run --read-storage

   # You can monitor the serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   <span data-ttu-id="f9bbe-125">La logique pour la lecture à partir du stockage Table Azure se trouve dans le fichier `azure-table.js`.</span><span class="sxs-lookup"><span data-stu-id="f9bbe-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>

   ![exécutez gulp --lire-stockage][gulp-run]

## <a name="summary"></a><span data-ttu-id="f9bbe-127">Résumé</span><span class="sxs-lookup"><span data-stu-id="f9bbe-127">Summary</span></span>
<span data-ttu-id="f9bbe-128">Vous avez correctement connecté votre carte Arduino à votre IoT Hub dans le cloud, et utilisé l’exemple d’application de clignotement pour envoyer des messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="f9bbe-128">You've successfully connected your Arduino board to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="f9bbe-129">Vous avez également utilisé l’application de fonction Azure pour stocker des messages d’IoT Hub entrants votre stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bbe-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="f9bbe-130">Vous pouvez désormais envoyer des messages cloud-à-appareil depuis votre IoT Hub vers votre carte Arduino.</span><span class="sxs-lookup"><span data-stu-id="f9bbe-130">You can now send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9bbe-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9bbe-131">Next steps</span></span>
<span data-ttu-id="f9bbe-132">[Envoyer des messages Cloud vers appareil][send-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="f9bbe-132">[Send cloud-to-device messages][send-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md