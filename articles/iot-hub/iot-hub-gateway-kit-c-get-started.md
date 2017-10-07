---
title: Appareil SensorTag et passerelle Azure IoT - Prise en main | Microsoft Docs
description: "Prise en main IoT passerelle Starter Kit, créez votre hub Azure IoT et connectez SensorTag et passerelle toohello IoT hub"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iot hub, passerelle iot, prise en main de hello internet des objets, iot toolkit
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
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="49fcc-104">Prise en main du Kit de démarrage de la passerelle IoT avec un SensorTag</span><span class="sxs-lookup"><span data-stu-id="49fcc-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="49fcc-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="49fcc-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="49fcc-106">Appareil simulé</span><span class="sxs-lookup"><span data-stu-id="49fcc-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="49fcc-107">Dans ce didacticiel, commencer par découvrir hello les bases de l’utilisation de [IoT passerelle Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="49fcc-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="49fcc-108">Vous allez travailler avec NUC Intel qui exécute Linux de vent district et hello [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="49fcc-108">You will be working with Intel NUC that's running Wind River Linux and hello [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="49fcc-109">Vous allez apprendre comment tooseamleesly connecter votre cloud toohello de périphériques à l’aide d’Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="49fcc-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="49fcc-110">**Vous n’avez pas encore de kit ?** Cliquez [ici](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="49fcc-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="49fcc-111">**Vous n’avez pas de SensorTag ?**[Commencez avec un appareil simulé](iot-hub-gateway-kit-c-sim-get-started.md) ou [achetez un SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="49fcc-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="49fcc-112">Leçon 1 : Configuration de votre NUC</span><span class="sxs-lookup"><span data-stu-id="49fcc-112">Lesson 1: Configure your NUC</span></span>
![Diagramme de bout en bout pour la leçon 1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="49fcc-114">Dans cette leçon, vous pouvez paramétrer des NUC Intel (suivant unité de calcul) Bonjour Kit comme passerelle Azure IoT, hello Azure IoT bord installer sur NUC et exécuter une fonctionnalité de passerelle exemple application tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="49fcc-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="49fcc-115">*Estimation du temps toocomplete : 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="49fcc-115">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="49fcc-116">Accédez trop[configurer NUC Intel comme passerelle IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="49fcc-116">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="49fcc-117">Leçon 2 : Création de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="49fcc-117">Lesson 2: Create your IoT Hub</span></span>
![Diagramme de bout en bout pour la leçon 2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="49fcc-119">Dans cette leçon, vous installez les outils de hello et des logiciels sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="49fcc-119">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="49fcc-120">Puis vous créez gratuitement un compte Azure, configurez votre concentrateur Azure IoT et créez votre premier appareil dans le hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="49fcc-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="49fcc-121">Avant de commencer cette leçon, terminez la Leçon 1.</span><span class="sxs-lookup"><span data-stu-id="49fcc-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="49fcc-122">Obtenir les outils de hello</span><span class="sxs-lookup"><span data-stu-id="49fcc-122">Get hello tools</span></span>
<span data-ttu-id="49fcc-123">Installez les outils hello et logiciels sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="49fcc-123">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="49fcc-124">*Estimation du temps toocomplete : 20 minutes*</span><span class="sxs-lookup"><span data-stu-id="49fcc-124">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="49fcc-125">Accédez trop[obtenir hello tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="49fcc-125">Go too[Get hello tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="49fcc-126">Créer un IoT hub et enregistrer votre appareil</span><span class="sxs-lookup"><span data-stu-id="49fcc-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="49fcc-127">Créer votre groupe de ressources et configurer votre concentrateur Azure IoT première ajouter votre premier appareil toohello IoT hub à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="49fcc-127">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="49fcc-128">*Estimation du temps toocomplete : 10 minutes*</span><span class="sxs-lookup"><span data-stu-id="49fcc-128">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="49fcc-129">Accédez trop[créez un IoT hub et inscrire votre appareil](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="49fcc-129">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="49fcc-130">Leçon 3 : Recevoir des messages à partir de SensorTag et lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="49fcc-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="49fcc-131">Dans cette leçon, vous allez utiliser la configuration de scripts tooautomate hello et l’exécution d’un exemple d’application BLE dans votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="49fcc-131">In this lesson, you will use scripts tooautomate hello configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="49fcc-132">Ces applications utilisent une collection de modules tooaggregate et transformer des données, traitent les commandes ou effectuer des tâches associées.</span><span class="sxs-lookup"><span data-stu-id="49fcc-132">Such applications use a collection of modules tooaggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="49fcc-133">Les modules communiquent entre eux par le bais d’un courtier de messages.</span><span class="sxs-lookup"><span data-stu-id="49fcc-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="49fcc-134">exemple d’application Hello a un module d’activer et d’un module de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="49fcc-134">hello sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="49fcc-135">module BLE Hello reçoit les données BLE SensorTag.</span><span class="sxs-lookup"><span data-stu-id="49fcc-135">hello BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="49fcc-136">Bonjour les packages de module de hub IoT les données de salutation reçu et l’envoie tooyour IoT hub via l’infrastructure de passerelle hello fournie dans Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="49fcc-136">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Diagramme de bout en bout pour la leçon 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a><span data-ttu-id="49fcc-138">Configurer et exécuter l’application d’exemple hello BLE</span><span class="sxs-lookup"><span data-stu-id="49fcc-138">Configure and run hello BLE sample app</span></span>
<span data-ttu-id="49fcc-139">Configurer une connectivité hello entre SensorTag et votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="49fcc-139">Set up hello connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="49fcc-140">Terminer la configuration de hello, puis exécutez hello BLE exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="49fcc-140">Then finish hello configuration and run hello BLE sample application.</span></span>

<span data-ttu-id="49fcc-141">*Estimation du temps toocomplete : 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="49fcc-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="49fcc-142">Accédez trop[configurer et l’exécution hello BLE exemple d’application](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="49fcc-142">Go too[Configure and run hello BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="49fcc-143">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="49fcc-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="49fcc-144">Exécutez exemple de code sur votre hôte tooread ordinateur des messages à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="49fcc-144">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="49fcc-145">*Estimation du temps toocomplete : 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="49fcc-145">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="49fcc-146">Accédez trop[lire les messages de votre hub IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="49fcc-146">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="49fcc-147">Leçon 4 : Enregistrer des messages tooAzure le stockage de Table</span><span class="sxs-lookup"><span data-stu-id="49fcc-147">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="49fcc-148">Créer une application Azure de fonction qui obtient les messages entrants à partir de votre IoT hub et les écrit tooAzure le stockage de Table.</span><span class="sxs-lookup"><span data-stu-id="49fcc-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Diagramme de bout en bout pour la leçon 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="49fcc-150">Création d’une application de fonction Azure et d’un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="49fcc-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="49fcc-151">Utilisez un toocreate de modèle Azure Resource Manager une application Azure (fonction) et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="49fcc-151">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="49fcc-152">*Estimation du temps toocomplete : 10 minutes*</span><span class="sxs-lookup"><span data-stu-id="49fcc-152">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="49fcc-153">Accédez trop[créer une application de la fonction Azure et d’un compte de stockage Azure](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="49fcc-153">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="49fcc-154">Lire des messages conservés dans le stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="49fcc-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="49fcc-155">Surveiller les messages de passerelle dans le cloud hello qu’ils sont écrits tooAzure le stockage de Table.</span><span class="sxs-lookup"><span data-stu-id="49fcc-155">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="49fcc-156">*Estimation du temps toocomplete : 5 minutes*</span><span class="sxs-lookup"><span data-stu-id="49fcc-156">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="49fcc-157">Accédez trop[lire les messages conservés dans le stockage Azure Table](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="49fcc-157">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="49fcc-158">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="49fcc-158">Troubleshooting</span></span>
<span data-ttu-id="49fcc-159">Si vous rencontrez des problèmes au cours des leçons de hello, rechercher des solutions dans hello [dépannage](iot-hub-gateway-kit-c-troubleshooting.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="49fcc-159">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="49fcc-160">Aller plus loin</span><span class="sxs-lookup"><span data-stu-id="49fcc-160">Explore more</span></span>
<span data-ttu-id="49fcc-161">Visitez hello [zone pour développeurs Intel IoT passerelle Kit](http://software.intel.com/iot/microsoft-azure) toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="49fcc-161">Visit hello [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) toolearn more.</span></span>
