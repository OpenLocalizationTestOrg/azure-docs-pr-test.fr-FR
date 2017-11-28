---
title: toocloud aaaSimulated framboises Pi (Node.js) - simulateur tooAzure IoT Hub de connecter un Pi framboises web | Documents Microsoft
description: "Se connecter framboises Pi web simulateur tooAzure IoT Hub pour framboises Pi toosend données toohello cloud Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "pi raspberry Raspberry pi simulateur, azure raspberry pi, raspberry pi iot hub iot, envoyer des données toocloud, raspberry pi toocloud"
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/28/2017
ms.author: xshi
ms.openlocfilehash: 83736caf6ce723a49001058495a780f7f51946a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a><span data-ttu-id="9f300-104">Se connecter framboises Pi en ligne simulateur tooAzure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="9f300-104">Connect Raspberry Pi online simulator tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="9f300-105">Dans ce didacticiel, commencer par découvrir hello les bases de l’utilisation de simulateur en ligne de framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="9f300-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="9f300-106">Vous apprendrez ensuite comment tooseamlessly connecter le cloud de toohello hello Pi simulateur à l’aide de [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="9f300-106">You then learn how tooseamlessly connect hello Pi simulator toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="9f300-107">Si vous avez des périphériques physiques, visitez [tooAzure de connecter un Pi framboises IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget a démarré.</span><span class="sxs-lookup"><span data-stu-id="9f300-107">If you have physical devices, visit [Connect Raspberry Pi tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="9f300-108">Procédure</span><span class="sxs-lookup"><span data-stu-id="9f300-108">What you do</span></span>

* <span data-ttu-id="9f300-109">Découvrez les principes de base de hello du simulateur en ligne de framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="9f300-109">Learn hello basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="9f300-110">Créez un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9f300-110">Create an IoT hub.</span></span>
* <span data-ttu-id="9f300-111">Inscrivez un appareil pour Pi dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9f300-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="9f300-112">Exécuter un exemple d’application sur Pi toosend simulée capteur données tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9f300-112">Run a sample application on Pi toosend simulated sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="9f300-113">Se connecter simulé framboises Pi tooan IoT hub que vous créez.</span><span class="sxs-lookup"><span data-stu-id="9f300-113">Connect simulated Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="9f300-114">Puis, vous exécutez un exemple d’application avec des données de capteur toogenerate hello simulateur.</span><span class="sxs-lookup"><span data-stu-id="9f300-114">Then you run a sample application with hello simulator toogenerate sensor data.</span></span> <span data-ttu-id="9f300-115">Enfin, vous envoyez le hub IoT tooyour hello capteur données.</span><span class="sxs-lookup"><span data-stu-id="9f300-115">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="9f300-116">Contenu</span><span class="sxs-lookup"><span data-stu-id="9f300-116">What you learn</span></span>

* <span data-ttu-id="9f300-117">Comment toocreate un Azure IoT hub et obtenir votre nouvelle chaîne de connexion de périphérique.</span><span class="sxs-lookup"><span data-stu-id="9f300-117">How toocreate an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="9f300-118">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="9f300-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="9f300-119">Comment toowork au Simulateur framboises Pi en ligne.</span><span class="sxs-lookup"><span data-stu-id="9f300-119">How toowork with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="9f300-120">Comment le hub IoT tooyour toosend capteur données.</span><span class="sxs-lookup"><span data-stu-id="9f300-120">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="9f300-121">Vue d’ensemble du simulateur web Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="9f300-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="9f300-122">Cliquez sur le simulateur en ligne de hello bouton toolaunch framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="9f300-122">Click hello button toolaunch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
<span data-ttu-id="9f300-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Démarrer le simulateur Raspberry Pi</a></span><span class="sxs-lookup"><span data-stu-id="9f300-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Start Raspberry Pi Simulator</a></span></span>

<span data-ttu-id="9f300-124">Il existe trois domaines dans le simulateur de web hello.</span><span class="sxs-lookup"><span data-stu-id="9f300-124">There are three areas in hello web simulator.</span></span>
1. <span data-ttu-id="9f300-125">Zone d’assemblage - hello par défaut est qu’un Pi se connecte avec un capteur BME280 et une DEL.</span><span class="sxs-lookup"><span data-stu-id="9f300-125">Assembly area - hello default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="9f300-126">zone de Hello est verrouillée dans la version d’évaluation donc actuellement, vous ne pouvez pas faire personnalisation.</span><span class="sxs-lookup"><span data-stu-id="9f300-126">hello area is locked in preview version so currently you cannot do customization.</span></span>
2. <span data-ttu-id="9f300-127">Codage zone - un éditeur de code en ligne pour vous toocode avec framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="9f300-127">Coding area - An online code editor for you toocode with Raspberry Pi.</span></span> <span data-ttu-id="9f300-128">application d’exemple Hello par défaut permet de données de capteur toocollect BME280 capteur et envoie tooyour Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9f300-128">hello default sample application helps toocollect sensor data from BME280 sensor and sends tooyour Azure IoT Hub.</span></span> <span data-ttu-id="9f300-129">application Hello est entièrement compatible avec les appareils Pi réels.</span><span class="sxs-lookup"><span data-stu-id="9f300-129">hello application is fully compatible with real Pi devices.</span></span> 
3. <span data-ttu-id="9f300-130">Fenêtre de console intégrée - il montre sortie hello de votre code.</span><span class="sxs-lookup"><span data-stu-id="9f300-130">Integrated console window - It shows hello output of your code.</span></span> <span data-ttu-id="9f300-131">Hello en haut de cette fenêtre, il existe trois boutons.</span><span class="sxs-lookup"><span data-stu-id="9f300-131">At hello top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="9f300-132">**Exécutez** -exécuter l’application hello Bonjour zone de codage.</span><span class="sxs-lookup"><span data-stu-id="9f300-132">**Run** - Run hello application in hello coding area.</span></span>
   * <span data-ttu-id="9f300-133">**Réinitialiser** -hello réinitialisation exemple d’application de zone toohello par défaut de codage.</span><span class="sxs-lookup"><span data-stu-id="9f300-133">**Reset** - Reset hello coding area toohello default sample application.</span></span>
   * <span data-ttu-id="9f300-134">**Pli/développement** - sur hello droite côté il existe un bouton pour vous toofold/développement hello fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="9f300-134">**Fold/Expand** - On hello right side there is a button for you toofold/expand hello console window.</span></span>

> [!NOTE] 
<span data-ttu-id="9f300-135">Simulateur de web Pi de framboises Hello est désormais disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="9f300-135">hello Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="9f300-136">Nous aimerions toohear votre voix Bonjour [Gitter un accroissement](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="9f300-136">We'd like toohear your voice in hello [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="9f300-137">code source de Hello est public sur [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="9f300-137">hello source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Vue d’ensemble du simulateur en ligne Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="9f300-139">Exécuter un exemple d’application sur le simulateur web Pi</span><span class="sxs-lookup"><span data-stu-id="9f300-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="9f300-140">Dans la zone de codage, assurez-vous que vous travaillez sur l’application d’exemple hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="9f300-140">In coding area, make sure you are working on hello default sample application.</span></span> <span data-ttu-id="9f300-141">Remplacez espace réservé de hello dans la ligne 15 hello chaîne de connexion de périphérique Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9f300-141">Replace hello placeholder in Line 15 with hello Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="9f300-142">![Remplacez la chaîne de connexion de périphérique hello](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="9f300-142">![Replace hello device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="9f300-143">Cliquez sur **exécuter** ou type `npm start` application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="9f300-143">Click **Run** or type `npm start` toorun hello application.</span></span>


<span data-ttu-id="9f300-144">Vous devez voir hello suivant de sortie qui affiche les données de capteur hello et messages hello envoyés tooyour IoT hub ![sortie - données de capteur envoyés à partir de hub IoT de tooyour framboises Pi](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="9f300-144">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub ![Output - sensor data sent from Raspberry Pi tooyour IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="9f300-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9f300-145">Next steps</span></span>

<span data-ttu-id="9f300-146">Vous avez exécuté un exemple de données de capteur application toocollect et envoyez tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9f300-146">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
