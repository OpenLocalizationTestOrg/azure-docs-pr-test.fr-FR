---
title: "Raspberry Pi vers cloud (Node.js) simulé - Connecter le simulateur web Raspberry Pi à Azure IoT Hub | Microsoft Docs"
description: "Connectez le simulateur web Raspberry Pi à Azure IoT Hub pour que Raspberry Pi puisse envoyer des données vers le cloud Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "simulateur raspberry, azure iot raspberry pi, raspberry pi iot hub, raspberry pi envoie des données vers le cloud, raspberry pi vers cloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 5b7e209b65ccf6edb32d211797663e5e5b170df8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-raspberry-pi-online-simulator-to-azure-iot-hub-nodejs"></a><span data-ttu-id="ac561-104">Connecter le simulateur en ligne Raspberry Pi à Azure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="ac561-104">Connect Raspberry Pi online simulator to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="ac561-105">Dans ce didacticiel, vous commencez par découvrir les principes fondamentaux de l’utilisation du simulateur en ligne Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="ac561-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="ac561-106">Vous apprenez ensuite à connecter en toute transparence le simulateur Pi au cloud à l’aide d’[Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="ac561-106">You then learn how to seamlessly connect the Pi simulator to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="ac561-107">Si vous avez des appareils physiques, voir [Connecter Raspberry Pi à Azure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) pour commencer.</span><span class="sxs-lookup"><span data-stu-id="ac561-107">If you have physical devices, visit [Connect Raspberry Pi to Azure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) to get started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator to Azure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="ac561-108">Procédure</span><span class="sxs-lookup"><span data-stu-id="ac561-108">What you do</span></span>

* <span data-ttu-id="ac561-109">Découvrez les principes fondamentaux du simulateur en ligne Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="ac561-109">Learn the basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="ac561-110">Créez un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ac561-110">Create an IoT hub.</span></span>
* <span data-ttu-id="ac561-111">Inscrivez un appareil pour Pi dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ac561-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="ac561-112">Exécutez un exemple d’application sur Pi pour envoyer des données de capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ac561-112">Run a sample application on Pi to send simulated sensor data to your IoT hub.</span></span>

<span data-ttu-id="ac561-113">Connectez le Raspberry Pi simulé à un IoT Hub que vous créez.</span><span class="sxs-lookup"><span data-stu-id="ac561-113">Connect simulated Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="ac561-114">Exécutez ensuite un exemple d’application avec le simulateur pour générer des données de capteur.</span><span class="sxs-lookup"><span data-stu-id="ac561-114">Then you run a sample application with the simulator to generate sensor data.</span></span> <span data-ttu-id="ac561-115">Enfin, envoyez les données du capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ac561-115">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="ac561-116">Contenu</span><span class="sxs-lookup"><span data-stu-id="ac561-116">What you learn</span></span>

* <span data-ttu-id="ac561-117">Création d’un Azure IoT Hub et obtention de la chaîne de connexion de votre nouvel appareil.</span><span class="sxs-lookup"><span data-stu-id="ac561-117">How to create an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="ac561-118">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="ac561-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="ac561-119">Utilisation du simulateur en ligne Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="ac561-119">How to work with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="ac561-120">Envoi des données du capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ac561-120">How to send sensor data to your IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="ac561-121">Vue d’ensemble du simulateur web Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="ac561-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="ac561-122">Cliquez sur le bouton pour lancer le simulateur en ligne Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="ac561-122">Click the button to launch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
[<span data-ttu-id="ac561-123">Démarrer le simulateur Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="ac561-123">Start Raspberry Pi simulator</span></span>](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

<span data-ttu-id="ac561-124">Le simulateur web comprend trois zones.</span><span class="sxs-lookup"><span data-stu-id="ac561-124">There are three areas in the web simulator.</span></span>
* <span data-ttu-id="ac561-125">Zone d’assemblage : le circuit par défaut est celui qu’un Pi connecte à un capteur BME280 et à une DEL.</span><span class="sxs-lookup"><span data-stu-id="ac561-125">Assembly area - The default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="ac561-126">La zone étant verrouillée dans la préversion, vous ne pouvez pas apporter de personnalisation.</span><span class="sxs-lookup"><span data-stu-id="ac561-126">The area is locked in preview version so currently you cannot do customization.</span></span>
* <span data-ttu-id="ac561-127">Zone de codage : éditeur de code en ligne permettant de coder avec Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="ac561-127">Coding area - An online code editor for you to code with Raspberry Pi.</span></span> <span data-ttu-id="ac561-128">L’exemple d’application par défaut aide à collecter les données du capteur BME280 et à les envoyer à votre Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ac561-128">The default sample application helps to collect sensor data from BME280 sensor and sends to your Azure IoT Hub.</span></span> <span data-ttu-id="ac561-129">L’application est entièrement compatible avec les appareils Pi réels.</span><span class="sxs-lookup"><span data-stu-id="ac561-129">The application is fully compatible with real Pi devices.</span></span> 
* <span data-ttu-id="ac561-130">Fenêtre de console intégrée : montre la sortie de votre code.</span><span class="sxs-lookup"><span data-stu-id="ac561-130">Integrated console window - It shows the output of your code.</span></span> <span data-ttu-id="ac561-131">En haut de cette fenêtre figurent trois boutons.</span><span class="sxs-lookup"><span data-stu-id="ac561-131">At the top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="ac561-132">**Exécuter** : exécuter l’application dans la zone de codage.</span><span class="sxs-lookup"><span data-stu-id="ac561-132">**Run** - Run the application in the coding area.</span></span>
   * <span data-ttu-id="ac561-133">**Réinitialiser**: réinitialiser la zone de codage pour l’exemple d’application par défaut.</span><span class="sxs-lookup"><span data-stu-id="ac561-133">**Reset** - Reset the coding area to the default sample application.</span></span>
   * <span data-ttu-id="ac561-134">**Plier/Développer** : situé du côté droit, ce bouton permet de plier/développer la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="ac561-134">**Fold/Expand** - On the right side there is a button for you to fold/expand the console window.</span></span>

> [!NOTE] 
<span data-ttu-id="ac561-135">Le simulateur web Raspberry Pi est désormais disponible en préversion.</span><span class="sxs-lookup"><span data-stu-id="ac561-135">The Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="ac561-136">Nous aimerions entendre votre voix dans le [salon de conversation Gitter](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="ac561-136">We'd like to hear your voice in the [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="ac561-137">Le code source est public et disponible sur [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="ac561-137">The source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Vue d’ensemble du simulateur en ligne Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="ac561-139">Exécuter un exemple d’application sur le simulateur web Pi</span><span class="sxs-lookup"><span data-stu-id="ac561-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="ac561-140">Dans la zone de codage, assurez-vous que vous travaillez dans l’exemple d’application par défaut.</span><span class="sxs-lookup"><span data-stu-id="ac561-140">In coding area, make sure you are working on the default sample application.</span></span> <span data-ttu-id="ac561-141">Remplacez l’espace réservé à la ligne 15 par la chaîne de connexion d’appareil Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ac561-141">Replace the placeholder in Line 15 with the Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="ac561-142">![Remplacer la chaîne de connexion d’appareil](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="ac561-142">![Replace the device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="ac561-143">Cliquez sur **Exécuter** ou tapez `npm start` pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="ac561-143">Click **Run** or type `npm start` to run the application.</span></span>


<span data-ttu-id="ac561-144">Vous devriez voir le résultat suivant, qui affiche les données de capteur et les messages envoyés à votre IoT Hub ![Sortie - données de capteur envoyées du Raspberry Pi à votre IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="ac561-144">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub ![Output - sensor data sent from Raspberry Pi to your IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="ac561-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ac561-145">Next steps</span></span>

<span data-ttu-id="ac561-146">Vous avez exécuté un exemple d’application pour collecter des données de capteur et les envoyer à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ac561-146">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
