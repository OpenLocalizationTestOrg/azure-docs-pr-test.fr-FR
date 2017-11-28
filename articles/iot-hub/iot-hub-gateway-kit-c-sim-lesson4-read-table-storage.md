---
title: "Appareil simulé et passerelle Azure IoT - Leçon 4 : Stockage de table | Microsoft Docs"
description: "Enregistrer des messages à partir de hub IoT de tooyour Intel NUC, notez-les tooAzure le stockage de Table et puis de les lire à partir du cloud de hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "récupérer des données du cloud, service cloud iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 78e4b6ea-968d-401e-a7dc-8f9acdb3ec1a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 43e299d63bbbe10d4d867af25e700c3a7cc07c53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="e0567-104">Lire des messages conservés dans le stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="e0567-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e0567-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="e0567-105">What you will do</span></span>

- <span data-ttu-id="e0567-106">Exécutez hello passerelle exemple d’application sur votre passerelle qui envoie l’IoT hub tooyour de messages.</span><span class="sxs-lookup"><span data-stu-id="e0567-106">Run hello gateway sample application on your gateway that sends messages tooyour IoT hub.</span></span>
- <span data-ttu-id="e0567-107">Exécutez l’exemple de code sur votre hôte ordinateur tooread les messages dans votre stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="e0567-107">Run sample code on your host computer tooread messages in your Azure Table storage.</span></span>

<span data-ttu-id="e0567-108">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e0567-108">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e0567-109">Contenu</span><span class="sxs-lookup"><span data-stu-id="e0567-109">What you will learn</span></span>

<span data-ttu-id="e0567-110">Comment toouse hello gulp outil toorun hello exemples code tooread de messages dans votre stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="e0567-110">How toouse hello gulp tool toorun hello sample code tooread messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e0567-111">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="e0567-111">What you need</span></span>

<span data-ttu-id="e0567-112">Vous avez correctement hello tâche suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0567-112">You have have successfully done hello following tasks:</span></span>

- <span data-ttu-id="e0567-113">[Créé une application de fonction Azure hello et compte de stockage Azure hello](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="e0567-113">[Created hello Azure function app and hello Azure storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="e0567-114">[Exécuter l’application d’exemple hello passerelle](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="e0567-114">[Run hello gateway sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>
- <span data-ttu-id="e0567-115">[lire des messages à partir de votre IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="e0567-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="e0567-116">Obtenir vos chaînes de connexion de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="e0567-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="e0567-117">Au début de cette leçon, vous avez créé un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e0567-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="e0567-118">chaîne de connexion tooget hello hello Azure du compte de stockage, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="e0567-118">tooget hello connection string of hello Azure storage account, run hello following commands:</span></span>

* <span data-ttu-id="e0567-119">Répertoriez tous vos comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="e0567-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="e0567-120">Obtenez la chaîne de connexion de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e0567-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="e0567-121">Utilisez `iot-gateway` en tant que valeur hello `{resource group name}` si vous n’avez pas modifier la valeur hello dans la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="e0567-121">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="e0567-122">Configurer la connexion du périphérique hello</span><span class="sxs-lookup"><span data-stu-id="e0567-122">Configure hello device connection</span></span>

<span data-ttu-id="e0567-123">Hello de mise à jour `config-azure.json` fichiers afin que les exemples de code hello qui s’exécute sur l’ordinateur hôte hello peut lire le message dans votre stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="e0567-123">Update hello `config-azure.json` file so that hello sample code that runs on hello host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="e0567-124">tooconfigure hello connexion du périphérique, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e0567-124">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="e0567-125">Fichier de configuration de périphérique ouvert hello `config-azure.json` par hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="e0567-125">Open hello device configuration file `config-azure.json` by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configuration](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="e0567-127">Remplacez `[Azure storage connection string]` par hello chaîne de connexion de stockage Azure que vous avez obtenu.</span><span class="sxs-lookup"><span data-stu-id="e0567-127">Replace `[Azure storage connection string]` with hello Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="e0567-128">`[IoT hub connection string]` doit déjà être remplacé dans la section [Lire des messages à partir d’Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) de la leçon 3.</span><span class="sxs-lookup"><span data-stu-id="e0567-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="e0567-129">Lire des messages dans votre stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="e0567-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="e0567-130">Exécuter l’application d’exemple hello passerelle et lire les messages de stockage Azure Table par hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e0567-130">Run hello gateway sample application and read Azure Table storage messages by hello following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="e0567-131">Votre hub IoT déclenche votre message toosave d’application Azure fonction dans votre stockage de Table Azure quand le nouveau message arrive.</span><span class="sxs-lookup"><span data-stu-id="e0567-131">Your IoT hub triggers your Azure Function application toosave message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="e0567-132">Hello `gulp run` commande exécute l’exemple d’application passerelle envoie IoT hub tooyour de messages.</span><span class="sxs-lookup"><span data-stu-id="e0567-132">hello `gulp run` command runs gateway sample application that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="e0567-133">Avec `table-storage` paramètre, il génère également un Bonjour tooreceive de processus enfant enregistré des messages dans votre stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="e0567-133">With `table-storage` parameter, it also spawns a child process tooreceive hello saved message in your Azure Table storage.</span></span>

<span data-ttu-id="e0567-134">messages de type Hello qui sont envoyés et reçus sont tous les hello afficher instantanément à même de fenêtre dans la console hello machine hôte.</span><span class="sxs-lookup"><span data-stu-id="e0567-134">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="e0567-135">instance de l’application exemple Hello se termine automatiquement au bout de 40 secondes.</span><span class="sxs-lookup"><span data-stu-id="e0567-135">hello sample application instance will terminate automatically in 40 seconds.</span></span>

   ![lecture de gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a><span data-ttu-id="e0567-137">Résumé</span><span class="sxs-lookup"><span data-stu-id="e0567-137">Summary</span></span>

<span data-ttu-id="e0567-138">Vous avez exécuté des messages hello tooread de code d’exemple hello dans votre stockage de Table Azure enregistré par votre application Azure (fonction).</span><span class="sxs-lookup"><span data-stu-id="e0567-138">You've run hello sample code tooread hello messages in your Azure Table storage saved by your Azure Function application.</span></span>
