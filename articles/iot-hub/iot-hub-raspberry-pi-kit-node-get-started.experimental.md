---
title: toocloud aaaRaspberry Pi (Node.js) - se connecter un Pi framboises tooAzure IoT Hub | Documents Microsoft
description: "Se connecter tooAzure framboises Pi IoT Hub pour framboises Pi toosend données toohello cloud Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure iot raspberry pi, raspberry pi iot hub, raspberry pi envoi données toocloud, raspberry pi toocloud"
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
ms.openlocfilehash: 07bc66983c427eab8118be18d91abb25deb03ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a><span data-ttu-id="2e923-104">Se connecter framboises Pi tooAzure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="2e923-104">Connect Raspberry Pi tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="2e923-105">Dans ce didacticiel, commencer par découvrir hello les bases de l’utilisation de Pi framboises qui Raspbian est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2e923-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="2e923-106">Vous apprendrez ensuite comment tooseamlessly connecter votre cloud toohello de périphériques à l’aide de [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="2e923-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="2e923-107">Pour obtenir des exemples de Windows 10 IoT Core, accédez à toohello [centre de développement Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="2e923-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="2e923-108">Vous n’avez pas encore de kit ?</span><span class="sxs-lookup"><span data-stu-id="2e923-108">Don't have a kit yet?</span></span> <span data-ttu-id="2e923-109">Essayez de hello [framboises Pi 3 émulateur](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span><span class="sxs-lookup"><span data-stu-id="2e923-109">Try hello [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span></span> <span data-ttu-id="2e923-110">Ou achetez un nouveau kit [ici](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="2e923-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="2e923-111">Procédure</span><span class="sxs-lookup"><span data-stu-id="2e923-111">What you do</span></span>

* <span data-ttu-id="2e923-112">Configurez Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="2e923-112">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="2e923-113">Créez un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2e923-113">Create an IoT hub.</span></span>
* <span data-ttu-id="2e923-114">Inscrivez un appareil pour Pi dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e923-114">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="2e923-115">Exécuter un exemple d’application sur le concentrateur de Pi toosend capteur données tooyour IoT.</span><span class="sxs-lookup"><span data-stu-id="2e923-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="2e923-116">Connectez framboises Pi tooan IoT concentrateur que vous créez.</span><span class="sxs-lookup"><span data-stu-id="2e923-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="2e923-117">Ensuite, vous exécutez un exemple d’application sur les données de température et humidité toocollect Pi à partir d’un capteur BME280.</span><span class="sxs-lookup"><span data-stu-id="2e923-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="2e923-118">Enfin, vous envoyez le hub IoT tooyour hello capteur données.</span><span class="sxs-lookup"><span data-stu-id="2e923-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="2e923-119">Contenu</span><span class="sxs-lookup"><span data-stu-id="2e923-119">What you learn</span></span>

* <span data-ttu-id="2e923-120">Comment toocreate un Azure IoT hub et obtenir votre nouvelle chaîne de connexion de périphérique.</span><span class="sxs-lookup"><span data-stu-id="2e923-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="2e923-121">Comment tooconnect Pi, avec un capteur BME280.</span><span class="sxs-lookup"><span data-stu-id="2e923-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="2e923-122">Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur Pi.</span><span class="sxs-lookup"><span data-stu-id="2e923-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="2e923-123">Comment le hub IoT tooyour toosend capteur données.</span><span class="sxs-lookup"><span data-stu-id="2e923-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2e923-124">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="2e923-124">What you need</span></span>

![Ce dont vous avez besoin](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="2e923-126">Hello framboises Pi 2 ou 3 de Pi framboises du tableau.</span><span class="sxs-lookup"><span data-stu-id="2e923-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="2e923-127">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="2e923-127">An active Azure subscription.</span></span> <span data-ttu-id="2e923-128">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="2e923-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="2e923-129">Un moniteur, un clavier USB et la souris qui se connectent tooPi.</span><span class="sxs-lookup"><span data-stu-id="2e923-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="2e923-130">Un Mac ou un PC exécutant Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="2e923-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="2e923-131">Une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="2e923-131">An Internet connection.</span></span>
* <span data-ttu-id="2e923-132">Une carte microSD d’au moins 16 Go.</span><span class="sxs-lookup"><span data-stu-id="2e923-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="2e923-133">Une USB-SD carte microSD carte tooburn hello système d’exploitation image ou sur une carte microSD de hello.</span><span class="sxs-lookup"><span data-stu-id="2e923-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="2e923-134">Une puissance de 2-amp 5-v fournir avec un câble USB micro de hello 6-pied.</span><span class="sxs-lookup"><span data-stu-id="2e923-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="2e923-135">Hello éléments suivants est facultatif :</span><span class="sxs-lookup"><span data-stu-id="2e923-135">hello following items are optional:</span></span>

* <span data-ttu-id="2e923-136">Un capteur de température, de pression et d’humidité Adafruit BME280 assemblé.</span><span class="sxs-lookup"><span data-stu-id="2e923-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="2e923-137">Une platine d’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="2e923-137">A breadboard.</span></span>
* <span data-ttu-id="2e923-138">6 câbles de liaison F/M.</span><span class="sxs-lookup"><span data-stu-id="2e923-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="2e923-139">Une LED de 10 mm diffuse.</span><span class="sxs-lookup"><span data-stu-id="2e923-139">A diffused 10-mm LED.</span></span>

  > [!NOTE] 
  <span data-ttu-id="2e923-140">Ces éléments sont facultatifs, car la prise en charge des exemples de code hello simulée des données de capteur.</span><span class="sxs-lookup"><span data-stu-id="2e923-140">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="2e923-141">Configuration de Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="2e923-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="2e923-142">Installer le système d’exploitation de Raspbian hello de Pi</span><span class="sxs-lookup"><span data-stu-id="2e923-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="2e923-143">Préparer la carte microSD de hello pour l’installation de l’image de Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="2e923-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="2e923-144">Téléchargez Raspbian.</span><span class="sxs-lookup"><span data-stu-id="2e923-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="2e923-145">[Télécharger Raspbian Jessie avec Pixel](https://www.raspberrypi.org/downloads/raspbian/) (fichier .zip de hello).</span><span class="sxs-lookup"><span data-stu-id="2e923-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="2e923-146">Extraire le dossier de tooa hello Raspbian image sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2e923-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="2e923-147">Installez Raspbian toohello microSD carte.</span><span class="sxs-lookup"><span data-stu-id="2e923-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="2e923-148">[Téléchargez et installez l’utilitaire graveur de hello Etcher SD carte](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="2e923-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="2e923-149">Exécutez Etcher et sélectionnez l’image Raspbian hello que vous avez extrait à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="2e923-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="2e923-150">Sélectionnez le lecteur de carte microSD hello.</span><span class="sxs-lookup"><span data-stu-id="2e923-150">Select hello microSD card drive.</span></span> <span data-ttu-id="2e923-151">Notez que Etcher peut avoir déjà sélectionné lecteur hello.</span><span class="sxs-lookup"><span data-stu-id="2e923-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="2e923-152">Cliquez sur le disque mémoire Flash tooinstall Raspbian toohello microSD carte.</span><span class="sxs-lookup"><span data-stu-id="2e923-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="2e923-153">Retirez hello microSD votre ordinateur lorsque l’installation est terminée.</span><span class="sxs-lookup"><span data-stu-id="2e923-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="2e923-154">Carte microSD de hello tooremove safe est directement car Etcher éjecte automatiquement ou démonte carte microSD de hello à l’achèvement.</span><span class="sxs-lookup"><span data-stu-id="2e923-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="2e923-155">Insérer carte microSD de hello Pi.</span><span class="sxs-lookup"><span data-stu-id="2e923-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="2e923-156">Activer SSH et I2C</span><span class="sxs-lookup"><span data-stu-id="2e923-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="2e923-157">Connecter le moniteur de toohello Pi, clavier et souris, démarrer Pi, puis Raspbian à l’aide de `pi` en tant que nom d’utilisateur hello et `raspberry` comme mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="2e923-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="2e923-158">Cliquez sur hello icône Raspberry > **préférences** > **framboises Pi Configuration**.</span><span class="sxs-lookup"><span data-stu-id="2e923-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![menu de préférences de Raspbian Hello](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="2e923-160">Sur hello **Interfaces** onglet, définissez **I2C** et **SSH** trop**activer**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e923-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="2e923-161">Si vous n’ayez des capteurs physiques et souhaitez que les données de capteur toouse simulée, cette étape est facultative.</span><span class="sxs-lookup"><span data-stu-id="2e923-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Activer I2C et SSH sur Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="2e923-163">tooenable SSH et I2C, vous trouverez plus de documents de référence sur [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) et [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="2e923-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="2e923-164">Se connecter hello capteur tooPi</span><span class="sxs-lookup"><span data-stu-id="2e923-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="2e923-165">Utilisez les fils de breadboard et cavaliers hello tooconnect une DEL et un tooPi BME280 comme suit.</span><span class="sxs-lookup"><span data-stu-id="2e923-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="2e923-166">Si vous n’avez pas capteur de hello, ignorez cette section.</span><span class="sxs-lookup"><span data-stu-id="2e923-166">If you don’t have hello sensor, skip this section.</span></span>

![Hello framboises Pi et capteur de connexion](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="2e923-168">capteur de Hello BME280 pouvez collecter des données de température et humidité.</span><span class="sxs-lookup"><span data-stu-id="2e923-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="2e923-169">Et hello LED clignote s’il existe une communication entre l’appareil et hello cloud.</span><span class="sxs-lookup"><span data-stu-id="2e923-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="2e923-170">Pour les codes confidentiels de capteur, utilisez hello suivant câblage :</span><span class="sxs-lookup"><span data-stu-id="2e923-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="2e923-171">Début (capteur et LED)</span><span class="sxs-lookup"><span data-stu-id="2e923-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="2e923-172">Fin (carte)</span><span class="sxs-lookup"><span data-stu-id="2e923-172">End (Board)</span></span>            | <span data-ttu-id="2e923-173">Couleur du câble</span><span class="sxs-lookup"><span data-stu-id="2e923-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="2e923-174">VDD (broche 5G)</span><span class="sxs-lookup"><span data-stu-id="2e923-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="2e923-175">ALIM 3,3 V (broche 1)</span><span class="sxs-lookup"><span data-stu-id="2e923-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="2e923-176">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="2e923-176">White cable</span></span>   |
| <span data-ttu-id="2e923-177">GND (broche 7G)</span><span class="sxs-lookup"><span data-stu-id="2e923-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="2e923-178">GND (broche 6)</span><span class="sxs-lookup"><span data-stu-id="2e923-178">GND (Pin 6)</span></span>            | <span data-ttu-id="2e923-179">Câble marron</span><span class="sxs-lookup"><span data-stu-id="2e923-179">Brown cable</span></span>   |
| <span data-ttu-id="2e923-180">SCK (broche 8G)</span><span class="sxs-lookup"><span data-stu-id="2e923-180">SCK (Pin 8G)</span></span>             | <span data-ttu-id="2e923-181">I2C1 SDA (broche 3)</span><span class="sxs-lookup"><span data-stu-id="2e923-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="2e923-182">Câble orange</span><span class="sxs-lookup"><span data-stu-id="2e923-182">Orange cable</span></span>  |
| <span data-ttu-id="2e923-183">SDI (broche 10G)</span><span class="sxs-lookup"><span data-stu-id="2e923-183">SDI (Pin 10G)</span></span>            | <span data-ttu-id="2e923-184">I2C1 SCL (broche 5)</span><span class="sxs-lookup"><span data-stu-id="2e923-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="2e923-185">Câble rouge</span><span class="sxs-lookup"><span data-stu-id="2e923-185">Red cable</span></span>     |
| <span data-ttu-id="2e923-186">LED VDD (broche 18F)</span><span class="sxs-lookup"><span data-stu-id="2e923-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="2e923-187">GPIO 24 (broche 18)</span><span class="sxs-lookup"><span data-stu-id="2e923-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="2e923-188">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="2e923-188">White cable</span></span>   |
| <span data-ttu-id="2e923-189">LED GND (broche 17F)</span><span class="sxs-lookup"><span data-stu-id="2e923-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="2e923-190">GND (broche 20)</span><span class="sxs-lookup"><span data-stu-id="2e923-190">GND (Pin 20)</span></span>           | <span data-ttu-id="2e923-191">Câble noir</span><span class="sxs-lookup"><span data-stu-id="2e923-191">Black cable</span></span>   |

<span data-ttu-id="2e923-192">Cliquez sur tooview [framboises Pi 2 et 3 mappages de code confidentiel](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) de référence.</span><span class="sxs-lookup"><span data-stu-id="2e923-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="2e923-193">Une fois que vous avez connecté BME280 tooyour framboises Pi, elle doit être comme sous l’image.</span><span class="sxs-lookup"><span data-stu-id="2e923-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Pi et BME280 connectés](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="2e923-195">Connecter Pi toohello réseau</span><span class="sxs-lookup"><span data-stu-id="2e923-195">Connect Pi toohello network</span></span>

<span data-ttu-id="2e923-196">Pi sous tension à l’aide de câble USB micro de hello et alimentation hello.</span><span class="sxs-lookup"><span data-stu-id="2e923-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="2e923-197">Utilisez hello Ethernet câble tooconnect Pi tooyour câblé réseau ou suivez hello [instructions hello framboises Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) réseau sans fil de tooconnect Pi tooyour.</span><span class="sxs-lookup"><span data-stu-id="2e923-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="2e923-198">Une fois votre Pi a été correctement connecté toohello réseau, vous devez tootake note de hello [adresse IP de votre Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="2e923-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Réseau de toowired connecté](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="2e923-200">Assurez-vous que Pi est connecté toohello même réseau que votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2e923-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="2e923-201">Par exemple, si votre ordinateur est connecté tooa les réseau sans fil pendant que Pi est connecté tooa réseau câblé, vous verrez ne peut-être pas hello IP adresse dans la sortie de devdisco hello.</span><span class="sxs-lookup"><span data-stu-id="2e923-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="2e923-202">Exécuter un exemple d’application sur Pi</span><span class="sxs-lookup"><span data-stu-id="2e923-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a><span data-ttu-id="2e923-203">Cloner l’exemple d’application et installer les packages de composants requis hello</span><span class="sxs-lookup"><span data-stu-id="2e923-203">Clone sample application and install hello prerequisite packages</span></span>

1. <span data-ttu-id="2e923-204">Utilisez une des hello suivant clients SSH à partir de votre ordinateur hôte ordinateur tooconnect tooyour framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="2e923-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
    - <span data-ttu-id="2e923-205">[PuTTY](http://www.putty.org/) pour Windows.</span><span class="sxs-lookup"><span data-stu-id="2e923-205">[PuTTY](http://www.putty.org/) for Windows.</span></span> <span data-ttu-id="2e923-206">Vous avez besoin d’adresse IP hello votre tooconnect Pi via SSH.</span><span class="sxs-lookup"><span data-stu-id="2e923-206">You need hello IP address of your Pi tooconnect it via SSH.</span></span>
    - <span data-ttu-id="2e923-207">client Hello intégré SSH sur Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="2e923-207">hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="2e923-208">Vous pouvez peut-être exécuter `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span><span class="sxs-lookup"><span data-stu-id="2e923-208">You might need run `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>

   > [!NOTE] 
   <span data-ttu-id="2e923-209">nom d’utilisateur par défaut de Hello est `pi` , et le mot de passe hello est `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="2e923-209">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="2e923-210">Installation de Node.js et NPM tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="2e923-210">Install Node.js and NPM tooyour Pi.</span></span>
   
   <span data-ttu-id="2e923-211">Tout d’abord, vous devez vérifier votre version de Node.js avec hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="2e923-211">First you should check your Node.js version with hello following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="2e923-212">Version de hello est inférieure à 4.x ou s’il n’existe aucune Node.js sur votre Pi, puis exécutez hello suivant tooinstall de commande ou de mettre à jour de Node.js.</span><span class="sxs-lookup"><span data-stu-id="2e923-212">If hello version is lower than 4.x or there is no Node.js on your Pi, then run hello following command tooinstall or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="2e923-213">Pour cloner l’exemple d’application hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2e923-213">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="2e923-214">Installez tous les packages en hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="2e923-214">Install all packages by hello following command.</span></span> <span data-ttu-id="2e923-215">Cela inclut Azure IoT device SDK, la bibliothèque de capteur BME280 et la bibliothèque de câblage de Pi.</span><span class="sxs-lookup"><span data-stu-id="2e923-215">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="2e923-216">Il peut prendre plusieurs minutes toofinish cette denpening de processus d’installation sur votre connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="2e923-216">It might take several minutes toofinish this installation process denpening on your network connection.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="2e923-217">Configurer l’application d’exemple hello</span><span class="sxs-lookup"><span data-stu-id="2e923-217">Configure hello sample application</span></span>

1. <span data-ttu-id="2e923-218">Ouvrez le fichier de configuration de hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="2e923-218">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Fichier de configuration](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="2e923-220">Deux éléments peuvent être configurés dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="2e923-220">There are two items in this file you can configurate.</span></span> <span data-ttu-id="2e923-221">Bonjour tout d’abord un est `interval`, qui définit l’intervalle de temps hello entre les deux messages toocloud d’envoi.</span><span class="sxs-lookup"><span data-stu-id="2e923-221">hello first one is `interval`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="2e923-222">Hello deuxième `simulatedData`, qui est une valeur booléenne pour toouse indique si les données de capteur simulé ou non.</span><span class="sxs-lookup"><span data-stu-id="2e923-222">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="2e923-223">Si vous **n’avez pas capteur de hello**, affectez la valeur hello `simulatedData` valeur trop`true` toomake hello exemple d’application, créer et utiliser des données de capteur simulé.</span><span class="sxs-lookup"><span data-stu-id="2e923-223">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="2e923-224">Enregistrez et quittez en appuyant sur Ctrl-O > Entrée > Ctrl-X.</span><span class="sxs-lookup"><span data-stu-id="2e923-224">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="2e923-225">Exécutez l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="2e923-225">Run hello sample application</span></span>

1. <span data-ttu-id="2e923-226">Exécuter l’exemple d’application hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2e923-226">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="2e923-227">Assurez-vous que vous copier-coller chaîne de connexion de périphérique hello dans des guillemets simples de hello.</span><span class="sxs-lookup"><span data-stu-id="2e923-227">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="2e923-228">Vous devez voir qu’affiche hello messages hello et les données de capteur envoyés tooyour IoT hub de sortie suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="2e923-228">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Sortie - données de capteur envoyés à partir de framboises Pi tooyour IoT hub](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="2e923-230">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e923-230">Next steps</span></span>

<span data-ttu-id="2e923-231">Vous avez exécuté un exemple de données de capteur application toocollect et envoyez tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2e923-231">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]