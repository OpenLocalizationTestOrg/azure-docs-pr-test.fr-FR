---
title: Appareil SensorTag et passerelle Azure IoT - Prise en main | Microsoft Docs
description: "Prise en main du Kit de démarrage de passerelle IoT, créer votre Azure IoT hub et connecter SensorTag et la passerelle vers l’IoT hub"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot hub, passerelle iot, bien démarrer avec l’internet des objets, kit d’outils iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 624bdc7877d5048da08897f868272fd8e8f3f7b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="199be-104">Prise en main du Kit de démarrage de la passerelle IoT avec un SensorTag</span><span class="sxs-lookup"><span data-stu-id="199be-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="199be-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="199be-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="199be-106">Appareil simulé</span><span class="sxs-lookup"><span data-stu-id="199be-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="199be-107">Dans ce didacticiel, vous commencez par découvrir les principes fondamentaux du [Kit de démarrage de la passerelle IoT](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="199be-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="199be-108">Vous allez travailler avec Intel NUC exécutant Wind River Linux et [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="199be-108">You will be working with Intel NUC that's running Wind River Linux and the [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="199be-109">Vous apprendrez ensuite à connecter en toute transparence vos appareils au cloud à l’aide d’Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="199be-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="199be-110">**Vous n’avez pas encore de kit ?** Cliquez [ici](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="199be-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="199be-111">**Vous n’avez pas de SensorTag ?** [Commencez avec un appareil simulé](iot-hub-gateway-kit-c-sim-get-started.md) ou [achetez un SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="199be-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="199be-112">Leçon 1 : Configuration de votre NUC</span><span class="sxs-lookup"><span data-stu-id="199be-112">Lesson 1: Configure your NUC</span></span>
![Diagramme de bout en bout pour la leçon 1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="199be-114">Dans cette leçon, vous allez configurer des NUC Intel (Next Unit of Computing) dans le Kit en tant que passerelle Azure IoT, installer le package Azure IoT Edge sur les NUC et exécuter un exemple d’application pour vérifier la fonctionnalité de passerelle.</span><span class="sxs-lookup"><span data-stu-id="199be-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="199be-115">*Durée estimée : 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="199be-115">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="199be-116">Consultez [Configurer Intel NUC comme passerelle IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="199be-116">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="199be-117">Leçon 2 : Création de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="199be-117">Lesson 2: Create your IoT Hub</span></span>
![Diagramme de bout en bout pour la leçon 2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="199be-119">Dans cette leçon, vous installez les outils et logiciels sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="199be-119">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="199be-120">Vous créez ensuite votre compte Azure gratuit, vous approvisionnez votre Azure IoT Hub et vous créez votre premier appareil dans l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="199be-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="199be-121">Avant de commencer cette leçon, terminez la Leçon 1.</span><span class="sxs-lookup"><span data-stu-id="199be-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="199be-122">Obtenir les outils</span><span class="sxs-lookup"><span data-stu-id="199be-122">Get the tools</span></span>
<span data-ttu-id="199be-123">Installez les outils et logiciels sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="199be-123">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="199be-124">*Durée estimée : 20 minutes*</span><span class="sxs-lookup"><span data-stu-id="199be-124">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="199be-125">Accédez à [Obtenir les outils](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md).</span><span class="sxs-lookup"><span data-stu-id="199be-125">Go to [Get the tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="199be-126">Créer un IoT hub et enregistrer votre appareil</span><span class="sxs-lookup"><span data-stu-id="199be-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="199be-127">Créez votre groupe de ressources, approvisionnez votre premier Azure IoT Hub et ajoutez votre premier appareil à l’IoT Hub à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="199be-127">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="199be-128">*Durée estimée : 10 minutes*</span><span class="sxs-lookup"><span data-stu-id="199be-128">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="199be-129">Accédez à [Créer un IoT hub et enregistrer votre appareil](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="199be-129">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="199be-130">Leçon 3 : Recevoir des messages à partir de SensorTag et lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="199be-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="199be-131">Dans cette leçon, vous utiliserez des scripts pour automatiser la configuration et l’exécution d’un exemple d’application BLE dans votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="199be-131">In this lesson, you will use scripts to automate the configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="199be-132">De telles applications utilisent une collection de modules pour agréger et transformer des données, traiter des commandes ou effectuer des tâches associées.</span><span class="sxs-lookup"><span data-stu-id="199be-132">Such applications use a collection of modules to aggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="199be-133">Les modules communiquent entre eux par le bais d’un courtier de messages.</span><span class="sxs-lookup"><span data-stu-id="199be-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="199be-134">L’exemple d’application comprend un module BLE et un module IoT hub.</span><span class="sxs-lookup"><span data-stu-id="199be-134">The sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="199be-135">Le module BLE reçoit des données du SensorTag BLE.</span><span class="sxs-lookup"><span data-stu-id="199be-135">The BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="199be-136">Le module IoT Hub regroupe les données reçues et les envoie à votre IoT Hub via l’infrastructure de passerelle fournie dans Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="199be-136">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![Diagramme de bout en bout pour la leçon 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-the-ble-sample-app"></a><span data-ttu-id="199be-138">Configurer et exécuter l’exemple d’application BLE</span><span class="sxs-lookup"><span data-stu-id="199be-138">Configure and run the BLE sample app</span></span>
<span data-ttu-id="199be-139">Configurez la connectivité entre SensorTag et votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="199be-139">Set up the connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="199be-140">Terminez la configuration, puis exécutez l’application d’exemple BLE.</span><span class="sxs-lookup"><span data-stu-id="199be-140">Then finish the configuration and run the BLE sample application.</span></span>

<span data-ttu-id="199be-141">*Durée estimée : 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="199be-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="199be-142">Accédez à [Configurer et exécuter l’exemple d’application BLE](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="199be-142">Go to [Configure and run the BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="199be-143">Lire des messages à partir de votre IoT hub</span><span class="sxs-lookup"><span data-stu-id="199be-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="199be-144">Exécutez l’exemple de code sur votre ordinateur hôte pour lire les messages provenant de votre IoT hub.</span><span class="sxs-lookup"><span data-stu-id="199be-144">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="199be-145">*Durée estimée : 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="199be-145">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="199be-146">Accédez à [Lire des messages à partir de votre IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="199be-146">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="199be-147">Leçon 4 : Enregistrer des messages sur le stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="199be-147">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="199be-148">Créez une application de fonction Azure qui récupère les messages entrants à partir de votre IoT Hub et les écrit dans le stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="199be-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Diagramme de bout en bout pour la leçon 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="199be-150">Création d’une application de fonction Azure et d’un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="199be-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="199be-151">Utilisez un modèle Azure Resource Manager pour créer une application de fonction Azure et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="199be-151">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="199be-152">*Durée estimée : 10 minutes*</span><span class="sxs-lookup"><span data-stu-id="199be-152">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="199be-153">Accédez à [Création d’une application de fonction Azure et d’un compte de stockage Azure](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="199be-153">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="199be-154">Lire des messages conservés dans le stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="199be-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="199be-155">Surveillez les messages passerelle-à-cloud lorsqu’ils sont écrits dans le stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="199be-155">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="199be-156">*Durée estimée : 5 minutes*</span><span class="sxs-lookup"><span data-stu-id="199be-156">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="199be-157">Accédez à [Lire des messages conservés dans le stockage Table Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="199be-157">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="199be-158">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="199be-158">Troubleshooting</span></span>
<span data-ttu-id="199be-159">Si vous rencontrez des problèmes au cours des leçons, recherchez des solutions dans l’article [Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="199be-159">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="199be-160">Aller plus loin</span><span class="sxs-lookup"><span data-stu-id="199be-160">Explore more</span></span>
<span data-ttu-id="199be-161">Consultez la [zone pour développeurs Intel IoT Gateway Kit](http://software.intel.com/iot/microsoft-azure) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="199be-161">Visit the [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) to learn more.</span></span>