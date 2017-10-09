---
featureFlags: usabilla
title: "Se connecter framboises Pi (nœud) tooAzure IoT - leçon 3 : stockage de Table | Documents Microsoft"
description: "Surveiller les messages appareil-à-cloud hello qu’ils sont écrits de stockage de Table Azure tooyour."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "récupérer des données du cloud, service cloud iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 9965bd54-61da-479b-aaad-5604850a2be5
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3c2c8086d3561b7603e18ed00492fcaa0593b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="e5a19-104">Lecture des messages conservés dans le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="e5a19-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="e5a19-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="e5a19-105">What you will do</span></span>
<span data-ttu-id="e5a19-106">Moniteur hello appareil-à-cloud les messages sont envoyés à partir de framboises Pi 3 tooyour IoT hub en tant que messages hello sont écrits stockage de Table Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="e5a19-106">Monitor hello device-to-cloud messages that are sent from Raspberry Pi 3 tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span> <span data-ttu-id="e5a19-107">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e5a19-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e5a19-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="e5a19-108">What you will learn</span></span>
<span data-ttu-id="e5a19-109">Dans cet article, vous allez apprendre le mode de conservation des messages de tooread toouse hello gulp tâche de lecture du message dans votre stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a19-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e5a19-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="e5a19-110">What you need</span></span>
<span data-ttu-id="e5a19-111">Avant de commencer ce processus, vous devez avoir terminé avec succès [exécuter hello blink Azure exemple d’application sur framboises Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="e5a19-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="e5a19-112">Lecture des nouveaux messages à partir de votre compte de stockage</span><span class="sxs-lookup"><span data-stu-id="e5a19-112">Read new messages from your storage account</span></span>
<span data-ttu-id="e5a19-113">Dans l’article précédent de hello, vous avez exécuté un exemple d’application sur Pi.</span><span class="sxs-lookup"><span data-stu-id="e5a19-113">In hello previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="e5a19-114">exemple d’application Hello envoyé concentrateur de messages tooyour Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="e5a19-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="e5a19-115">messages d’appel envoyés tooyour IoT hub sont stockés dans votre stockage de Table Azure via l’application de fonction Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e5a19-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="e5a19-116">Vous devez les messages tooread chaîne hello stockage Azure connexion à partir de votre stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a19-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="e5a19-117">les messages tooread stockés dans votre stockage de Table Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e5a19-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="e5a19-118">Obtenir la chaîne de connexion hello en exécutant hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="e5a19-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="e5a19-119">Hello première commande extrait hello `storage name` qui est utilisée dans la chaîne de connexion hello deuxième commande tooget hello.</span><span class="sxs-lookup"><span data-stu-id="e5a19-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="e5a19-120">Utilisez `iot-sample` en tant que valeur hello `{resource group name}` si vous n’avez modifié la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="e5a19-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="e5a19-121">Fichier de configuration Open hello `config-raspberrypi.json` dans le Code de Visual Studio en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e5a19-121">Open hello configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="e5a19-122">Remplacez `[Azure storage connection string]` avec la chaîne de connexion hello que vous avez obtenu à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="e5a19-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="e5a19-123">Enregistrer hello `config-raspberrypi.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="e5a19-123">Save hello `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="e5a19-124">Envoyer des messages à nouveau et les lire à partir de votre stockage de Table Azure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e5a19-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="e5a19-125">Bonjour logique pour la lecture à partir du stockage de Table Azure est Bonjour `azure-table.js` fichier.</span><span class="sxs-lookup"><span data-stu-id="e5a19-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>
   
    ![exécutez gulp --lire-stockage](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message.png)

## <a name="summary"></a><span data-ttu-id="e5a19-127">Résumé</span><span class="sxs-lookup"><span data-stu-id="e5a19-127">Summary</span></span>
<span data-ttu-id="e5a19-128">Vous avez correctement connecté hub IoT Pi tooyour cloud de hello et utilisé hello blink exemples application toosend appareil-à-cloud de messages.</span><span class="sxs-lookup"><span data-stu-id="e5a19-128">You've successfully connected Pi tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="e5a19-129">Vous avez également utilisé hello fonction Azure application toostore entrant IoT hub messages tooyour stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a19-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="e5a19-130">Vous pouvez maintenant envoyer des messages cloud-à-appareil de votre tooPi de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e5a19-130">You can now send cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5a19-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e5a19-131">Next steps</span></span>
[<span data-ttu-id="e5a19-132">Exécutez hello exemples application tooreceive cloud-à-appareil de messages</span><span class="sxs-lookup"><span data-stu-id="e5a19-132">Run hello sample application tooreceive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)

