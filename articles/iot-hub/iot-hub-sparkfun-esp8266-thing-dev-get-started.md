---
title: "ESP8266 vers cloud - Connecter la carte Sparkfun ESP8266 Thing Dev à Azure IoT Hub | Microsoft Docs"
description: "Dans ce didacticiel, découvrez comment configurer et connecter Sparkfun ESP8266 Thing Dev à Azure IoT Hub pour lui permettre d’envoyer des données à la plateforme cloud Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 557f0cdf375b345e0dbe0526f5a5bd3c050dec38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="5ad8c-103">Connecter la carte Sparkfun ESP8266 Thing Dev à Azure IoT Hub dans le cloud</span><span class="sxs-lookup"><span data-stu-id="5ad8c-103">Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![connexion entre un capteur DHT22, Thing Dev et IoT Hub](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="5ad8c-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="5ad8c-105">What you will do</span></span>

<span data-ttu-id="5ad8c-106">Connectez la carte Sparkfun ESP8266 Thing Dev à une instance Azure IoT Hub que vous allez créer.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-106">Connect Sparkfun ESP8266 Thing Dev to an IoT hub you will create.</span></span> <span data-ttu-id="5ad8c-107">Ensuite, vous exécuterez un exemple d’application sur l’ESP8266 pour collecter des données de température et d’humidité provenant d’un capteur DHT22.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-107">Then run a sample application on ESP8266 to collect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="5ad8c-108">Enfin, vous enverrez les données du capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-108">Finally, send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="5ad8c-109">Si vous utilisez une autre carte ESP8266, vous pouvez également suivre ces étapes pour la connecter à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-109">If you are using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="5ad8c-110">Selon la carte ESP8266 que vous utilisez, il se peut que vous deviez reconfigurer le paramètre `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-110">Depending on the ESP8266 board you are using, you may need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="5ad8c-111">Par exemple, si vous utilisez l’ESP8266 d’AI-Thinker, vous devrez peut-être remplacer la valeur `0` de ce paramètre par `2`.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` to `2`.</span></span> <span data-ttu-id="5ad8c-112">Vous n’avez pas encore de kit ? Cliquez [ici](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="5ad8c-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5ad8c-113">Contenu</span><span class="sxs-lookup"><span data-stu-id="5ad8c-113">What you will learn</span></span>

* <span data-ttu-id="5ad8c-114">Création d’une instance IoT Hub et enregistrement d’un appareil pour la carte Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-114">How to create an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="5ad8c-115">Connexion de la carte Thing Dev au capteur et à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-115">How to connect Thing Dev with the sensor and your computer.</span></span>
* <span data-ttu-id="5ad8c-116">Collecte des données du capteur via l’exécution d’un exemple d’application sur une carte Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-116">How to collect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="5ad8c-117">Envoi des données du capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-117">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="5ad8c-118">Éléments requis</span><span class="sxs-lookup"><span data-stu-id="5ad8c-118">What you will need</span></span>

![Composants requis pour le didacticiel](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="5ad8c-120">Pour effectuer cette opération, vous aurez besoin des composants suivants de votre Kit de démarrage Thing Dev :</span><span class="sxs-lookup"><span data-stu-id="5ad8c-120">To complete this operation, you need the following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="5ad8c-121">Une carte Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-121">The Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="5ad8c-122">Un câble Micro USB Micro B vers USB Type A.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-122">A Micro USB to Type A USB cable.</span></span>

<span data-ttu-id="5ad8c-123">Vous aurez également besoin des éléments suivants pour votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="5ad8c-123">You also need the following for your development environment:</span></span>

* <span data-ttu-id="5ad8c-124">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-124">An active Azure subscription.</span></span> <span data-ttu-id="5ad8c-125">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="5ad8c-126">Un Mac ou un PC exécutant Windows ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="5ad8c-127">Un réseau sans fil pour la connexion de la carte Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-127">Wireless network for Sparkfun ESP8266 Thing Dev to connect to.</span></span>
* <span data-ttu-id="5ad8c-128">Une connexion Internet pour télécharger l’outil de configuration.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-128">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="5ad8c-129">[L’IDE Arduino](https://www.arduino.cc/en/main/software) version 1.6.8 ou ultérieure (les versions antérieures ne fonctionneront pas avec la bibliothèque AzureIoT).</span><span class="sxs-lookup"><span data-stu-id="5ad8c-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with the AzureIoT library.</span></span>

<span data-ttu-id="5ad8c-130">Les éléments suivants sont facultatifs si vous n’avez pas de capteur.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-130">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="5ad8c-131">Vous avez également la possibilité d’utiliser des données de capteur simulées.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-131">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="5ad8c-132">Un capteur de température et d’humidité Adafruit DHT22.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="5ad8c-133">Une platine d’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-133">A breadboard.</span></span>
* <span data-ttu-id="5ad8c-134">Des câbles de liaison M/M.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-the-sensor-and-your-computer"></a><span data-ttu-id="5ad8c-135">Connecter la carte ESP8266 Thing Dev au capteur et à votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="5ad8c-135">Connect ESP8266 Thing Dev with the sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-esp8266-thing-dev"></a><span data-ttu-id="5ad8c-136">Connecter un capteur de température et d’humidité DHT22 à la carte ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="5ad8c-136">Connect a DHT22 temperature and humidity sensor to ESP8266 Thing Dev</span></span>

<span data-ttu-id="5ad8c-137">Utilisez la platine d’expérimentation et les câbles de liaison pour effectuer la connexion comme suit.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-137">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="5ad8c-138">Si vous n’avez pas de capteur, ignorez cette section. Vous pourrez utiliser des données de capteur simulées à la place.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Schéma des connexions](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="5ad8c-140">Pour les broches du capteur, nous utiliserons le câblage suivant :</span><span class="sxs-lookup"><span data-stu-id="5ad8c-140">For sensor pins, we will use the following wiring:</span></span>

| <span data-ttu-id="5ad8c-141">Début (capteur)</span><span class="sxs-lookup"><span data-stu-id="5ad8c-141">Start (Sensor)</span></span>           | <span data-ttu-id="5ad8c-142">Fin (carte)</span><span class="sxs-lookup"><span data-stu-id="5ad8c-142">End (Board)</span></span>           | <span data-ttu-id="5ad8c-143">Couleur du câble</span><span class="sxs-lookup"><span data-stu-id="5ad8c-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="5ad8c-144">VDD (broche 27F)</span><span class="sxs-lookup"><span data-stu-id="5ad8c-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="5ad8c-145">3V (broche 8A)</span><span class="sxs-lookup"><span data-stu-id="5ad8c-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="5ad8c-146">Câble rouge</span><span class="sxs-lookup"><span data-stu-id="5ad8c-146">Red cable</span></span>     |
| <span data-ttu-id="5ad8c-147">DATA (broche 28F)</span><span class="sxs-lookup"><span data-stu-id="5ad8c-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="5ad8c-148">GPIO 2 (broche 9A)</span><span class="sxs-lookup"><span data-stu-id="5ad8c-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="5ad8c-149">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="5ad8c-149">White cable</span></span>    |
| <span data-ttu-id="5ad8c-150">GND (broche 30F)</span><span class="sxs-lookup"><span data-stu-id="5ad8c-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="5ad8c-151">GND (broche 7J)</span><span class="sxs-lookup"><span data-stu-id="5ad8c-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="5ad8c-152">Câble noir</span><span class="sxs-lookup"><span data-stu-id="5ad8c-152">Black cable</span></span>   |


- <span data-ttu-id="5ad8c-153">Pour en savoir plus, consultez les [détails de la configuration du capteur DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) et les [spécifications relatives à la carte Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711).</span><span class="sxs-lookup"><span data-stu-id="5ad8c-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="5ad8c-154">Votre carte Sparkfun ESP8266 Thing Dev devrait à présent être connectée à un capteur opérationnel.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![connecter un capteur dht22 à la carte ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-to-your-computer"></a><span data-ttu-id="5ad8c-156">Connecter la carte Sparkfun ESP8266 Thing Dev à votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="5ad8c-156">Connect Sparkfun ESP8266 Thing Dev to your computer</span></span>

<span data-ttu-id="5ad8c-157">À l’aide du câble Micro USB vers USB Type A, connectez la carte Sparkfun ESP8266 Thing Dev à votre ordinateur en procédant comme suit.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-157">Use the Micro USB to Type A USB cable to connect Sparkfun ESP8266 Thing Dev to your computer as follows.</span></span>

![Connexion de la carte Feather HUZZAH à votre ordinateur](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="5ad8c-159">Ajouter des autorisations de port série (Ubuntu uniquement)</span><span class="sxs-lookup"><span data-stu-id="5ad8c-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="5ad8c-160">Si vous utilisez Ubuntu, assurez-vous qu’un utilisateur normal dispose des autorisations nécessaires pour utiliser le port USB de la carte Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-160">If you use Ubuntu, make sure a normal user has the permissions to operate on the USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="5ad8c-161">Pour ajouter des autorisations de port série pour un utilisateur normal, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5ad8c-161">To add serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="5ad8c-162">Dans un terminal, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5ad8c-162">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="5ad8c-163">Vous obtenez l’une des sorties suivantes :</span><span class="sxs-lookup"><span data-stu-id="5ad8c-163">You get one of the following outputs:</span></span>

   * <span data-ttu-id="5ad8c-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="5ad8c-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="5ad8c-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="5ad8c-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="5ad8c-166">Dans la sortie, `uucp` ou `dialout` correspond au nom du propriétaire du groupe du port USB.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-166">In the output, notice `uucp` or `dialout` that is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="5ad8c-167">Ajoutez l’utilisateur au groupe en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5ad8c-167">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="5ad8c-168">`<group-owner-name>` est le nom du propriétaire du groupe que vous avez obtenu à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-168">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="5ad8c-169">`<username>` est le nom de votre utilisateur Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="5ad8c-170">Déconnectez-vous de Ubuntu et connectez-vous à nouveau pour que la modification prenne effet.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-170">Log out Ubuntu and log in it again for the change to take effect.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="5ad8c-171">Collecter les données du capteur et les envoyer à votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5ad8c-171">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="5ad8c-172">Dans cette section, vous allez déployer et exécuter un exemple d’application sur la carte Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="5ad8c-173">L’exemple d’application fait clignoter la LED de la carte Sparkfun ESP8266 Thing Dev et envoie les données de température et d’humidité collectées à partir du capteur DHT22 à votre instance IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-173">The sample application blinks the LED on Sparkfun ESP8266 Thing Dev and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="5ad8c-174">Obtenir l’exemple d’application à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="5ad8c-174">Get the sample application from GitHub</span></span>

<span data-ttu-id="5ad8c-175">L’exemple d’application est hébergé sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-175">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="5ad8c-176">Clonez l’exemple de référentiel contenant l’exemple d’application à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-176">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="5ad8c-177">Pour cloner l’exemple de référentiel, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5ad8c-177">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="5ad8c-178">Ouvrez une invite de commandes ou une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="5ad8c-179">Accédez au dossier à utiliser pour le stockage de l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-179">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="5ad8c-180">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5ad8c-180">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="5ad8c-181">Installez le package de la carte Sparkfun ESP8266 Thing Dev dans l’IDE Arduino :</span><span class="sxs-lookup"><span data-stu-id="5ad8c-181">Install the package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="5ad8c-182">Ouvrez le dossier où l’exemple d’application est stocké.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-182">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="5ad8c-183">Ouvrez le fichier app.ino dans le dossier app de l’IDE Arduino.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-183">Open the app.ino file in the app folder in Arduino IDE.</span></span>

   ![Ouverture de l’exemple d’application dans l’IDE Arduino](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="5ad8c-185">Dans l’IDE Arduino, cliquez sur **Fichier** > **Préférences**.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-185">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="5ad8c-186">Dans la boîte de dialogue **Préférences**, cliquez sur l’icône en regard de la zone de texte **URL de gestionnaire de cartes supplémentaires**.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-186">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="5ad8c-187">Dans la fenêtre contextuelle, entrez l’URL suivante, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-187">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Pointage vers l’URL d’un package dans l’IDE Arduino](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="5ad8c-189">Dans la boîte de dialogue **Préférences**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-189">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="5ad8c-190">Cliquez sur **Outils** > **Type de carte** > **Gestionnaire de carte**, puis recherchez « esp8266 ».</span><span class="sxs-lookup"><span data-stu-id="5ad8c-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="5ad8c-191">La version 2.2.0 ou ultérieure du package ESP8266 doit être installée.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![Le package ESP8266 est installé](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="5ad8c-193">Cliquez sur **Outils** > **Carte** > **Sparkfun ESP8266 Thing Dev**.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="5ad8c-194">Installer les bibliothèques nécessaires</span><span class="sxs-lookup"><span data-stu-id="5ad8c-194">Install necessary libraries</span></span>

1. <span data-ttu-id="5ad8c-195">Dans l’IDE Arduino, cliquez sur **Croquis** > **Inclure une bibliothèque** > **Gérer les bibliothèques**.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-195">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="5ad8c-196">Recherchez les noms de bibliothèque suivants un par un.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-196">Search for the following library names one by one.</span></span> <span data-ttu-id="5ad8c-197">Pour chacune des bibliothèques trouvées, cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-197">For each of the library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="5ad8c-198">Vous n’avez pas de capteur DHT22 ?</span><span class="sxs-lookup"><span data-stu-id="5ad8c-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="5ad8c-199">L’exemple d’application permet de simuler des données de température et d’humidité si vous n’avez pas de capteur DHT22.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-199">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="5ad8c-200">Pour activer l’utilisation de données simulées par l’exemple d’application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5ad8c-200">To enable the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="5ad8c-201">Ouvrez le fichier `config.h` dans le dossier `app`.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-201">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="5ad8c-202">Recherchez la ligne de code suivante et remplacez la valeur `false` par `true` :</span><span class="sxs-lookup"><span data-stu-id="5ad8c-202">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configuration de l’exemple d’application pour utiliser des données simulées](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="5ad8c-204">Enregistrez avec `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-204">Save with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-sparkfun-esp8266-thing-dev"></a><span data-ttu-id="5ad8c-205">Déployer l’exemple d’application sur la carte Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="5ad8c-205">Deploy the sample application to Sparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="5ad8c-206">Dans l’IDE Arduino, cliquez sur **Outil** > **Port**, puis sélectionnez le port série de la carte Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-206">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="5ad8c-207">Cliquez sur **Croquis** > **Téléverser** pour générer et déployer l’exemple d’application sur la carte Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-207">Click **Sketch** > **Upload** to build and deploy the sample application to Sparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="5ad8c-208">Si vous utilisez macOS, vous avez probablement pu voir les messages suivants lors du chargement.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-208">If you are using macOS you could probably see the following messages during uploading.</span></span> <span data-ttu-id="5ad8c-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="5ad8c-210">Ouvrez la fenêtre du terminal et terminez les actions ci-dessous pour résoudre ce problème.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-210">Please open your ternimal window and finish below actions to solve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="5ad8c-211">Entrer vos informations d’identification</span><span class="sxs-lookup"><span data-stu-id="5ad8c-211">Enter your credentials</span></span>

<span data-ttu-id="5ad8c-212">Une fois le chargement terminé, suivez cette procédure pour entrer vos informations d’identification :</span><span class="sxs-lookup"><span data-stu-id="5ad8c-212">After the upload completes successfully, follow the steps to enter your credentials:</span></span>

1. <span data-ttu-id="5ad8c-213">Dans l’IDE Arduino, cliquez sur **Outils** > **Moniteur série**.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-213">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="5ad8c-214">Dans la fenêtre Moniteur série, vous pouvez remarquer la présence de deux listes déroulantes dans l’angle inférieur droit.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-214">In the serial monitor window, notice the two drop-down lists on the bottom right corner.</span></span>
1. <span data-ttu-id="5ad8c-215">Pour la liste déroulante de gauche, sélectionnez **Pas de fin de ligne**.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-215">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="5ad8c-216">Pour la liste déroulante de droite, sélectionnez **115200 baud**.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-216">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="5ad8c-217">Dans la zone de saisie située en haut de la fenêtre Moniteur série, entrez les informations suivantes si elles vous sont demandées, puis cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-217">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="5ad8c-218">SSID Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="5ad8c-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="5ad8c-219">Mot de passe Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="5ad8c-219">Wi-Fi password</span></span>
   * <span data-ttu-id="5ad8c-220">Chaîne de connexion de l’appareil</span><span class="sxs-lookup"><span data-stu-id="5ad8c-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="5ad8c-221">Les informations d’identification sont stockées dans la mémoire EEPROM de la carte Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-221">The credential information is stored in the EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="5ad8c-222">Si vous cliquez sur le bouton de réinitialisation de la carte Sparkfun ESP8266 Thing Dev, l’exemple d’application vous demande si vous souhaitez effacer ces informations.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-222">If you click the reset button on the Sparkfun ESP8266 Thing Dev board, the sample application asks you if you want to erase the information.</span></span> <span data-ttu-id="5ad8c-223">Entrez `Y` pour les effacer. Vous serez alors à nouveau invité à fournir ces informations.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-223">Enter `Y` to have the information erased and you are asked to provide the information again.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="5ad8c-224">Vérifier que l’exemple d’application s’exécute correctement</span><span class="sxs-lookup"><span data-stu-id="5ad8c-224">Verify the sample application is running successfully</span></span>

<span data-ttu-id="5ad8c-225">Si vous voyez la sortie suivante dans la fenêtre Moniteur série, et si la LED clignote sur la carte Sparkfun ESP8266 Thing Dev, cela signifie que l’exemple d’application s’exécute correctement.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-225">If you see the following output from the serial monitor window and the blinking LED on Sparkfun ESP8266 Thing Dev, the sample application is running successfully.</span></span>

![Sortie finale dans l’IDE Arduino](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="5ad8c-227">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5ad8c-227">Next steps</span></span>

<span data-ttu-id="5ad8c-228">Vous avez correctement connecté une carte Sparkfun ESP8266 Thing Dev à votre instance IoT Hub et envoyé les données de capteur collectées à cette instance.</span><span class="sxs-lookup"><span data-stu-id="5ad8c-228">You have successfully connected a Sparkfun ESP8266 Thing Dev to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
