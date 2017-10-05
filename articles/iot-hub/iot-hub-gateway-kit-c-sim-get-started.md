---
title: "Appareil simulé et passerelle Azure IoT - Prise en main | Microsoft Docs"
description: "Prise en main du Kit de démarrage de passerelle IoT, créer votre Azure IoT Hub et connecter la passerelle à l'IoT Hub"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot hub, passerelle iot, bien démarrer avec l’internet des objets, kit d’outils iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 916fa40d9ac857dfa72197b40c232834593d3891
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="58a38-104">Prise en main du Kit de démarrage de la passerelle IoT avec un appareil simulé</span><span class="sxs-lookup"><span data-stu-id="58a38-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="58a38-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="58a38-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="58a38-106">Appareil simulé</span><span class="sxs-lookup"><span data-stu-id="58a38-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="58a38-107">Dans ce didacticiel, vous commencez par découvrir les principes fondamentaux du [Kit de démarrage de la passerelle IoT](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="58a38-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="58a38-108">Vous allez travailler avec Intel NUC exécutant Wind River Linux.</span><span class="sxs-lookup"><span data-stu-id="58a38-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="58a38-109">Vous apprendrez ensuite à connecter en toute transparence vos appareils au cloud à l’aide d’Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="58a38-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="58a38-110">**Vous n’avez pas encore de kit ?** Cliquez [ici](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="58a38-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="58a38-111">Leçon 1 : Configuration de votre NUC</span><span class="sxs-lookup"><span data-stu-id="58a38-111">Lesson 1: Configure your NUC</span></span>
![Diagramme de bout en bout pour la leçon 1](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="58a38-113">Dans cette leçon, vous allez configurer des NUC Intel (Next Unit of Computing) dans le Kit en tant que passerelle Azure IoT, installer le package Azure IoT Edge sur les NUC et exécuter un exemple d’application pour vérifier la fonctionnalité de passerelle.</span><span class="sxs-lookup"><span data-stu-id="58a38-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="58a38-114">*Durée estimée : 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="58a38-114">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="58a38-115">Consultez [Configurer Intel NUC comme passerelle IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="58a38-115">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="58a38-116">Leçon 2 : Création de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="58a38-116">Lesson 2: Create your IoT Hub</span></span>
![Diagramme de bout en bout pour la leçon 2](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="58a38-118">Dans cette leçon, vous installez les outils et logiciels sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="58a38-118">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="58a38-119">Vous créez ensuite votre compte Azure gratuit, vous approvisionnez votre Azure IoT Hub et vous créez votre premier appareil dans l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="58a38-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="58a38-120">Avant de commencer cette leçon, terminez la Leçon 1.</span><span class="sxs-lookup"><span data-stu-id="58a38-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="58a38-121">Obtenir les outils</span><span class="sxs-lookup"><span data-stu-id="58a38-121">Get the tools</span></span>
<span data-ttu-id="58a38-122">Installez les outils et logiciels sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="58a38-122">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="58a38-123">*Durée estimée : 20 minutes*</span><span class="sxs-lookup"><span data-stu-id="58a38-123">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="58a38-124">Accédez à [Obtenir les outils](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md).</span><span class="sxs-lookup"><span data-stu-id="58a38-124">Go to [Get the tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="58a38-125">Créer un IoT hub et enregistrer votre appareil</span><span class="sxs-lookup"><span data-stu-id="58a38-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="58a38-126">Créez votre groupe de ressources, approvisionnez votre premier Azure IoT Hub et ajoutez votre premier appareil à l’IoT Hub à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="58a38-126">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="58a38-127">*Durée estimée : 10 minutes*</span><span class="sxs-lookup"><span data-stu-id="58a38-127">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="58a38-128">Accédez à [Créer un IoT Hub et enregistrer votre appareil](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="58a38-128">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-the-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="58a38-129">Leçon 3 : Recevoir des messages à partir de l’appareil simulé et lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="58a38-129">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="58a38-130">Dans cette leçon, vous utiliserez des scripts pour automatiser la configuration et l’exécution d’une application d'appareil simulé dans votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="58a38-130">In this lesson, you will use scripts to automate the configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="58a38-131">L’application d'appareil simulé génère des exemples de données de température et les envoie à un module IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="58a38-131">The simulated device app generates sample temperature data and sends it to an IoT hub module.</span></span> <span data-ttu-id="58a38-132">Le module IoT Hub regroupe les données reçues et les envoie à votre IoT Hub via l’infrastructure de passerelle fournie dans Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="58a38-132">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![Diagramme de bout en bout pour la leçon 3](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="58a38-134">Configurer et exécuter un appareil simulé</span><span class="sxs-lookup"><span data-stu-id="58a38-134">Configure and run a simulated device</span></span>
<span data-ttu-id="58a38-135">Préparez les exemples de codes.</span><span class="sxs-lookup"><span data-stu-id="58a38-135">Prepare the sample codes.</span></span> <span data-ttu-id="58a38-136">Puis configurez et exécutez l'exemple d’application d’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="58a38-136">Then configure and run the simulated device sample application.</span></span>

<span data-ttu-id="58a38-137">*Durée estimée : 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="58a38-137">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="58a38-138">Accédez à [Configurer et exécuter un appareil simulé](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="58a38-138">Go to [Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="58a38-139">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="58a38-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="58a38-140">Exécutez un exemple de code sur votre ordinateur hôte pour lire les messages à partir de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="58a38-140">Run a sample code on your host computer to read the messages from your IoT hub.</span></span>

<span data-ttu-id="58a38-141">*Durée estimée : 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="58a38-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="58a38-142">Accédez à [Lire des messages à partir de votre IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="58a38-142">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="58a38-143">Leçon 4 : Enregistrer des messages sur le stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="58a38-143">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="58a38-144">Créez une application de fonction Azure qui récupère les messages entrants à partir de votre IoT Hub et les écrit dans le stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="58a38-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Diagramme de bout en bout pour la leçon 4](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="58a38-146">Création d’une application de fonction Azure et d’un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="58a38-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="58a38-147">Utilisez un modèle Azure Resource Manager pour créer une application de fonction Azure et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="58a38-147">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="58a38-148">*Durée estimée : 10 minutes*</span><span class="sxs-lookup"><span data-stu-id="58a38-148">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="58a38-149">Accédez à [Création d’une application de fonction Azure et d’un compte de stockage Azure](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="58a38-149">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="58a38-150">Lire des messages conservés dans le stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="58a38-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="58a38-151">Surveillez les messages passerelle-à-cloud lorsqu’ils sont écrits dans le stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="58a38-151">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="58a38-152">*Durée estimée : 5 minutes*</span><span class="sxs-lookup"><span data-stu-id="58a38-152">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="58a38-153">Accédez à [Lire des messages conservés dans le stockage Table Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="58a38-153">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="58a38-154">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="58a38-154">Troubleshooting</span></span>
<span data-ttu-id="58a38-155">Si vous rencontrez des problèmes au cours des leçons, recherchez des solutions dans l’article [Résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="58a38-155">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="58a38-156">Aller plus loin</span><span class="sxs-lookup"><span data-stu-id="58a38-156">Explore more</span></span>
<span data-ttu-id="58a38-157">Consultez la [zone pour développeurs Intel IoT Gateway Kit](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="58a38-157">Visit the [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) to learn more.</span></span>