---
title: "Raspberry Pi to cloud (Python) - Connecter Raspberry Pi à Azure IoT Hub | Microsoft Docs"
description: "Dans ce didacticiel, découvrez comment configurer et connecter Raspberry Pi à Azure IoT Hub pour lui permettre d’envoyer des données à la plateforme cloud Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot raspberry pi, raspberry pi iot hub, raspberry pi envoie des données vers le cloud, raspberry pi vers cloud"
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 1b1a9dc960846cbc15ce09d0fd106e1492937439
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-python"></a><span data-ttu-id="10645-104">Connecter Raspberry Pi à Azure IoT Hub (Python)</span><span class="sxs-lookup"><span data-stu-id="10645-104">Connect Raspberry Pi to Azure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="10645-105">Dans ce didacticiel, vous commencez par découvrir les principes fondamentaux de l’utilisation de Raspberry Pi exécutant Raspbian.</span><span class="sxs-lookup"><span data-stu-id="10645-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="10645-106">Vous apprenez ensuite à connecter en toute transparence vos appareils au cloud avec [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="10645-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="10645-107">Pour obtenir des exemples Windows 10 IoT Standard, accédez au [centre de développement Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="10645-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="10645-108">Vous n’avez pas encore de kit ?</span><span class="sxs-lookup"><span data-stu-id="10645-108">Don't have a kit yet?</span></span> <span data-ttu-id="10645-109">Essayez [le simulateur en ligne Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="10645-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="10645-110">Ou achetez un nouveau kit [ici](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="10645-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="10645-111">Procédure</span><span class="sxs-lookup"><span data-stu-id="10645-111">What you do</span></span>

* <span data-ttu-id="10645-112">Créez un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="10645-112">Create an IoT hub.</span></span>
* <span data-ttu-id="10645-113">Inscrivez un appareil pour Pi dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="10645-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="10645-114">Configurez Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="10645-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="10645-115">Exécutez un exemple d’application sur Pi pour envoyer des données de capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="10645-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="10645-116">Connectez Raspberry Pi à un IoT Hub créé à cette fin.</span><span class="sxs-lookup"><span data-stu-id="10645-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="10645-117">Exécutez ensuite un exemple d’application sur Pi pour collecter des données de température et d’humidité provenant d’un capteur BME280.</span><span class="sxs-lookup"><span data-stu-id="10645-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="10645-118">Enfin, envoyez les données du capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="10645-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="10645-119">Contenu</span><span class="sxs-lookup"><span data-stu-id="10645-119">What you learn</span></span>

* <span data-ttu-id="10645-120">Création d’un Azure IoT Hub et obtention de la chaîne de connexion de votre nouvel appareil.</span><span class="sxs-lookup"><span data-stu-id="10645-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="10645-121">Connexion de Pi à un capteur BME280.</span><span class="sxs-lookup"><span data-stu-id="10645-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="10645-122">Collecte des données du capteur en exécutant un exemple d’application sur Pi.</span><span class="sxs-lookup"><span data-stu-id="10645-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="10645-123">Envoi des données du capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="10645-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="10645-124">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="10645-124">What you need</span></span>

![Ce dont vous avez besoin](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="10645-126">Une carte Raspberry Pi 2 ou Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="10645-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="10645-127">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="10645-127">An active Azure subscription.</span></span> <span data-ttu-id="10645-128">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="10645-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="10645-129">Un moniteur, un clavier USB et une souris qui se connectent à Pi.</span><span class="sxs-lookup"><span data-stu-id="10645-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="10645-130">Un Mac ou un PC exécutant Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="10645-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="10645-131">Une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="10645-131">An Internet connection.</span></span>
* <span data-ttu-id="10645-132">Une carte microSD d’au moins 16 Go.</span><span class="sxs-lookup"><span data-stu-id="10645-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="10645-133">Un adaptateur USB-SD ou une carte microSD pour graver l’image du système d’exploitation sur la carte microSD.</span><span class="sxs-lookup"><span data-stu-id="10645-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="10645-134">Une alimentation 5 V 2 A avec le câble micro USB de 6 pieds (env. 183 cm).</span><span class="sxs-lookup"><span data-stu-id="10645-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="10645-135">Les éléments suivants sont facultatifs :</span><span class="sxs-lookup"><span data-stu-id="10645-135">The following items are optional:</span></span>

* <span data-ttu-id="10645-136">Un capteur de température, de pression et d’humidité Adafruit BME280 assemblé.</span><span class="sxs-lookup"><span data-stu-id="10645-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="10645-137">Une platine d’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="10645-137">A breadboard.</span></span>
* <span data-ttu-id="10645-138">6 câbles de liaison F/M.</span><span class="sxs-lookup"><span data-stu-id="10645-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="10645-139">Une LED de 10 mm diffuse.</span><span class="sxs-lookup"><span data-stu-id="10645-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="10645-140">Ces éléments sont facultatifs, car l’exemple de code prend en charge les données de capteur simulées.</span><span class="sxs-lookup"><span data-stu-id="10645-140">These items are optional because the code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="10645-141">Installer Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="10645-141">Set up Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="10645-142">Installation du système d’exploitation Raspbian pour Pi</span><span class="sxs-lookup"><span data-stu-id="10645-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="10645-143">Préparez la carte microSD pour l’installation de l’image Raspbian.</span><span class="sxs-lookup"><span data-stu-id="10645-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="10645-144">Téléchargez Raspbian.</span><span class="sxs-lookup"><span data-stu-id="10645-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="10645-145">[Téléchargez Raspbian Jessie avec Desktop](https://www.raspberrypi.org/downloads/raspbian/) (fichier .zip).</span><span class="sxs-lookup"><span data-stu-id="10645-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="10645-146">Extrayez l’image Raspbian dans un dossier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="10645-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="10645-147">Installez Raspbian sur la carte microSD.</span><span class="sxs-lookup"><span data-stu-id="10645-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="10645-148">[Téléchargez et installez l’utilitaire de graveur de carte SD Etcher](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="10645-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="10645-149">Exécutez Etcher et sélectionnez l’image Raspbian extraite à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="10645-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="10645-150">Sélectionnez le lecteur de carte microSD.</span><span class="sxs-lookup"><span data-stu-id="10645-150">Select the microSD card drive.</span></span> <span data-ttu-id="10645-151">Remarque : Etcher a peut-être déjà sélectionné le lecteur approprié.</span><span class="sxs-lookup"><span data-stu-id="10645-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="10645-152">Cliquez sur Flash pour installer Raspbian sur la carte microSD.</span><span class="sxs-lookup"><span data-stu-id="10645-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="10645-153">Retirez la carte microSD de votre ordinateur une fois l’installation terminée.</span><span class="sxs-lookup"><span data-stu-id="10645-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="10645-154">Vous pouvez retirer directement la carte microSD en toute sécurité, car Etcher éjecte ou démonte automatiquement la carte microSD une fois le processus terminé.</span><span class="sxs-lookup"><span data-stu-id="10645-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="10645-155">Insérez la carte microSD dans Pi.</span><span class="sxs-lookup"><span data-stu-id="10645-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="10645-156">Activer SSH et I2C</span><span class="sxs-lookup"><span data-stu-id="10645-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="10645-157">Connectez Pi au moniteur, au clavier et à la souris, démarrez Pi puis connectez-vous à Raspbian en utilisant `pi` comme nom d’utilisateur et `raspberry` comme mot de passe.</span><span class="sxs-lookup"><span data-stu-id="10645-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="10645-158">Cliquez sur l’icône Raspberry > **Préférences** > **Configuration de Raspberry Pi**.</span><span class="sxs-lookup"><span data-stu-id="10645-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Le menu Préférences de Raspbian](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="10645-160">Sur l’onglet **Interfaces**, définissez **I2C** et **SSH** sur **Activer**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="10645-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="10645-161">Si vous ne possédez pas de capteurs physiques et que vous souhaitez utiliser des données de capteur simulé, cette étape est facultative.</span><span class="sxs-lookup"><span data-stu-id="10645-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Activer I2C et SSH sur Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="10645-163">Pour activer SSH et I2C, vous trouverez d’autres documents de référence sur [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) et [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="10645-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="10645-164">Connecter le capteur à Pi</span><span class="sxs-lookup"><span data-stu-id="10645-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="10645-165">Utilisez la platine d’expérimentation et les câbles de liaison pour connecter une LED et un BME280 à Pi comme suit.</span><span class="sxs-lookup"><span data-stu-id="10645-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="10645-166">Si vous ne disposez pas de ce capteur, [ignorez cette section](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="10645-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![La connexion entre Raspberry Pi et le capteur](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="10645-168">Le capteur BME280 peut collecter des données sur la température et l’humidité.</span><span class="sxs-lookup"><span data-stu-id="10645-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="10645-169">Et la DEL clignote s’il existe une communication entre l’appareil et le cloud.</span><span class="sxs-lookup"><span data-stu-id="10645-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="10645-170">Pour les broches du capteur, utilisez le câblage suivant :</span><span class="sxs-lookup"><span data-stu-id="10645-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="10645-171">Début (capteur et LED)</span><span class="sxs-lookup"><span data-stu-id="10645-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="10645-172">Fin (carte)</span><span class="sxs-lookup"><span data-stu-id="10645-172">End (Board)</span></span>            | <span data-ttu-id="10645-173">Couleur du câble</span><span class="sxs-lookup"><span data-stu-id="10645-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="10645-174">VDD (broche 5G)</span><span class="sxs-lookup"><span data-stu-id="10645-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="10645-175">ALIM 3,3 V (broche 1)</span><span class="sxs-lookup"><span data-stu-id="10645-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="10645-176">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="10645-176">White cable</span></span>   |
| <span data-ttu-id="10645-177">GND (broche 7G)</span><span class="sxs-lookup"><span data-stu-id="10645-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="10645-178">GND (broche 6)</span><span class="sxs-lookup"><span data-stu-id="10645-178">GND (Pin 6)</span></span>            | <span data-ttu-id="10645-179">Câble marron</span><span class="sxs-lookup"><span data-stu-id="10645-179">Brown cable</span></span>   |
| <span data-ttu-id="10645-180">SDI (broche 10G)</span><span class="sxs-lookup"><span data-stu-id="10645-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="10645-181">I2C1 SDA (broche 3)</span><span class="sxs-lookup"><span data-stu-id="10645-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="10645-182">Câble rouge</span><span class="sxs-lookup"><span data-stu-id="10645-182">Red cable</span></span>     |
| <span data-ttu-id="10645-183">SCK (broche 8G)</span><span class="sxs-lookup"><span data-stu-id="10645-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="10645-184">I2C1 SCL (broche 5)</span><span class="sxs-lookup"><span data-stu-id="10645-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="10645-185">Câble orange</span><span class="sxs-lookup"><span data-stu-id="10645-185">Orange cable</span></span>  |
| <span data-ttu-id="10645-186">LED VDD (broche 18F)</span><span class="sxs-lookup"><span data-stu-id="10645-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="10645-187">GPIO 24 (broche 18)</span><span class="sxs-lookup"><span data-stu-id="10645-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="10645-188">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="10645-188">White cable</span></span>   |
| <span data-ttu-id="10645-189">LED GND (broche 17F)</span><span class="sxs-lookup"><span data-stu-id="10645-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="10645-190">GND (broche 20)</span><span class="sxs-lookup"><span data-stu-id="10645-190">GND (Pin 20)</span></span>           | <span data-ttu-id="10645-191">Câble noir</span><span class="sxs-lookup"><span data-stu-id="10645-191">Black cable</span></span>   |

<span data-ttu-id="10645-192">Cliquez pour afficher les [mappages de broches de Raspberry Pi 2 et 3](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) à titre de référence.</span><span class="sxs-lookup"><span data-stu-id="10645-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="10645-193">Une fois le BME280 connecté à votre Raspberry Pi, il doit se présenter comme sur l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="10645-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Pi et BME280 connectés](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="10645-195">Connexion de Pi au réseau</span><span class="sxs-lookup"><span data-stu-id="10645-195">Connect Pi to the network</span></span>

<span data-ttu-id="10645-196">Mettez Pi sous tension à l’aide du câble micro USB et de l’alimentation.</span><span class="sxs-lookup"><span data-stu-id="10645-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="10645-197">Utilisez le câble Ethernet pour connecter Pi à votre réseau câblé ou suivez les [instructions fournies par la Fondation Raspberry Pi](https://www.raspberrypi.org/learning/software-guide/wifi/) pour connecter Pi à votre réseau sans fil.</span><span class="sxs-lookup"><span data-stu-id="10645-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="10645-198">Une fois que votre Pi est correctement connecté au réseau, vous devez relever son [adresse IP](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="10645-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Connecté au réseau câblé](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="10645-200">Assurez-vous que Pi est connecté au même réseau que votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="10645-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="10645-201">Par exemple, si votre ordinateur est connecté à un réseau sans fil alors que Pi est connecté à un réseau câblé, il se peut que vous ne voyiez pas l’adresse IP dans la sortie devdisco.</span><span class="sxs-lookup"><span data-stu-id="10645-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="10645-202">Exécuter un exemple d’application sur Pi</span><span class="sxs-lookup"><span data-stu-id="10645-202">Run a sample application on Pi</span></span>

### <a name="install-the-prerequisite-packages"></a><span data-ttu-id="10645-203">Installer les packages requis</span><span class="sxs-lookup"><span data-stu-id="10645-203">Install the prerequisite packages</span></span>

<span data-ttu-id="10645-204">Utilisez l’un des clients SSH suivants à partir de votre ordinateur hôte pour vous connecter à votre Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="10645-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="10645-205">**Utilisateurs Windows**</span><span class="sxs-lookup"><span data-stu-id="10645-205">**Windows Users**</span></span>
   1. <span data-ttu-id="10645-206">Téléchargez et installez [PuTTY](http://www.putty.org/) pour Windows.</span><span class="sxs-lookup"><span data-stu-id="10645-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="10645-207">Copiez l’adresse IP de votre Pi dans la section du nom d’hôte (ou adresse IP) et sélectionnez SSH en tant que type de connexion.</span><span class="sxs-lookup"><span data-stu-id="10645-207">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   
   <span data-ttu-id="10645-208">**Utilisateurs Mac et Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="10645-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="10645-209">Utilisez le client SSH intégré sur Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="10645-209">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="10645-210">Vous devrez peut-être exécuter `ssh pi@<ip address of pi>` pour connecter le Pi via le protocole SSH.</span><span class="sxs-lookup"><span data-stu-id="10645-210">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="10645-211">Le nom d’utilisateur par défaut est `pi` et le mot de passe est `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="10645-211">The default username is `pi` , and the password is `raspberry`.</span></span>


### <a name="configure-the-sample-application"></a><span data-ttu-id="10645-212">Configurer l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="10645-212">Configure the sample application</span></span>

1. <span data-ttu-id="10645-213">Clonez l’exemple d’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="10645-213">Clone the sample application by running the following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="10645-214">Ouvrez le fichier de configuration en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="10645-214">Open the config file by running the following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="10645-215">Ce fichier contient 5 macros configurables.</span><span class="sxs-lookup"><span data-stu-id="10645-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="10645-216">Le premier est `MESSAGE_TIMESPAN`, qui définit le délai (en millisecondes) entre deux messages envoyés au cloud.</span><span class="sxs-lookup"><span data-stu-id="10645-216">The first one is `MESSAGE_TIMESPAN`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="10645-217">Le deuxième est `SIMULATED_DATA`, qui est une valeur booléenne pour l’utilisation ou non des données de capteur simulées.</span><span class="sxs-lookup"><span data-stu-id="10645-217">The second one `SIMULATED_DATA`, which is a Boolean value for whether to use simulated sensor data or not.</span></span> <span data-ttu-id="10645-218">`I2C_ADDRESS`est l’adresse I2C à laquelle votre capteur BME280 est connecté.</span><span class="sxs-lookup"><span data-stu-id="10645-218">`I2C_ADDRESS` is the I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="10645-219">`GPIO_PIN_ADDRESS`est l’adresse GPIO pour votre LED.</span><span class="sxs-lookup"><span data-stu-id="10645-219">`GPIO_PIN_ADDRESS` is the GPIO address for your LED.</span></span> <span data-ttu-id="10645-220">Enfin, `BLINK_TIMESPAN` définit l’intervalle de temps lors de l’activation de votre LED en millisecondes.</span><span class="sxs-lookup"><span data-stu-id="10645-220">The last one is `BLINK_TIMESPAN`, which defined the timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="10645-221">Si vous **ne disposez pas du capteur**, définissez la valeur `SIMULATED_DATA` sur `True` pour que l’exemple d’application crée et utilise des données de capteur simulées.</span><span class="sxs-lookup"><span data-stu-id="10645-221">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `True` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="10645-222">Enregistrez et quittez en appuyant sur Ctrl-O > Entrée > Ctrl-X.</span><span class="sxs-lookup"><span data-stu-id="10645-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="10645-223">Générer et exécuter l'exemple d’application</span><span class="sxs-lookup"><span data-stu-id="10645-223">Build and run the sample application</span></span>

1. <span data-ttu-id="10645-224">Générez l’exemple d’application en exécutant la commande ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="10645-224">Build the sample application by running the following command.</span></span> <span data-ttu-id="10645-225">Étant donné que les Kits de développement logiciel (SDK) Azure IoT pour Python sont des wrappers placés sur des Kits de développement logiciel (SDK) Azure IoT Device C, vous devez compiler les bibliothèques C si vous voulez ou devez générer les bibliothèques Python à partir du code source.</span><span class="sxs-lookup"><span data-stu-id="10645-225">Because the Azure IoT SDKs for Python are wrappers on top of the Azure IoT Device C SDK, you will need to compile the C libraries if you want or need to generate the Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="10645-226">Vous pouvez également spécifier la version souhaitée en exécutant `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span><span class="sxs-lookup"><span data-stu-id="10645-226">You can also specify the version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="10645-227">Si vous exécutez le script sans paramètre, il détecte automatiquement la version de python installée (séquence de recherche 2.7 -> 3.4 -> 3.5).</span><span class="sxs-lookup"><span data-stu-id="10645-227">If you run script without parameter, the script will automatically detect the version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="10645-228">Assurez-vous de la cohérence de votre version de Python pendant la création et l’exécution.</span><span class="sxs-lookup"><span data-stu-id="10645-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="10645-229">Lors de la création de la bibliothèque cliente de Python (iothub_client.so) sur des appareils Linux disposant de moins de 1 Go de RAM, vous pouvez assister à un blocage à 98 % pendant la génération de iothub_client_python.cpp comme indiqué ci-dessous `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span><span class="sxs-lookup"><span data-stu-id="10645-229">On building the Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="10645-230">Si vous rencontrez ce problème, vérifiez la consommation de mémoire de l’appareil en utilisant `free -m command` dans une autre fenêtre de terminal pendant ce temps.</span><span class="sxs-lookup"><span data-stu-id="10645-230">If you run into this issue, check the memory consumption of the device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="10645-231">Si l’espace mémoire est insuffisant lors de la compilation du fichier iothub_client_python.cpp, vous devez augmenter temporairement l’espace d’échange pour libérer plus d’espace dans la mémoire afin de générer la bibliothèque de Kits de développement logiciel (SDK) Python de l’appareil côté client.</span><span class="sxs-lookup"><span data-stu-id="10645-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have to temporarily increase the swap space to get more available memory to successfully build the Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="10645-232">Exécutez l’exemple d’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="10645-232">Run the sample application by running the following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="10645-233">Assurez-vous de copier-coller la chaîne de connexion de l’appareil entre les guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="10645-233">Make sure you copy-paste the device connection string into the single quotes.</span></span> <span data-ttu-id="10645-234">Et si vous utilisez python 3, vous pouvez utiliser la commande `python3 app.py '<your Azure IoT hub device connection string>'`.</span><span class="sxs-lookup"><span data-stu-id="10645-234">And if you use the python 3, then you can use the command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="10645-235">Vous devriez voir le résultat suivant, qui affiche les données de capteur et les messages envoyés à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="10645-235">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

   ![Sortie - données de capteur envoyées depuis Raspberry Pi vers votre IoT Hub](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="10645-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="10645-237">Next steps</span></span>

<span data-ttu-id="10645-238">Vous avez exécuté un exemple d’application pour collecter des données de capteur et les envoyer à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="10645-238">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="10645-239">Pour voir les messages envoyés par Raspberry Pi à votre IoT Hub ou pour envoyer des messages à votre Raspberry Pi depuis une interface de ligne de commande, consultez le [tutoriel Gérer une messagerie cloud vers appareil avec l’explorateur IoT hub](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="10645-239">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
