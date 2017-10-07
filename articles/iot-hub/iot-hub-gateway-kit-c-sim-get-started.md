---
title: "Appareil simulé et passerelle Azure IoT - Prise en main | Microsoft Docs"
description: "Prise en main IoT passerelle Starter Kit, créez votre hub Azure IoT et connectez IoT hub toohello de passerelle"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iot hub, passerelle iot, prise en main de hello internet des objets, iot toolkit
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
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="5a2f1-104">Prise en main du Kit de démarrage de la passerelle IoT avec un appareil simulé</span><span class="sxs-lookup"><span data-stu-id="5a2f1-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a2f1-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="5a2f1-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="5a2f1-106">Appareil simulé</span><span class="sxs-lookup"><span data-stu-id="5a2f1-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="5a2f1-107">Dans ce didacticiel, commencer par découvrir hello les bases de l’utilisation de [IoT passerelle Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="5a2f1-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="5a2f1-108">Vous allez travailler avec Intel NUC exécutant Wind River Linux.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="5a2f1-109">Vous allez apprendre comment tooseamleesly connecter votre cloud toohello de périphériques à l’aide d’Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="5a2f1-110">**Vous n’avez pas encore de kit ?** Cliquez [ici](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="5a2f1-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="5a2f1-111">Leçon 1 : Configuration de votre NUC</span><span class="sxs-lookup"><span data-stu-id="5a2f1-111">Lesson 1: Configure your NUC</span></span>
![Diagramme de bout en bout pour la leçon 1](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="5a2f1-113">Dans cette leçon, vous pouvez paramétrer des NUC Intel (suivant unité de calcul) Bonjour Kit comme passerelle Azure IoT, hello Azure IoT bord installer sur NUC et exécuter une fonctionnalité de passerelle exemple application tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="5a2f1-114">*Estimation du temps toocomplete : 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="5a2f1-114">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="5a2f1-115">Accédez trop[configurer NUC Intel comme passerelle IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="5a2f1-115">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="5a2f1-116">Leçon 2 : Création de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5a2f1-116">Lesson 2: Create your IoT Hub</span></span>
![Diagramme de bout en bout pour la leçon 2](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="5a2f1-118">Dans cette leçon, vous installez les outils de hello et des logiciels sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-118">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="5a2f1-119">Puis vous créez gratuitement un compte Azure, configurez votre concentrateur Azure IoT et créez votre premier appareil dans le hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="5a2f1-120">Avant de commencer cette leçon, terminez la Leçon 1.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="5a2f1-121">Obtenir les outils de hello</span><span class="sxs-lookup"><span data-stu-id="5a2f1-121">Get hello tools</span></span>
<span data-ttu-id="5a2f1-122">Installez les outils hello et logiciels sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-122">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="5a2f1-123">*Estimation du temps toocomplete : 20 minutes*</span><span class="sxs-lookup"><span data-stu-id="5a2f1-123">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="5a2f1-124">Accédez trop[obtenir hello tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="5a2f1-124">Go too[Get hello tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="5a2f1-125">Créer un IoT hub et enregistrer votre appareil</span><span class="sxs-lookup"><span data-stu-id="5a2f1-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="5a2f1-126">Créer votre groupe de ressources et configurer votre concentrateur Azure IoT première ajouter votre premier appareil toohello IoT hub à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-126">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="5a2f1-127">*Estimation du temps toocomplete : 10 minutes*</span><span class="sxs-lookup"><span data-stu-id="5a2f1-127">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="5a2f1-128">Accédez trop[créez un IoT hub et inscrire votre appareil](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="5a2f1-128">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="5a2f1-129">Leçon 3 : Recevoir des messages à partir de l’appareil simulé de hello et lire des messages à partir de votre hub IoT</span><span class="sxs-lookup"><span data-stu-id="5a2f1-129">Lesson 3: Receive messages from hello simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="5a2f1-130">Dans cette leçon, vous allez utiliser la configuration de scripts tooautomate hello et l’exécution d’une application d’appareil simulé dans votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-130">In this lesson, you will use scripts tooautomate hello configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="5a2f1-131">application d’appareil simulé Hello génère les exemples de données de température et il envoie le module de hub IoT tooan.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-131">hello simulated device app generates sample temperature data and sends it tooan IoT hub module.</span></span> <span data-ttu-id="5a2f1-132">Bonjour les packages de module de hub IoT les données de salutation reçu et l’envoie tooyour IoT hub via l’infrastructure de passerelle hello fournie dans Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-132">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Diagramme de bout en bout pour la leçon 3](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="5a2f1-134">Configurer et exécuter un appareil simulé</span><span class="sxs-lookup"><span data-stu-id="5a2f1-134">Configure and run a simulated device</span></span>
<span data-ttu-id="5a2f1-135">Préparer les exemples de code hello.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-135">Prepare hello sample codes.</span></span> <span data-ttu-id="5a2f1-136">Puis configurez et exécutez hello simulée appareil exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-136">Then configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="5a2f1-137">*Estimation du temps toocomplete : 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="5a2f1-137">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="5a2f1-138">Accédez trop[configurer et exécuter un appareil simulé](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="5a2f1-138">Go too[Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="5a2f1-139">Lire des messages à partir de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5a2f1-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="5a2f1-140">Exécuter un exemple de code sur votre hôte ordinateur tooread hello des messages à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-140">Run a sample code on your host computer tooread hello messages from your IoT hub.</span></span>

<span data-ttu-id="5a2f1-141">*Estimation du temps toocomplete : 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="5a2f1-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="5a2f1-142">Accédez trop[lire les messages de votre hub IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="5a2f1-142">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="5a2f1-143">Leçon 4 : Enregistrer des messages tooAzure le stockage de Table</span><span class="sxs-lookup"><span data-stu-id="5a2f1-143">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="5a2f1-144">Créer une application Azure de fonction qui obtient les messages entrants à partir de votre IoT hub et les écrit tooAzure le stockage de Table.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Diagramme de bout en bout pour la leçon 4](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="5a2f1-146">Création d’une application de fonction Azure et d’un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="5a2f1-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="5a2f1-147">Utilisez un toocreate de modèle Azure Resource Manager une application Azure (fonction) et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-147">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="5a2f1-148">*Estimation du temps toocomplete : 10 minutes*</span><span class="sxs-lookup"><span data-stu-id="5a2f1-148">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="5a2f1-149">Accédez trop[créer une application de la fonction Azure et d’un compte de stockage Azure](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="5a2f1-149">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="5a2f1-150">Lire des messages conservés dans le stockage Table Azure</span><span class="sxs-lookup"><span data-stu-id="5a2f1-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="5a2f1-151">Surveiller les messages de passerelle dans le cloud hello qu’ils sont écrits tooAzure le stockage de Table.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-151">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="5a2f1-152">*Estimation du temps toocomplete : 5 minutes*</span><span class="sxs-lookup"><span data-stu-id="5a2f1-152">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="5a2f1-153">Accédez trop[lire les messages conservés dans le stockage Azure Table](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="5a2f1-153">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5a2f1-154">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="5a2f1-154">Troubleshooting</span></span>
<span data-ttu-id="5a2f1-155">Si vous rencontrez des problèmes au cours des leçons de hello, rechercher des solutions dans hello [dépannage](iot-hub-gateway-kit-c-sim-troubleshooting.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-155">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="5a2f1-156">Aller plus loin</span><span class="sxs-lookup"><span data-stu-id="5a2f1-156">Explore more</span></span>
<span data-ttu-id="5a2f1-157">Visitez hello [zone pour développeurs Intel IoT passerelle Kit](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="5a2f1-157">Visit hello [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn more.</span></span>
