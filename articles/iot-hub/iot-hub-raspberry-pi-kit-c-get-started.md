---
title: "Raspberry Pi vers cloud (C) - Connecter Raspberry Pi à Azure IoT Hub | Microsoft Docs"
description: "Dans ce didacticiel, découvrez comment configurer et connecter Raspberry Pi à Azure IoT Hub pour lui permettre d’envoyer des données à la plateforme cloud Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot raspberry pi, raspberry pi iot hub, raspberry pi envoie des données vers le cloud, raspberry pi vers cloud"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8b8fda17a8d1d1796d5299e3aba4b0fd5e719a4c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-c"></a><span data-ttu-id="4d6f2-104">Connecter Raspberry Pi à Azure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-104">Connect Raspberry Pi to Azure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="4d6f2-105">Dans ce didacticiel, vous commencez par découvrir les principes fondamentaux de l’utilisation de Raspberry Pi exécutant Raspbian.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="4d6f2-106">Vous apprenez ensuite à connecter en toute transparence vos appareils au cloud avec [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="4d6f2-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="4d6f2-107">Pour obtenir des exemples Windows 10 IoT Standard, accédez au [centre de développement Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="4d6f2-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="4d6f2-108">Vous n’avez pas encore de kit ?</span><span class="sxs-lookup"><span data-stu-id="4d6f2-108">Don't have a kit yet?</span></span> <span data-ttu-id="4d6f2-109">Essayez [le simulateur en ligne Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4d6f2-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="4d6f2-110">Ou achetez un nouveau kit [ici](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="4d6f2-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="4d6f2-111">Procédure</span><span class="sxs-lookup"><span data-stu-id="4d6f2-111">What you do</span></span>

* <span data-ttu-id="4d6f2-112">Créez un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-112">Create an IoT hub.</span></span>
* <span data-ttu-id="4d6f2-113">Inscrivez un appareil pour Pi dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="4d6f2-114">Configurez Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="4d6f2-115">Exécutez un exemple d’application sur Pi pour envoyer des données de capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="4d6f2-116">Connectez Raspberry Pi à un IoT Hub créé à cette fin.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="4d6f2-117">Exécutez ensuite un exemple d’application sur Pi pour collecter des données de température et d’humidité provenant d’un capteur BME280.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="4d6f2-118">Enfin, envoyez les données du capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="4d6f2-119">Contenu</span><span class="sxs-lookup"><span data-stu-id="4d6f2-119">What you learn</span></span>

* <span data-ttu-id="4d6f2-120">Création d’un Azure IoT Hub et obtention de la chaîne de connexion de votre nouvel appareil.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="4d6f2-121">Connexion de Pi à un capteur BME280.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="4d6f2-122">Collecte des données du capteur en exécutant un exemple d’application sur Pi.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="4d6f2-123">Envoi des données du capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4d6f2-124">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="4d6f2-124">What you need</span></span>

![Ce dont vous avez besoin](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="4d6f2-126">Une carte Raspberry Pi 2 ou Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="4d6f2-127">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-127">An active Azure subscription.</span></span> <span data-ttu-id="4d6f2-128">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="4d6f2-129">Un moniteur, un clavier USB et une souris qui se connectent à Pi.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="4d6f2-130">Un Mac ou un PC exécutant Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="4d6f2-131">Une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-131">An Internet connection.</span></span>
* <span data-ttu-id="4d6f2-132">Une carte microSD d’au moins 16 Go.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="4d6f2-133">Un adaptateur USB-SD ou une carte microSD pour graver l’image du système d’exploitation sur la carte microSD.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="4d6f2-134">Une alimentation 5 V 2 A avec le câble micro USB de 6 pieds (env. 183 cm).</span><span class="sxs-lookup"><span data-stu-id="4d6f2-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="4d6f2-135">Les éléments suivants sont facultatifs :</span><span class="sxs-lookup"><span data-stu-id="4d6f2-135">The following items are optional:</span></span>

* <span data-ttu-id="4d6f2-136">Un capteur de température, de pression et d’humidité Adafruit BME280 assemblé.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="4d6f2-137">Une platine d’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-137">A breadboard.</span></span>
* <span data-ttu-id="4d6f2-138">6 câbles de liaison F/M.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="4d6f2-139">Une LED de 10 mm diffuse.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="4d6f2-140">Ces éléments sont facultatifs, car l’exemple de code prend en charge les données de capteur simulées.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-140">These items are optional because the code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="4d6f2-141">Configuration de Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="4d6f2-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="4d6f2-142">Installation du système d’exploitation Raspbian pour Pi</span><span class="sxs-lookup"><span data-stu-id="4d6f2-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="4d6f2-143">Préparez la carte microSD pour l’installation de l’image Raspbian.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="4d6f2-144">Téléchargez Raspbian.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="4d6f2-145">[Téléchargez Raspbian Jessie avec Desktop](https://www.raspberrypi.org/downloads/raspbian/) (fichier .zip).</span><span class="sxs-lookup"><span data-stu-id="4d6f2-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="4d6f2-146">Extrayez l’image Raspbian dans un dossier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="4d6f2-147">Installez Raspbian sur la carte microSD.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="4d6f2-148">[Téléchargez et installez l’utilitaire de graveur de carte SD Etcher](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="4d6f2-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="4d6f2-149">Exécutez Etcher et sélectionnez l’image Raspbian extraite à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="4d6f2-150">Sélectionnez le lecteur de carte microSD.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-150">Select the microSD card drive.</span></span> <span data-ttu-id="4d6f2-151">Remarque : Etcher a peut-être déjà sélectionné le lecteur approprié.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="4d6f2-152">Cliquez sur Flash pour installer Raspbian sur la carte microSD.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="4d6f2-153">Retirez la carte microSD de votre ordinateur une fois l’installation terminée.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="4d6f2-154">Vous pouvez retirer directement la carte microSD en toute sécurité, car Etcher éjecte ou démonte automatiquement la carte microSD une fois le processus terminé.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="4d6f2-155">Insérez la carte microSD dans Pi.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-spi"></a><span data-ttu-id="4d6f2-156">Activer SSH et SPI</span><span class="sxs-lookup"><span data-stu-id="4d6f2-156">Enable SSH and SPI</span></span>

1. <span data-ttu-id="4d6f2-157">Connectez Pi au moniteur, au clavier et à la souris, démarrez Pi puis connectez-vous à Raspbian en utilisant `pi` comme nom d’utilisateur et `raspberry` comme mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="4d6f2-158">Cliquez sur l’icône Raspberry > **Préférences** > **Configuration de Raspberry Pi**.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Le menu Préférences de Raspbian](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="4d6f2-160">Sur l’onglet **Interfaces**, définissez **SPI** et **SSH** sur **Activer**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-160">On the **Interfaces** tab, set **SPI** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="4d6f2-161">Si vous n’avez pas de capteurs physiques et que vous souhaitez utiliser des données de capteur simulé, cette étape est facultative.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Activer SPI et SSH sur Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="4d6f2-163">Pour activer SSH et SPI, vous trouverez d’autres documents de référence sur [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) et [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="4d6f2-163">To enable SSH and SPI, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="4d6f2-164">Connecter le capteur à Pi</span><span class="sxs-lookup"><span data-stu-id="4d6f2-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="4d6f2-165">Utilisez la platine d’expérimentation et les câbles de liaison pour connecter une LED et un BME280 à Pi comme suit.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="4d6f2-166">Si vous ne disposez pas de ce capteur, [ignorez cette section](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="4d6f2-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![La connexion entre Raspberry Pi et le capteur](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="4d6f2-168">Le capteur BME280 peut collecter des données sur la température et l’humidité.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="4d6f2-169">Et la DEL clignote s’il existe une communication entre l’appareil et le cloud.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="4d6f2-170">Pour les broches du capteur, utilisez le câblage suivant :</span><span class="sxs-lookup"><span data-stu-id="4d6f2-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="4d6f2-171">Début (capteur et LED)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="4d6f2-172">Fin (carte)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-172">End (Board)</span></span>            | <span data-ttu-id="4d6f2-173">Couleur du câble</span><span class="sxs-lookup"><span data-stu-id="4d6f2-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="4d6f2-174">LED VDD (broche 5G)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-174">LED VDD (Pin 5G)</span></span>         | <span data-ttu-id="4d6f2-175">GPIO 4 (broche 7)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-175">GPIO 4 (Pin 7)</span></span>         | <span data-ttu-id="4d6f2-176">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="4d6f2-176">White cable</span></span>   |
| <span data-ttu-id="4d6f2-177">LED GND (broche 6G)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-177">LED GND (Pin 6G)</span></span>         | <span data-ttu-id="4d6f2-178">GND (broche 6)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-178">GND (Pin 6)</span></span>            | <span data-ttu-id="4d6f2-179">Câble noir</span><span class="sxs-lookup"><span data-stu-id="4d6f2-179">Black cable</span></span>   |
| <span data-ttu-id="4d6f2-180">VDD (broche 18F)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-180">VDD (Pin 18F)</span></span>            | <span data-ttu-id="4d6f2-181">ALIM 3,3V (broche 17)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-181">3.3V PWR (Pin 17)</span></span>      | <span data-ttu-id="4d6f2-182">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="4d6f2-182">White cable</span></span>   |
| <span data-ttu-id="4d6f2-183">GND (broche 20F)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-183">GND (Pin 20F)</span></span>            | <span data-ttu-id="4d6f2-184">GND (broche 20)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-184">GND (Pin 20)</span></span>           | <span data-ttu-id="4d6f2-185">Câble noir</span><span class="sxs-lookup"><span data-stu-id="4d6f2-185">Black cable</span></span>   |
| <span data-ttu-id="4d6f2-186">SCK (broche 21F)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-186">SCK (Pin 21F)</span></span>            | <span data-ttu-id="4d6f2-187">SPI0 SCLK (broche 23)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-187">SPI0 SCLK (Pin 23)</span></span>     | <span data-ttu-id="4d6f2-188">Câble orange</span><span class="sxs-lookup"><span data-stu-id="4d6f2-188">Orange cable</span></span>  |
| <span data-ttu-id="4d6f2-189">SDO (broche 22F)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-189">SDO (Pin 22F)</span></span>            | <span data-ttu-id="4d6f2-190">SPI0 MISO (broche 21)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-190">SPI0 MISO (Pin 21)</span></span>     | <span data-ttu-id="4d6f2-191">Câble jaune</span><span class="sxs-lookup"><span data-stu-id="4d6f2-191">Yellow cable</span></span>  |
| <span data-ttu-id="4d6f2-192">SDI (broche 23F)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-192">SDI (Pin 23F)</span></span>            | <span data-ttu-id="4d6f2-193">SPI0 MOSI (broche 19)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-193">SPI0 MOSI (Pin 19)</span></span>     | <span data-ttu-id="4d6f2-194">Câble vert</span><span class="sxs-lookup"><span data-stu-id="4d6f2-194">Green cable</span></span>   |
| <span data-ttu-id="4d6f2-195">CS (broche 24F)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-195">CS (Pin 24F)</span></span>             | <span data-ttu-id="4d6f2-196">SPI0 CS (broche 24)</span><span class="sxs-lookup"><span data-stu-id="4d6f2-196">SPI0 CS (Pin 24)</span></span>       | <span data-ttu-id="4d6f2-197">Câble bleu</span><span class="sxs-lookup"><span data-stu-id="4d6f2-197">Blue cable</span></span>    |

<span data-ttu-id="4d6f2-198">Cliquez pour afficher les [mappages de broches de Raspberry Pi 2 et 3](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) à titre de référence.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-198">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="4d6f2-199">Une fois le BME280 connecté à votre Raspberry Pi, il doit se présenter comme sur l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-199">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Pi et BME280 connectés](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="4d6f2-201">Connexion de Pi au réseau</span><span class="sxs-lookup"><span data-stu-id="4d6f2-201">Connect Pi to the network</span></span>

<span data-ttu-id="4d6f2-202">Mettez Pi sous tension à l’aide du câble micro USB et de l’alimentation.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-202">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="4d6f2-203">Utilisez le câble Ethernet pour connecter Pi à votre réseau câblé ou suivez les [instructions fournies par la Fondation Raspberry Pi](https://www.raspberrypi.org/learning/software-guide/wifi/) pour connecter Pi à votre réseau sans fil.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-203">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="4d6f2-204">Une fois que votre Pi est correctement connecté au réseau, vous devez relever son [adresse IP](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="4d6f2-204">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Connecté au réseau câblé](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="4d6f2-206">Exécuter un exemple d’application sur Pi</span><span class="sxs-lookup"><span data-stu-id="4d6f2-206">Run a sample application on Pi</span></span>

### <a name="install-the-prerequisite-packages"></a><span data-ttu-id="4d6f2-207">Installer les packages requis</span><span class="sxs-lookup"><span data-stu-id="4d6f2-207">Install the prerequisite packages</span></span>

1. <span data-ttu-id="4d6f2-208">Utilisez l’un des clients SSH suivants à partir de votre ordinateur hôte pour vous connecter à votre Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-208">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="4d6f2-209">**Utilisateurs Windows**</span><span class="sxs-lookup"><span data-stu-id="4d6f2-209">**Windows Users**</span></span>
   1. <span data-ttu-id="4d6f2-210">Téléchargez et installez [PuTTY](http://www.putty.org/) pour Windows.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-210">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="4d6f2-211">Copiez l’adresse IP de votre Pi dans la section du nom d’hôte (ou adresse IP) et sélectionnez le type de connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-211">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="4d6f2-213">**Utilisateurs Mac et Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="4d6f2-213">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="4d6f2-214">Utilisez le client SSH intégré sur Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-214">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="4d6f2-215">Vous devrez peut-être exécuter `ssh pi@<ip address of pi>` pour connecter le Pi via le protocole SSH.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-215">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="4d6f2-216">Le nom d’utilisateur par défaut est `pi` et le mot de passe est `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-216">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="4d6f2-217">Installez les packages requis pour le Microsoft Azure IoT Device SDK pour C et Cmake en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d6f2-217">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C and Cmake by running the following commands:</span></span>

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake libcurl4-openssl-dev git-core
   git clone git://git.drogon.net/wiringPi
   cd ./wiringPi
   ./build
   ```


### <a name="configure-the-sample-application"></a><span data-ttu-id="4d6f2-218">Configurer l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="4d6f2-218">Configure the sample application</span></span>

1. <span data-ttu-id="4d6f2-219">Clonez l’exemple d’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4d6f2-219">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. <span data-ttu-id="4d6f2-220">Ouvrez le fichier de configuration en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d6f2-220">Open the config file by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Fichier de configuration](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   <span data-ttu-id="4d6f2-222">Deux éléments de type macros peuvent être configurés dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="4d6f2-223">Le premier est `INTERVAL`, qui définit le délai (en millisecondes) entre deux messages envoyés au cloud.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-223">The first one is `INTERVAL`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="4d6f2-224">Le deuxième est `SIMULATED_DATA`, qui est une valeur booléenne pour l’utilisation ou non des données de capteur simulées.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-224">The second one `SIMULATED_DATA`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="4d6f2-225">Si vous **ne disposez pas du capteur**, définissez la valeur `SIMULATED_DATA` sur `1` pour que l’exemple d’application crée et utilise des données de capteur simulées.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-225">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `1` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="4d6f2-226">Enregistrez et quittez en appuyant sur Ctrl-O > Entrée > Ctrl-X.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="4d6f2-227">Générer et exécuter l'exemple d’application</span><span class="sxs-lookup"><span data-stu-id="4d6f2-227">Build and run the sample application</span></span>

1. <span data-ttu-id="4d6f2-228">Générez l’exemple d’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4d6f2-228">Build the sample application by running the following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Sortie de la génération](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. <span data-ttu-id="4d6f2-230">Exécutez l’exemple d’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4d6f2-230">Run the sample application by running the following command:</span></span>

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="4d6f2-231">Assurez-vous de copier-coller la chaîne de connexion de l’appareil entre les guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-231">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="4d6f2-232">Vous devriez voir le résultat suivant, qui affiche les données de capteur et les messages envoyés à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-232">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Sortie - données de capteur envoyées depuis Raspberry Pi vers votre IoT Hub](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="4d6f2-234">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d6f2-234">Next steps</span></span>

<span data-ttu-id="4d6f2-235">Vous avez exécuté un exemple d’application pour collecter des données de capteur et les envoyer à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d6f2-235">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="4d6f2-236">Pour voir les messages envoyés par Raspberry Pi à votre IoT Hub ou pour envoyer des messages à votre Raspberry Pi depuis une interface de ligne de commande, consultez le [tutoriel Gérer une messagerie cloud vers appareil avec l’explorateur IoT hub](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="4d6f2-236">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
