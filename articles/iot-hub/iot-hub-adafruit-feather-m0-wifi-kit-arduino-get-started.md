---
title: "M0 vers cloud : Connecter la carte Feather M0 WiFi à Azure IoT Hub | Microsoft Docs"
description: "Ce didacticiel explique comment configurer la carte Adafruit Feather M0 WiFi et la connecter à Azure IoT Hub pour envoyer des données à la plateforme cloud Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 0dcf6b46a4c6c743c713d24ce7844e801b278dcf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-adafruit-feather-m0-wifi-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="74a39-103">Connecter Adafruit Feather M0 WiFi à Azure IoT Hub dans le cloud</span><span class="sxs-lookup"><span data-stu-id="74a39-103">Connect Adafruit Feather M0 WiFi to Azure IoT Hub in the cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connexion entre un capteur BME280, une carte Feather M0 WiFi et IoT Hub](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="74a39-105">Dans ce didacticiel, vous commencez par découvrir les principes fondamentaux de l’utilisation de votre carte Arduino.</span><span class="sxs-lookup"><span data-stu-id="74a39-105">In this tutorial, you begin by learning the basics of working with your Arduino board.</span></span> <span data-ttu-id="74a39-106">Vous apprenez ensuite à connecter en toute transparence vos appareils au cloud avec [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="74a39-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="74a39-107">Procédure</span><span class="sxs-lookup"><span data-stu-id="74a39-107">What you do</span></span>

<span data-ttu-id="74a39-108">Connectez Adafruit Feather M0 WiFi à un IoT Hub créé à cette fin.</span><span class="sxs-lookup"><span data-stu-id="74a39-108">Connect Adafruit Feather M0 WiFi to an IoT hub that you create.</span></span> <span data-ttu-id="74a39-109">Exécutez ensuite un exemple d’application sur M0 WiFi pour collecter les données de température et d’humidité provenant d’un capteur BME280.</span><span class="sxs-lookup"><span data-stu-id="74a39-109">Then you run a sample application on M0 WiFi to collect the temperature and humidity data from a BME280.</span></span> <span data-ttu-id="74a39-110">Enfin, envoyez les données du capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="74a39-110">Finally, you send the sensor data to your IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="74a39-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="74a39-111">What you learn</span></span>

* <span data-ttu-id="74a39-112">Création d’un IoT Hub et inscription d’un appareil pour la carte Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="74a39-112">How to create an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="74a39-113">Connexion de la carte Feather M0 WiFi au capteur et à votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="74a39-113">How to connect Feather M0 WiFi with the sensor and your computer</span></span>
* <span data-ttu-id="74a39-114">Collecte des données du capteur en exécutant un exemple d’application sur la carte Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="74a39-114">How to collect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="74a39-115">Envoi des données du capteur à votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="74a39-115">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="74a39-116">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="74a39-116">What you need</span></span>

![Composants requis pour le didacticiel](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="74a39-118">Pour cette opération, vous aurez besoin des composants suivants de votre Kit de démarrage Feather M0 WiFi :</span><span class="sxs-lookup"><span data-stu-id="74a39-118">To complete this operation, you need the following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="74a39-119">La carte Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="74a39-119">The Feather M0 WiFi board</span></span>
* <span data-ttu-id="74a39-120">Un câble Micro USB vers USB Type A</span><span class="sxs-lookup"><span data-stu-id="74a39-120">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="74a39-121">Vous aurez également besoin des éléments suivants pour votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="74a39-121">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="74a39-122">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="74a39-122">An active Azure subscription.</span></span> <span data-ttu-id="74a39-123">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="74a39-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="74a39-124">Un Mac ou un PC exécutant Windows ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="74a39-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="74a39-125">Un réseau sans fil auquel connecter la carte Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="74a39-125">A wireless network for Feather M0 WiFi to connect to.</span></span>
* <span data-ttu-id="74a39-126">Une connexion Internet pour télécharger l’outil de configuration.</span><span class="sxs-lookup"><span data-stu-id="74a39-126">An Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="74a39-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="74a39-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="74a39-128">Les versions antérieures ne fonctionneront pas avec la bibliothèque Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="74a39-128">Earlier versions don't work with the Azure IoT Hub library.</span></span>

<span data-ttu-id="74a39-129">Si vous n’avez pas de capteur, les éléments suivants sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="74a39-129">If you don’t have a sensor, the following items are optional.</span></span> <span data-ttu-id="74a39-130">Vous avez également la possibilité d’utiliser des données de capteur simulées :</span><span class="sxs-lookup"><span data-stu-id="74a39-130">You also have the option of using simulated sensor data:</span></span>

* <span data-ttu-id="74a39-131">Un capteur de température et d’humidité BME280</span><span class="sxs-lookup"><span data-stu-id="74a39-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="74a39-132">Une platine d’expérimentation</span><span class="sxs-lookup"><span data-stu-id="74a39-132">A breadboard</span></span>
* <span data-ttu-id="74a39-133">Des câbles de liaison M/M</span><span class="sxs-lookup"><span data-stu-id="74a39-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-the-sensor-and-your-computer"></a><span data-ttu-id="74a39-134">Connecter la carte Feather M0 WiFi au capteur et à votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="74a39-134">Connect Feather M0 WiFi with the sensor and your computer</span></span>
<span data-ttu-id="74a39-135">Dans cette section, vous connectez les capteurs à votre carte.</span><span class="sxs-lookup"><span data-stu-id="74a39-135">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="74a39-136">Puis vous connectez votre appareil à votre ordinateur pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="74a39-136">Then you plug in your device to your computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-m0-wifi"></a><span data-ttu-id="74a39-137">Connecter un capteur de température et d’humidité DHT22 à la carte Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="74a39-137">Connect a DHT22 temperature and humidity sensor to Feather M0 WiFi</span></span>

<span data-ttu-id="74a39-138">Utilisez la platine d’expérimentation et les câbles de liaison pour effectuer la connexion.</span><span class="sxs-lookup"><span data-stu-id="74a39-138">Use the breadboard and jumper wires to make the connection.</span></span> <span data-ttu-id="74a39-139">Si vous n’avez pas de capteur, ignorez cette section. Vous pourrez utiliser des données de capteur simulées à la place.</span><span class="sxs-lookup"><span data-stu-id="74a39-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Schéma des connexions](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="74a39-141">Pour les broches du capteur, utilisez le câblage suivant :</span><span class="sxs-lookup"><span data-stu-id="74a39-141">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="74a39-142">Début (capteur)</span><span class="sxs-lookup"><span data-stu-id="74a39-142">Start (sensor)</span></span>           | <span data-ttu-id="74a39-143">Fin (carte)</span><span class="sxs-lookup"><span data-stu-id="74a39-143">End (board)</span></span>            | <span data-ttu-id="74a39-144">Couleur du câble</span><span class="sxs-lookup"><span data-stu-id="74a39-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="74a39-145">VDD (broche 27A)</span><span class="sxs-lookup"><span data-stu-id="74a39-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="74a39-146">3V (broche 3A)</span><span class="sxs-lookup"><span data-stu-id="74a39-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="74a39-147">Câble rouge</span><span class="sxs-lookup"><span data-stu-id="74a39-147">Red cable</span></span>     |
| <span data-ttu-id="74a39-148">GND (broche 29A)</span><span class="sxs-lookup"><span data-stu-id="74a39-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="74a39-149">GND (broche 6A)</span><span class="sxs-lookup"><span data-stu-id="74a39-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="74a39-150">Câble noir</span><span class="sxs-lookup"><span data-stu-id="74a39-150">Black cable</span></span>   |
| <span data-ttu-id="74a39-151">SCK (broche 30A)</span><span class="sxs-lookup"><span data-stu-id="74a39-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="74a39-152">SCK (broche 12A)</span><span class="sxs-lookup"><span data-stu-id="74a39-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="74a39-153">Câble jaune</span><span class="sxs-lookup"><span data-stu-id="74a39-153">Yellow cable</span></span>  |
| <span data-ttu-id="74a39-154">SDO (broche 31A)</span><span class="sxs-lookup"><span data-stu-id="74a39-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="74a39-155">MI (broche 14A)</span><span class="sxs-lookup"><span data-stu-id="74a39-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="74a39-156">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="74a39-156">White cable</span></span>   |
| <span data-ttu-id="74a39-157">SDI (broche 32A)</span><span class="sxs-lookup"><span data-stu-id="74a39-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="74a39-158">M0 (broche 13A)</span><span class="sxs-lookup"><span data-stu-id="74a39-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="74a39-159">Câble bleu</span><span class="sxs-lookup"><span data-stu-id="74a39-159">Blue cable</span></span>    |
| <span data-ttu-id="74a39-160">CS (broche 33A)</span><span class="sxs-lookup"><span data-stu-id="74a39-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="74a39-161">GPIO 5 (broche 15J)</span><span class="sxs-lookup"><span data-stu-id="74a39-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="74a39-162">Câble orange</span><span class="sxs-lookup"><span data-stu-id="74a39-162">Orange cable</span></span>  |

<span data-ttu-id="74a39-163">Pour plus d’informations, consultez [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) (Atelier sur le capteur de température, de pression barométrique et d’humidité Adafruit BME280) et [Adafruit Feather M0 WiFi Pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts) (Brochages de la carte Adafruit Feather M0 WiFi).</span><span class="sxs-lookup"><span data-stu-id="74a39-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="74a39-164">Votre carte Feather M0 WiFi devrait à présent être connectée à un capteur opérationnel.</span><span class="sxs-lookup"><span data-stu-id="74a39-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![Connexion du capteur DHT22 à la carte Feather Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-to-your-computer"></a><span data-ttu-id="74a39-166">Connexion de la carte Feather M0 WiFi à votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="74a39-166">Connect Feather M0 WiFi to your computer</span></span>

<span data-ttu-id="74a39-167">Utilisez le câble Micro USB vers USB Type A pour connecter la carte Feather M0 WiFi à votre ordinateur, comme illustré ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="74a39-167">Use the Micro USB to Type A USB cable to connect Feather M0 WiFi to your computer, as shown:</span></span>

![Connexion de la carte Feather Huzzah à votre ordinateur](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="74a39-169">Ajouter des autorisations de port série (Ubuntu uniquement)</span><span class="sxs-lookup"><span data-stu-id="74a39-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="74a39-170">Si vous utilisez Ubuntu, assurez-vous que vous disposez des autorisations nécessaires pour utiliser le port USB de la carte Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="74a39-170">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="74a39-171">Pour ajouter des autorisations de port série, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74a39-171">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="74a39-172">Dans un terminal, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="74a39-172">At a terminal, run the following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="74a39-173">Vous obtenez l’une des sorties suivantes :</span><span class="sxs-lookup"><span data-stu-id="74a39-173">You get one of the following outputs:</span></span>

   * <span data-ttu-id="74a39-174">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="74a39-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="74a39-175">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="74a39-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="74a39-176">Dans la sortie, `uucp` ou `dialout` correspond au nom du propriétaire du groupe du port USB.</span><span class="sxs-lookup"><span data-stu-id="74a39-176">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

2. <span data-ttu-id="74a39-177">Pour ajouter l’utilisateur au groupe, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="74a39-177">To add the user to the group, run the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="74a39-178">À l’étape précédente, vous avez obtenu le nom du propriétaire du groupe `<group-owner-name>`.</span><span class="sxs-lookup"><span data-stu-id="74a39-178">In the previous step, you obtained the group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="74a39-179">Votre nom d’utilisateur Ubuntu est `<username>`.</span><span class="sxs-lookup"><span data-stu-id="74a39-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="74a39-180">Pour que la modification prenne effet, déconnectez-vous d’Ubuntu, puis reconnectez-vous.</span><span class="sxs-lookup"><span data-stu-id="74a39-180">For the change to appear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="74a39-181">Collecter les données du capteur et les envoyer à votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="74a39-181">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="74a39-182">Dans cette section, vous allez déployer et exécuter un exemple d’application sur la carte Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="74a39-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="74a39-183">L’exemple d’application fait clignoter la LED de la carte Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="74a39-183">The sample application makes the LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="74a39-184">Il envoie ensuite les données de température et d’humidité collectées à partir du capteur BME280 à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="74a39-184">It then sends the temperature and humidity data collected from the BME280 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github-and-prepare-the-arduino-ide"></a><span data-ttu-id="74a39-185">Obtenir l’exemple d’application à partir de GitHub et préparer l’IDE Arduino</span><span class="sxs-lookup"><span data-stu-id="74a39-185">Get the sample application from GitHub and prepare the Arduino IDE</span></span>

<span data-ttu-id="74a39-186">L’exemple d’application est hébergé sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="74a39-186">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="74a39-187">Clonez l’exemple de référentiel contenant l’exemple d’application à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="74a39-187">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="74a39-188">Pour cloner l’exemple de référentiel, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74a39-188">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="74a39-189">Ouvrez une invite de commandes ou une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="74a39-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="74a39-190">Accédez au dossier à utiliser pour le stockage de l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="74a39-190">Go to a folder where you want the sample application to be stored.</span></span>
3. <span data-ttu-id="74a39-191">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="74a39-191">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-the-package-for-feather-m0-wifi-in-the-arduino-ide"></a><span data-ttu-id="74a39-192">Installer le package pour la carte Feather M0 WiFi dans l’IDE Arduino</span><span class="sxs-lookup"><span data-stu-id="74a39-192">Install the package for Feather M0 WiFi in the Arduino IDE</span></span>

1. <span data-ttu-id="74a39-193">Ouvrez le dossier où l’exemple d’application est stocké.</span><span class="sxs-lookup"><span data-stu-id="74a39-193">Open the folder where the sample application is stored.</span></span>

2. <span data-ttu-id="74a39-194">Ouvrez le fichier app.ino dans le dossier app de l’IDE Arduino.</span><span class="sxs-lookup"><span data-stu-id="74a39-194">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![Ouverture de l’exemple d’application dans l’IDE Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="74a39-196">Cliquez sur **Fichier** > **Préférences** (Windows/Linux) ou sur **Arduino** > **Préférences** (Mac), puis copiez et collez le lien ci-dessous dans le champ de l’option **URL de gestionnaire de cartes supplémentaires**.</span><span class="sxs-lookup"><span data-stu-id="74a39-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste the link below into the **Additional Boards Manager URLs** option in the Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="74a39-197">Cliquez sur **Outils** > **Carte** > **Gestionnaire de cartes**, puis installez `Arduino SAMD Boards` version `1.6.2` ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="74a39-197">Click **Tools** > **Board** > **Boards Manager**, and then install the `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="74a39-198">Dans la même fenêtre, installez ensuite le package `Adafruit SAMD Boards` pour ajouter les définitions de fichier de carte.</span><span class="sxs-lookup"><span data-stu-id="74a39-198">Then in the same window, install `Adafruit SAMD Boards` package to add the board file definitions.</span></span>

   ![Le package ESP8266 est installé](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="74a39-200">Cliquez sur **Outils** > **Carte** > **Adafruit M0 WiFi**.</span><span class="sxs-lookup"><span data-stu-id="74a39-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="74a39-201">Installez les pilotes (pour Windows uniquement).</span><span class="sxs-lookup"><span data-stu-id="74a39-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="74a39-202">Lorsque vous branchez la carte M0 WiFi, il se peut que vous deviez installer un pilote.</span><span class="sxs-lookup"><span data-stu-id="74a39-202">When you plug in Feather M0 WiFi, you might need to install a driver.</span></span> <span data-ttu-id="74a39-203">Cliquez sur [ce lien](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) pour télécharger le programme d’installation des pilotes.</span><span class="sxs-lookup"><span data-stu-id="74a39-203">Click [the download link on the webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) to download the driver installer.</span></span> <span data-ttu-id="74a39-204">Suivez les étapes à l’écran pour installer les pilotes souhaités.</span><span class="sxs-lookup"><span data-stu-id="74a39-204">Follow the steps to install the drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="74a39-205">Installer les bibliothèques nécessaires</span><span class="sxs-lookup"><span data-stu-id="74a39-205">Install necessary libraries</span></span>

1. <span data-ttu-id="74a39-206">Dans l’IDE Arduino, cliquez sur **Croquis** > **Inclure une bibliothèque** > **Gérer les bibliothèques**.</span><span class="sxs-lookup"><span data-stu-id="74a39-206">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="74a39-207">Recherchez les noms de bibliothèque suivants un par un.</span><span class="sxs-lookup"><span data-stu-id="74a39-207">Search for the following library names one by one.</span></span> <span data-ttu-id="74a39-208">Pour chacune des bibliothèques trouvées, cliquez sur **Installer** :</span><span class="sxs-lookup"><span data-stu-id="74a39-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="74a39-209">Installez manuellement `Adafruit_WINC1500`.</span><span class="sxs-lookup"><span data-stu-id="74a39-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="74a39-210">Accédez à [ce site web](https://github.com/adafruit/Adafruit_WINC1500) et cliquez sur **Clone or download** (Cloner ou télécharger)  > **Download ZIP** (Télécharger ZIP).</span><span class="sxs-lookup"><span data-stu-id="74a39-210">Go to [this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="74a39-211">Ensuite, dans votre IDE Arduino, accédez à **Croquis** > **Inclure une bibliothèque** > **Ajouter la bibliothèque .ZIP** et ajoutez le fichier zip.</span><span class="sxs-lookup"><span data-stu-id="74a39-211">Then in your Arduino IDE, go to **Sketch** > **Include Library** > **Add .zip Library** and add the zip file.</span></span>

### <a name="use-the-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="74a39-212">Utiliser l’exemple d’application en l’absence de capteur BME280</span><span class="sxs-lookup"><span data-stu-id="74a39-212">Use the sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="74a39-213">Si vous n’avez pas de capteur BME280, l’exemple d’application permet de simuler des données de température et d’humidité.</span><span class="sxs-lookup"><span data-stu-id="74a39-213">If you don’t have a real BME280 sensor, the sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="74a39-214">Pour que l’exemple d’application utilise des données simulées, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74a39-214">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="74a39-215">Ouvrez le fichier `config.h` dans le dossier `app`.</span><span class="sxs-lookup"><span data-stu-id="74a39-215">Open the `config.h` file in the `app` folder.</span></span>

2. <span data-ttu-id="74a39-216">Recherchez la ligne de code suivante et remplacez la valeur `false` par `true` :</span><span class="sxs-lookup"><span data-stu-id="74a39-216">Locate the following line of code and change the value from `false` to `true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![Configuration de l’exemple d’application pour utiliser des données simulées](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="74a39-218">Enregistrez le fichier avec `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="74a39-218">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-m0-wifi"></a><span data-ttu-id="74a39-219">Déployer l’exemple d’application sur la carte M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="74a39-219">Deploy the sample application to Feather M0 WiFi</span></span>

1. <span data-ttu-id="74a39-220">Dans l’IDE Arduino, cliquez sur **Outil** > **Port**, puis cliquez sur le port série pour la carte Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="74a39-220">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="74a39-221">Cliquez sur **Croquis** > **Téléverser** pour générer et déployer l’exemple d’application sur la carte Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="74a39-221">Click **Sketch** > **Upload** to build and deploy the sample application to Feather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="74a39-222">Entrer vos informations d’identification</span><span class="sxs-lookup"><span data-stu-id="74a39-222">Enter your credentials</span></span>

<span data-ttu-id="74a39-223">Une fois le chargement terminé, suivez cette procédure pour entrer vos informations d’identification :</span><span class="sxs-lookup"><span data-stu-id="74a39-223">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="74a39-224">Dans l’IDE Arduino, cliquez sur **Outils** > **Moniteur série**.</span><span class="sxs-lookup"><span data-stu-id="74a39-224">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="74a39-225">Dans le coin inférieur droit de la fenêtre du moniteur série, sélectionnez **Pas de fin de ligne** dans la liste déroulante de gauche.</span><span class="sxs-lookup"><span data-stu-id="74a39-225">In the lower-right corner of the serial monitor window, select **No line ending** in the drop-down list on the left.</span></span>
3. <span data-ttu-id="74a39-226">Dans la liste déroulante de droite, sélectionnez **115200 baud**.</span><span class="sxs-lookup"><span data-stu-id="74a39-226">Select **115200 baud** in the drop-down list on the right.</span></span>
4. <span data-ttu-id="74a39-227">Dans la zone de saisie située en haut, entrez les informations suivantes si vous êtes invité à les fournir, puis cliquez sur **Envoyer** :</span><span class="sxs-lookup"><span data-stu-id="74a39-227">In the input box at the top, enter the following information if you're asked to provide it, and click **Send**:</span></span>

   * <span data-ttu-id="74a39-228">SSID Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="74a39-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="74a39-229">Mot de passe Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="74a39-229">Wi-Fi password</span></span>
   * <span data-ttu-id="74a39-230">Chaîne de connexion de l’appareil</span><span class="sxs-lookup"><span data-stu-id="74a39-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="74a39-231">Les informations d’identification sont stockées dans la mémoire EEPROM de la carte Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="74a39-231">The credential information is stored in the EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="74a39-232">Si vous cliquez sur le bouton de réinitialisation de la carte Feather M0 WiFi, l’exemple d’application vous demande si vous souhaitez effacer ces informations.</span><span class="sxs-lookup"><span data-stu-id="74a39-232">If you click the reset button on the Feather M0 WiFi board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="74a39-233">Entrez `Y` pour effacer les informations.</span><span class="sxs-lookup"><span data-stu-id="74a39-233">Enter `Y` to erase the information.</span></span> <span data-ttu-id="74a39-234">Vous êtes invité à fournir les informations une deuxième fois.</span><span class="sxs-lookup"><span data-stu-id="74a39-234">You're asked to provide the information a second time.</span></span>

### <a name="verify-that-the-sample-application-is-running-successfully"></a><span data-ttu-id="74a39-235">Vérifier que l’exemple d’application s’exécute correctement</span><span class="sxs-lookup"><span data-stu-id="74a39-235">Verify that the sample application is running successfully</span></span>

<span data-ttu-id="74a39-236">Si vous voyez la sortie suivante dans la fenêtre du moniteur série et la LED clignoter sur la carte Feather M0 WiFi, l’exemple d’application s’exécute correctement :</span><span class="sxs-lookup"><span data-stu-id="74a39-236">If you see the following output from the serial monitor window and the blinking LED on Feather M0 WiFi, the sample application is running successfully:</span></span>

![Sortie finale dans l’IDE Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="74a39-238">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="74a39-238">Next steps</span></span>

<span data-ttu-id="74a39-239">Vous avez correctement connecté la carte Feather M0 WiFi à votre IoT Hub et envoyé les données de capteur collectées à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="74a39-239">You have successfully connected Feather M0 WiFi to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

