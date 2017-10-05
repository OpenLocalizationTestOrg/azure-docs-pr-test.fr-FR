---
title: "Connecter Raspberry Pi (C) à Azure IoT - Leçon 3 : Stockage de tables | Microsoft Docs"
description: "Surveillez les messages appareil-à-cloud alors qu’ils sont écrits dans votre stockage Table Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "récupérer des données du cloud, service cloud iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8c5558bb-3c31-4445-90e6-b1a978738545
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 16b7f2e38bfe3b40d199cb6e07976433aa54ea32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="5e747-104">Lecture des messages conservés dans le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="5e747-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5e747-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="5e747-105">What you will do</span></span>
<span data-ttu-id="5e747-106">Surveillez les messages appareil-à-cloud qui sont envoyés à partir de Raspberry Pi 3 à votre IoT Hub, à mesure que les messages sont écrits dans votre stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="5e747-106">Monitor the device-to-cloud messages that are sent from Raspberry Pi 3 to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="5e747-107">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5e747-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5e747-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="5e747-108">What you will learn</span></span>
<span data-ttu-id="5e747-109">Dans cet article, vous allez apprendre à utiliser la tâche de lecture de message gulp pour lire les messages conservés dans votre stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="5e747-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5e747-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="5e747-110">What you need</span></span>
<span data-ttu-id="5e747-111">Avant de commencer, vous devez avoir correctement suivi la section [Exécution de l’exemple d’application de clignotement Azure sur Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="5e747-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="5e747-112">Lecture des nouveaux messages à partir de votre compte de stockage</span><span class="sxs-lookup"><span data-stu-id="5e747-112">Read new messages from your storage account</span></span>
<span data-ttu-id="5e747-113">Dans l’article précédent, vous avez exécuté un exemple d’application sur Pi.</span><span class="sxs-lookup"><span data-stu-id="5e747-113">In the previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="5e747-114">L’exemple d’application a envoyé des messages à votre Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5e747-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="5e747-115">Les messages envoyés à votre IoT Hub sont stockés dans votre stockage Table Azure via l’application de fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="5e747-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="5e747-116">Pour lire les messages à partir de votre stockage Table Azure, vous avez besoin de la chaîne de connexion du Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="5e747-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="5e747-117">Pour lire les messages stockés dans votre stockage Table Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5e747-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="5e747-118">Obtenez la chaîne de connexion en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5e747-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="5e747-119">La première commande récupère le `storage name` utilisé dans la deuxième commande pour obtenir la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="5e747-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="5e747-120">Si vous n’avez pas modifié la valeur, utilisez `iot-sample` en tant que valeur de `{resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="5e747-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="5e747-121">Ouvrez le fichier de configuration `config-raspberrypi.json` dans Visual Studio Code en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5e747-121">Open the configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="5e747-122">Remplacez `[Azure storage connection string]` par la chaîne de connexion que vous avez obtenue à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="5e747-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="5e747-123">Enregistrez le fichier `config-raspberrypi.json`.</span><span class="sxs-lookup"><span data-stu-id="5e747-123">Save the `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="5e747-124">Envoyez de nouveau des messages et lisez-les à partir de votre stockage Table Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5e747-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="5e747-125">La logique pour la lecture à partir du stockage Table Azure se trouve dans le fichier `azure-table.js`.</span><span class="sxs-lookup"><span data-stu-id="5e747-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>
   
   ![exécutez gulp --lire-stockage](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message_c.png)

## <a name="summary"></a><span data-ttu-id="5e747-127">Résumé</span><span class="sxs-lookup"><span data-stu-id="5e747-127">Summary</span></span>
<span data-ttu-id="5e747-128">Vous avez correctement connecté Pi à votre IoT Hub dans le cloud et utilisé l’exemple d’application de clignotement pour envoyer des messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="5e747-128">You've successfully connected Pi to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="5e747-129">Vous avez également utilisé l’application de fonction Azure pour stocker des messages d’IoT Hub entrants votre stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="5e747-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="5e747-130">Vous pouvez désormais envoyer des messages cloud-à-appareil depuis votre IoT Hub vers Pi.</span><span class="sxs-lookup"><span data-stu-id="5e747-130">You can now send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e747-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5e747-131">Next steps</span></span>
[<span data-ttu-id="5e747-132">Exécution d’un exemple d’application pour recevoir des messages cloud-à-appareil</span><span class="sxs-lookup"><span data-stu-id="5e747-132">Run a sample application to receive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)

