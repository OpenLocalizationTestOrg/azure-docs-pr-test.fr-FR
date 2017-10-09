---
title: "Connect Intel Edison (C) tooAzure IoT - leçon 3 : surveiller les messages | Documents Microsoft"
description: "Surveiller les messages appareil-à-cloud hello qu’ils sont écrits de stockage de Table Azure tooyour."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "données dans le cloud de hello, collecte de données de cloud, le service cloud iot, iot données"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: cad545c3-dd88-486c-a663-d587a924ccd4
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2679b22f2987f77ecd1eea03044ed8ea03bf73f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="9fe58-104">Lecture des messages conservés dans le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="9fe58-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="9fe58-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="9fe58-105">What you will do</span></span>
<span data-ttu-id="9fe58-106">Moniteur hello appareil-à-cloud les messages sont envoyés à partir de hub IoT de tooyour Intel Edison en tant que messages hello sont écrits tooyour stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="9fe58-106">Monitor hello device-to-cloud messages that are sent from Intel Edison tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span> <span data-ttu-id="9fe58-107">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="9fe58-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9fe58-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="9fe58-108">What you will learn</span></span>
<span data-ttu-id="9fe58-109">Dans cet article, vous allez apprendre le mode de conservation des messages de tooread toouse hello gulp tâche de lecture du message dans votre stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="9fe58-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9fe58-110">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="9fe58-110">What you need</span></span>
<span data-ttu-id="9fe58-111">Avant de commencer ce processus, vous devez avoir terminé avec succès [exécuter hello blink Azure exemple d’application sur Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="9fe58-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="9fe58-112">Lecture des nouveaux messages à partir de votre compte de stockage</span><span class="sxs-lookup"><span data-stu-id="9fe58-112">Read new messages from your storage account</span></span>
<span data-ttu-id="9fe58-113">Dans l’article précédent de hello, vous avez exécuté un exemple d’application sur Edison.</span><span class="sxs-lookup"><span data-stu-id="9fe58-113">In hello previous article, you ran a sample application on Edison.</span></span> <span data-ttu-id="9fe58-114">exemple d’application Hello envoyé concentrateur de messages tooyour Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="9fe58-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="9fe58-115">messages d’appel envoyés tooyour IoT hub sont stockés dans votre stockage de Table Azure via l’application de fonction Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9fe58-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="9fe58-116">Vous devez les messages tooread chaîne hello stockage Azure connexion à partir de votre stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="9fe58-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="9fe58-117">les messages tooread stockés dans votre stockage de Table Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9fe58-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="9fe58-118">Obtenir la chaîne de connexion hello en exécutant hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="9fe58-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="9fe58-119">Hello première commande extrait hello `storage name` qui est utilisée dans la chaîne de connexion hello deuxième commande tooget hello.</span><span class="sxs-lookup"><span data-stu-id="9fe58-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="9fe58-120">Utilisez `iot-sample` en tant que valeur hello `{resource group name}` si vous n’avez modifié la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="9fe58-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="9fe58-121">Fichier de configuration Open hello `config-edison.json` dans le Code de Visual Studio en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9fe58-121">Open hello configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. <span data-ttu-id="9fe58-122">Remplacez `[Azure storage connection string]` avec la chaîne de connexion hello que vous avez obtenu à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="9fe58-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="9fe58-123">Enregistrer hello `config-edison.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="9fe58-123">Save hello `config-edison.json` file.</span></span>
5. <span data-ttu-id="9fe58-124">Envoyer des messages à nouveau et les lire à partir de votre stockage de Table Azure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9fe58-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>

   ```bash
   gulp run --read-storage
   ```

   <span data-ttu-id="9fe58-125">Bonjour logique pour la lecture à partir du stockage de Table Azure est Bonjour `azure-table.js` fichier.</span><span class="sxs-lookup"><span data-stu-id="9fe58-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>

   ![exécutez gulp --lire-stockage][gulp run]

## <a name="summary"></a><span data-ttu-id="9fe58-127">Résumé</span><span class="sxs-lookup"><span data-stu-id="9fe58-127">Summary</span></span>
<span data-ttu-id="9fe58-128">Vous avez correctement connecté hub IoT Edison tooyour cloud de hello et utilisé hello blink exemples application toosend appareil-à-cloud de messages.</span><span class="sxs-lookup"><span data-stu-id="9fe58-128">You've successfully connected Edison tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="9fe58-129">Vous avez également utilisé hello fonction Azure application toostore entrant IoT hub messages tooyour stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="9fe58-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="9fe58-130">Vous pouvez maintenant envoyer des messages cloud-à-appareil de votre tooEdison de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9fe58-130">You can now send cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fe58-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9fe58-131">Next steps</span></span>
<span data-ttu-id="9fe58-132">[Exécuter un tooreceive d’application exemple messages cloud-à-appareil][receive-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="9fe58-132">[Run a sample application tooreceive cloud-to-device messages][receive-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message_c.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md