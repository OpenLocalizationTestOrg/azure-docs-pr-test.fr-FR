---
title: "Appareil simulé et passerelle Azure IoT - Leçon 4 : Stockage de table | Microsoft Docs"
description: "Enregistrez des messages à partir d’Intel NUC dans votre hub IoT, écrivez-les dans le stockage Table Azure, puis lisez-les à partir du cloud."
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
ms.openlocfilehash: de5fae794c195132e2a487c0095845c756aa28e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="75537-104">Lire des messages conservés dans le stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="75537-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="75537-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="75537-105">What you will do</span></span>

- <span data-ttu-id="75537-106">Exécutez l’exemple d’application de votre passerelle qui envoie des messages à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="75537-106">Run the gateway sample application on your gateway that sends messages to your IoT hub.</span></span>
- <span data-ttu-id="75537-107">Exécutez l’exemple de code sur votre ordinateur hôte pour lire les messages dans votre stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="75537-107">Run sample code on your host computer to read messages in your Azure Table storage.</span></span>

<span data-ttu-id="75537-108">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="75537-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="75537-109">Contenu</span><span class="sxs-lookup"><span data-stu-id="75537-109">What you will learn</span></span>

<span data-ttu-id="75537-110">Utilisation de l’outil gulp pour exécuter l’exemple de code permettant de lire les messages dans votre stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="75537-110">How to use the gulp tool to run the sample code to read messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="75537-111">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="75537-111">What you need</span></span>

<span data-ttu-id="75537-112">Vous avez effectué les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="75537-112">You have have successfully done the following tasks:</span></span>

- <span data-ttu-id="75537-113">[créer l’application de fonction Azure et le compte de stockage Azure](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md) ;</span><span class="sxs-lookup"><span data-stu-id="75537-113">[Created the Azure function app and the Azure storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="75537-114">[exécuter l’exemple d’application de la passerelle](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md) ;</span><span class="sxs-lookup"><span data-stu-id="75537-114">[Run the gateway sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>
- <span data-ttu-id="75537-115">[lire des messages à partir de votre IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="75537-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="75537-116">Obtenir vos chaînes de connexion de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="75537-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="75537-117">Au début de cette leçon, vous avez créé un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="75537-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="75537-118">Pour obtenir la chaîne de connexion du compte de stockage Azure, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="75537-118">To get the connection string of the Azure storage account, run the following commands:</span></span>

* <span data-ttu-id="75537-119">Répertoriez tous vos comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="75537-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="75537-120">Obtenez la chaîne de connexion Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="75537-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="75537-121">Si vous n’avez pas modifié la valeur à la leçon 2, utilisez `iot-gateway` en tant que valeur de `{resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="75537-121">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="75537-122">Configuration de la connexion de l’appareil</span><span class="sxs-lookup"><span data-stu-id="75537-122">Configure the device connection</span></span>

<span data-ttu-id="75537-123">Mettez à jour le fichier `config-azure.json` afin que l’exemple de code qui s’exécute sur l’ordinateur hôte puisse lire le message dans votre stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="75537-123">Update the `config-azure.json` file so that the sample code that runs on the host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="75537-124">Procédez comme suit pour configurer la connexion de l’appareil :</span><span class="sxs-lookup"><span data-stu-id="75537-124">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="75537-125">Ouvrez le fichier de configuration d’appareil `config-azure.json` en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="75537-125">Open the device configuration file `config-azure.json` by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configuration](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="75537-127">Remplacez `[Azure storage connection string]` par la chaîne de connexion de stockage Azure que vous avez obtenue.</span><span class="sxs-lookup"><span data-stu-id="75537-127">Replace `[Azure storage connection string]` with the Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="75537-128">`[IoT hub connection string]` doit déjà être remplacé dans la section [Lire des messages à partir d’Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) de la leçon 3.</span><span class="sxs-lookup"><span data-stu-id="75537-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="75537-129">Lire des messages dans votre stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="75537-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="75537-130">Exécutez l’exemple d’application de la passerelle et lisez les messages de stockage Table Azure avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="75537-130">Run the gateway sample application and read Azure Table storage messages by the following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="75537-131">Votre IoT Hub déclenche votre application Azure Function pour enregistrer un nouveau message arrivant dans votre stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="75537-131">Your IoT hub triggers your Azure Function application to save message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="75537-132">La commande `gulp run` exécute l’exemple d’application de la passerelle qui envoie des messages à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="75537-132">The `gulp run` command runs gateway sample application that sends messages to your IoT hub.</span></span> <span data-ttu-id="75537-133">Avec le paramètre `table-storage`, elle génère également un processus enfant pour recevoir le message enregistré dans votre stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="75537-133">With `table-storage` parameter, it also spawns a child process to receive the saved message in your Azure Table storage.</span></span>

<span data-ttu-id="75537-134">Les messages envoyés et reçus sont tous affichés instantanément sur la même fenêtre de console sur l’ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="75537-134">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="75537-135">L’exemple d’instance d’application se ferme automatiquement au bout de 40 secondes.</span><span class="sxs-lookup"><span data-stu-id="75537-135">The sample application instance will terminate automatically in 40 seconds.</span></span>

   ![lecture de gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a><span data-ttu-id="75537-137">Résumé</span><span class="sxs-lookup"><span data-stu-id="75537-137">Summary</span></span>

<span data-ttu-id="75537-138">Vous avez exécuté l’exemple de code pour lire les messages de votre stockage Table Azure enregistrés par votre application Azure Function.</span><span class="sxs-lookup"><span data-stu-id="75537-138">You've run the sample code to read the messages in your Azure Table storage saved by your Azure Function application.</span></span>
