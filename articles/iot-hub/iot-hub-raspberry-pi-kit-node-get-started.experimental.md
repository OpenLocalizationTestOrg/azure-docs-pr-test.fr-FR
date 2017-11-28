---
title: "Raspberry Pi vers cloud (Node.js) – Connecter Raspberry Pi à Azure IoT Hub | Microsoft Docs"
description: "Connectez Raspberry Pi à Azure IoT Hub pour que Raspberry Pi puisse envoyer des données vers le cloud Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot raspberry pi, raspberry pi iot hub, raspberry pi envoie des données vers le cloud, raspberry pi vers cloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 956ed5ab0ed38ddebd978b35eb54bc96567f0d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a><span data-ttu-id="cf78e-104">Connecter Raspberry Pi à Azure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="cf78e-104">Connect Raspberry Pi to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="cf78e-105">Dans ce didacticiel, vous commencez par découvrir les principes fondamentaux de l’utilisation de Raspberry Pi exécutant Raspbian.</span><span class="sxs-lookup"><span data-stu-id="cf78e-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="cf78e-106">Vous apprenez ensuite à connecter en toute transparence vos appareils au cloud avec [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="cf78e-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="cf78e-107">Pour obtenir des exemples Windows 10 IoT Standard, accédez au [centre de développement Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="cf78e-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="cf78e-108">Vous n’avez pas encore de kit ?</span><span class="sxs-lookup"><span data-stu-id="cf78e-108">Don't have a kit yet?</span></span> <span data-ttu-id="cf78e-109">Essayez l’[émulateur Raspberry Pi 3](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span><span class="sxs-lookup"><span data-stu-id="cf78e-109">Try the [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span></span> <span data-ttu-id="cf78e-110">Ou achetez un nouveau kit [ici](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="cf78e-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="cf78e-111">Procédure</span><span class="sxs-lookup"><span data-stu-id="cf78e-111">What you do</span></span>

* <span data-ttu-id="cf78e-112">Configurez Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="cf78e-112">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="cf78e-113">Créez un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cf78e-113">Create an IoT hub.</span></span>
* <span data-ttu-id="cf78e-114">Inscrivez un appareil pour Pi dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cf78e-114">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="cf78e-115">Exécutez un exemple d’application sur Pi pour envoyer des données de capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cf78e-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="cf78e-116">Connectez Raspberry Pi à un IoT Hub créé à cette fin.</span><span class="sxs-lookup"><span data-stu-id="cf78e-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="cf78e-117">Exécutez ensuite un exemple d’application sur Pi pour collecter des données de température et d’humidité provenant d’un capteur BME280.</span><span class="sxs-lookup"><span data-stu-id="cf78e-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="cf78e-118">Enfin, envoyez les données du capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cf78e-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="cf78e-119">Contenu</span><span class="sxs-lookup"><span data-stu-id="cf78e-119">What you learn</span></span>

* <span data-ttu-id="cf78e-120">Création d’un Azure IoT Hub et obtention de la chaîne de connexion de votre nouvel appareil.</span><span class="sxs-lookup"><span data-stu-id="cf78e-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="cf78e-121">Connexion de Pi à un capteur BME280.</span><span class="sxs-lookup"><span data-stu-id="cf78e-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="cf78e-122">Collecte des données du capteur en exécutant un exemple d’application sur Pi.</span><span class="sxs-lookup"><span data-stu-id="cf78e-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="cf78e-123">Envoi des données du capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cf78e-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cf78e-124">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="cf78e-124">What you need</span></span>

![Ce dont vous avez besoin](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="cf78e-126">Une carte Raspberry Pi 2 ou Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="cf78e-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="cf78e-127">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="cf78e-127">An active Azure subscription.</span></span> <span data-ttu-id="cf78e-128">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="cf78e-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="cf78e-129">Un moniteur, un clavier USB et une souris qui se connectent à Pi.</span><span class="sxs-lookup"><span data-stu-id="cf78e-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="cf78e-130">Un Mac ou un PC exécutant Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="cf78e-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="cf78e-131">Une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="cf78e-131">An Internet connection.</span></span>
* <span data-ttu-id="cf78e-132">Une carte microSD d’au moins 16 Go.</span><span class="sxs-lookup"><span data-stu-id="cf78e-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="cf78e-133">Un adaptateur USB-SD ou une carte microSD pour graver l’image du système d’exploitation sur la carte microSD.</span><span class="sxs-lookup"><span data-stu-id="cf78e-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="cf78e-134">Une alimentation 5 V 2 A avec le câble micro USB de 6 pieds (env. 183 cm).</span><span class="sxs-lookup"><span data-stu-id="cf78e-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="cf78e-135">Les éléments suivants sont facultatifs :</span><span class="sxs-lookup"><span data-stu-id="cf78e-135">The following items are optional:</span></span>

* <span data-ttu-id="cf78e-136">Un capteur de température, de pression et d’humidité Adafruit BME280 assemblé.</span><span class="sxs-lookup"><span data-stu-id="cf78e-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="cf78e-137">Une platine d’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="cf78e-137">A breadboard.</span></span>
* <span data-ttu-id="cf78e-138">6 câbles de liaison F/M.</span><span class="sxs-lookup"><span data-stu-id="cf78e-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="cf78e-139">Une LED de 10 mm diffuse.</span><span class="sxs-lookup"><span data-stu-id="cf78e-139">A diffused 10-mm LED.</span></span>

  > [!NOTE] 
  <span data-ttu-id="cf78e-140">Ces éléments sont facultatifs, car l’exemple de code prend en charge les données de capteur simulées.</span><span class="sxs-lookup"><span data-stu-id="cf78e-140">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="cf78e-141">Configuration de Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="cf78e-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="cf78e-142">Installation du système d’exploitation Raspbian pour Pi</span><span class="sxs-lookup"><span data-stu-id="cf78e-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="cf78e-143">Préparez la carte microSD pour l’installation de l’image Raspbian.</span><span class="sxs-lookup"><span data-stu-id="cf78e-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="cf78e-144">Téléchargez Raspbian.</span><span class="sxs-lookup"><span data-stu-id="cf78e-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="cf78e-145">[Téléchargez Raspbian Jessie avec Pixel](https://www.raspberrypi.org/downloads/raspbian/) (fichier .zip).</span><span class="sxs-lookup"><span data-stu-id="cf78e-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="cf78e-146">Extrayez l’image Raspbian dans un dossier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cf78e-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="cf78e-147">Installez Raspbian sur la carte microSD.</span><span class="sxs-lookup"><span data-stu-id="cf78e-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="cf78e-148">[Téléchargez et installez l’utilitaire de graveur de carte SD Etcher](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="cf78e-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="cf78e-149">Exécutez Etcher et sélectionnez l’image Raspbian extraite à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="cf78e-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="cf78e-150">Sélectionnez le lecteur de carte microSD.</span><span class="sxs-lookup"><span data-stu-id="cf78e-150">Select the microSD card drive.</span></span> <span data-ttu-id="cf78e-151">Remarque : Etcher a peut-être déjà sélectionné le lecteur approprié.</span><span class="sxs-lookup"><span data-stu-id="cf78e-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="cf78e-152">Cliquez sur Flash pour installer Raspbian sur la carte microSD.</span><span class="sxs-lookup"><span data-stu-id="cf78e-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="cf78e-153">Retirez la carte microSD de votre ordinateur une fois l’installation terminée.</span><span class="sxs-lookup"><span data-stu-id="cf78e-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="cf78e-154">Vous pouvez retirer directement la carte microSD en toute sécurité, car Etcher éjecte ou démonte automatiquement la carte microSD une fois le processus terminé.</span><span class="sxs-lookup"><span data-stu-id="cf78e-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="cf78e-155">Insérez la carte microSD dans Pi.</span><span class="sxs-lookup"><span data-stu-id="cf78e-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="cf78e-156">Activer SSH et I2C</span><span class="sxs-lookup"><span data-stu-id="cf78e-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="cf78e-157">Connectez Pi au moniteur, au clavier et à la souris, démarrez Pi puis connectez-vous à Raspbian en utilisant `pi` comme nom d’utilisateur et `raspberry` comme mot de passe.</span><span class="sxs-lookup"><span data-stu-id="cf78e-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="cf78e-158">Cliquez sur l’icône Raspberry > **Préférences** > **Configuration de Raspberry Pi**.</span><span class="sxs-lookup"><span data-stu-id="cf78e-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Le menu Préférences de Raspbian](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="cf78e-160">Sur l’onglet **Interfaces**, définissez **I2C** et **SSH** sur **Activer**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf78e-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="cf78e-161">Si vous ne possédez pas de capteurs physiques et que vous souhaitez utiliser des données de capteur simulé, cette étape est facultative.</span><span class="sxs-lookup"><span data-stu-id="cf78e-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Activer I2C et SSH sur Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="cf78e-163">Pour activer SSH et I2C, vous trouverez d’autres documents de référence sur [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) et [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="cf78e-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="cf78e-164">Connecter le capteur à Pi</span><span class="sxs-lookup"><span data-stu-id="cf78e-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="cf78e-165">Utilisez la platine d’expérimentation et les câbles de liaison pour connecter une LED et un BME280 à Pi comme suit.</span><span class="sxs-lookup"><span data-stu-id="cf78e-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="cf78e-166">Si vous ne disposez pas de ce capteur, ignorez cette section.</span><span class="sxs-lookup"><span data-stu-id="cf78e-166">If you don’t have the sensor, skip this section.</span></span>

![La connexion entre Raspberry Pi et le capteur](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="cf78e-168">Le capteur BME280 peut collecter des données sur la température et l’humidité.</span><span class="sxs-lookup"><span data-stu-id="cf78e-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="cf78e-169">Et la DEL clignote s’il existe une communication entre l’appareil et le cloud.</span><span class="sxs-lookup"><span data-stu-id="cf78e-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="cf78e-170">Pour les broches du capteur, utilisez le câblage suivant :</span><span class="sxs-lookup"><span data-stu-id="cf78e-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="cf78e-171">Début (capteur et LED)</span><span class="sxs-lookup"><span data-stu-id="cf78e-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="cf78e-172">Fin (carte)</span><span class="sxs-lookup"><span data-stu-id="cf78e-172">End (Board)</span></span>            | <span data-ttu-id="cf78e-173">Couleur du câble</span><span class="sxs-lookup"><span data-stu-id="cf78e-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="cf78e-174">VDD (broche 5G)</span><span class="sxs-lookup"><span data-stu-id="cf78e-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="cf78e-175">ALIM 3,3 V (broche 1)</span><span class="sxs-lookup"><span data-stu-id="cf78e-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="cf78e-176">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="cf78e-176">White cable</span></span>   |
| <span data-ttu-id="cf78e-177">GND (broche 7G)</span><span class="sxs-lookup"><span data-stu-id="cf78e-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="cf78e-178">GND (broche 6)</span><span class="sxs-lookup"><span data-stu-id="cf78e-178">GND (Pin 6)</span></span>            | <span data-ttu-id="cf78e-179">Câble marron</span><span class="sxs-lookup"><span data-stu-id="cf78e-179">Brown cable</span></span>   |
| <span data-ttu-id="cf78e-180">SCK (broche 8G)</span><span class="sxs-lookup"><span data-stu-id="cf78e-180">SCK (Pin 8G)</span></span>             | <span data-ttu-id="cf78e-181">I2C1 SDA (broche 3)</span><span class="sxs-lookup"><span data-stu-id="cf78e-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="cf78e-182">Câble orange</span><span class="sxs-lookup"><span data-stu-id="cf78e-182">Orange cable</span></span>  |
| <span data-ttu-id="cf78e-183">SDI (broche 10G)</span><span class="sxs-lookup"><span data-stu-id="cf78e-183">SDI (Pin 10G)</span></span>            | <span data-ttu-id="cf78e-184">I2C1 SCL (broche 5)</span><span class="sxs-lookup"><span data-stu-id="cf78e-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="cf78e-185">Câble rouge</span><span class="sxs-lookup"><span data-stu-id="cf78e-185">Red cable</span></span>     |
| <span data-ttu-id="cf78e-186">LED VDD (broche 18F)</span><span class="sxs-lookup"><span data-stu-id="cf78e-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="cf78e-187">GPIO 24 (broche 18)</span><span class="sxs-lookup"><span data-stu-id="cf78e-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="cf78e-188">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="cf78e-188">White cable</span></span>   |
| <span data-ttu-id="cf78e-189">LED GND (broche 17F)</span><span class="sxs-lookup"><span data-stu-id="cf78e-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="cf78e-190">GND (broche 20)</span><span class="sxs-lookup"><span data-stu-id="cf78e-190">GND (Pin 20)</span></span>           | <span data-ttu-id="cf78e-191">Câble noir</span><span class="sxs-lookup"><span data-stu-id="cf78e-191">Black cable</span></span>   |

<span data-ttu-id="cf78e-192">Cliquez pour afficher les [mappages de broches de Raspberry Pi 2 et 3](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) à titre de référence.</span><span class="sxs-lookup"><span data-stu-id="cf78e-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="cf78e-193">Une fois le BME280 connecté à votre Raspberry Pi, il doit se présenter comme sur l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cf78e-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Pi et BME280 connectés](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="cf78e-195">Connexion de Pi au réseau</span><span class="sxs-lookup"><span data-stu-id="cf78e-195">Connect Pi to the network</span></span>

<span data-ttu-id="cf78e-196">Mettez Pi sous tension à l’aide du câble micro USB et de l’alimentation.</span><span class="sxs-lookup"><span data-stu-id="cf78e-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="cf78e-197">Utilisez le câble Ethernet pour connecter Pi à votre réseau câblé ou suivez les [instructions fournies par la Fondation Raspberry Pi](https://www.raspberrypi.org/learning/software-guide/wifi/) pour connecter Pi à votre réseau sans fil.</span><span class="sxs-lookup"><span data-stu-id="cf78e-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="cf78e-198">Une fois que votre Pi est correctement connecté au réseau, vous devez relever son [adresse IP](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="cf78e-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Connecté au réseau câblé](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="cf78e-200">Assurez-vous que Pi est connecté au même réseau que votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cf78e-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="cf78e-201">Par exemple, si votre ordinateur est connecté à un réseau sans fil alors que Pi est connecté à un réseau câblé, il se peut que vous ne voyiez pas l’adresse IP dans la sortie devdisco.</span><span class="sxs-lookup"><span data-stu-id="cf78e-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="cf78e-202">Exécuter un exemple d’application sur Pi</span><span class="sxs-lookup"><span data-stu-id="cf78e-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a><span data-ttu-id="cf78e-203">Cloner l’exemple d’application et installer les packages de composants requis</span><span class="sxs-lookup"><span data-stu-id="cf78e-203">Clone sample application and install the prerequisite packages</span></span>

1. <span data-ttu-id="cf78e-204">Utilisez l’un des clients SSH suivants à partir de votre ordinateur hôte pour vous connecter à votre Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="cf78e-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
    - <span data-ttu-id="cf78e-205">[PuTTY](http://www.putty.org/) pour Windows.</span><span class="sxs-lookup"><span data-stu-id="cf78e-205">[PuTTY](http://www.putty.org/) for Windows.</span></span> <span data-ttu-id="cf78e-206">Vous avez besoin de l’adresse IP de votre Pi pour le connecter via le protocole SSH.</span><span class="sxs-lookup"><span data-stu-id="cf78e-206">You need the IP address of your Pi to connect it via SSH.</span></span>
    - <span data-ttu-id="cf78e-207">Le client SSH intégré sur Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="cf78e-207">The built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="cf78e-208">Vous devrez peut-être exécuter `ssh pi@<ip address of pi>` pour connecter le Pi via le protocole SSH.</span><span class="sxs-lookup"><span data-stu-id="cf78e-208">You might need run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>

   > [!NOTE] 
   <span data-ttu-id="cf78e-209">Le nom d’utilisateur par défaut est `pi` et le mot de passe est `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="cf78e-209">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="cf78e-210">Installez Node.js et NPM sur votre Pi.</span><span class="sxs-lookup"><span data-stu-id="cf78e-210">Install Node.js and NPM to your Pi.</span></span>
   
   <span data-ttu-id="cf78e-211">Dans un premier temps, vous devez vérifier votre version de Node.js avec la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="cf78e-211">First you should check your Node.js version with the following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="cf78e-212">Si la version est antérieure à 4.x ou qu’aucun Node.js n’existe sur votre Pi, exécutez la commande suivante pour installer ou mettre à jour Node.js.</span><span class="sxs-lookup"><span data-stu-id="cf78e-212">If the version is lower than 4.x or there is no Node.js on your Pi, then run the following command to install or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="cf78e-213">Clonez l’exemple d’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cf78e-213">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="cf78e-214">Installez tous les packages à l’aide de la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="cf78e-214">Install all packages by the following command.</span></span> <span data-ttu-id="cf78e-215">Cela inclut Azure IoT device SDK, la bibliothèque de capteur BME280 et la bibliothèque de câblage de Pi.</span><span class="sxs-lookup"><span data-stu-id="cf78e-215">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="cf78e-216">La procédure d’installation peut prendre plusieurs minutes, en fonction de la connexion de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="cf78e-216">It might take several minutes to finish this installation process denpening on your network connection.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="cf78e-217">Configurer l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="cf78e-217">Configure the sample application</span></span>

1. <span data-ttu-id="cf78e-218">Ouvrez le fichier de configuration en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cf78e-218">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Fichier de configuration](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="cf78e-220">Deux éléments peuvent être configurés dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="cf78e-220">There are two items in this file you can configurate.</span></span> <span data-ttu-id="cf78e-221">Le premier est `interval`, qui définit le délai entre deux messages envoyés au cloud.</span><span class="sxs-lookup"><span data-stu-id="cf78e-221">The first one is `interval`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="cf78e-222">Le deuxième est `simulatedData`, qui est une valeur booléenne pour l’utilisation ou non des données de capteur simulées.</span><span class="sxs-lookup"><span data-stu-id="cf78e-222">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="cf78e-223">Si vous **ne disposez pas du capteur**, définissez la valeur `simulatedData` sur `true` pour que l’exemple d’application crée et utilise des données de capteur simulées.</span><span class="sxs-lookup"><span data-stu-id="cf78e-223">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="cf78e-224">Enregistrez et quittez en appuyant sur Ctrl-O > Entrée > Ctrl-X.</span><span class="sxs-lookup"><span data-stu-id="cf78e-224">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="cf78e-225">Exécuter l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="cf78e-225">Run the sample application</span></span>

1. <span data-ttu-id="cf78e-226">Exécutez l’exemple d’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cf78e-226">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="cf78e-227">Assurez-vous de copier-coller la chaîne de connexion de l’appareil entre les guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="cf78e-227">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="cf78e-228">Vous devriez voir le résultat suivant, qui affiche les données de capteur et les messages envoyés à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cf78e-228">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Sortie - données de capteur envoyées depuis Raspberry Pi vers votre IoT Hub](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="cf78e-230">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cf78e-230">Next steps</span></span>

<span data-ttu-id="cf78e-231">Vous avez exécuté un exemple d’application pour collecter des données de capteur et les envoyer à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cf78e-231">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]