---
title: aaaRaspberry Pi toocloud (C) - se connecter un Pi framboises tooAzure IoT Hub | Documents Microsoft
description: "Découvrez comment toosetup et connectez-vous framboises Pi tooAzure IoT Hub pour la plateforme de cloud computing Azure framboises Pi toosend données toohello dans ce didacticiel."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot raspberry pi, raspberry pi iot hub, raspberry pi envoi données toocloud, raspberry pi toocloud"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05086890458e196d7fdc87a53fcabb9386245d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-c"></a><span data-ttu-id="fafa5-104">Se connecter framboises Pi tooAzure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="fafa5-104">Connect Raspberry Pi tooAzure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="fafa5-105">Dans ce didacticiel, commencer par découvrir hello les bases de l’utilisation de Pi framboises qui Raspbian est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fafa5-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="fafa5-106">Vous apprendrez ensuite comment tooseamlessly connecter votre cloud toohello de périphériques à l’aide de [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="fafa5-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="fafa5-107">Pour obtenir des exemples de Windows 10 IoT Core, accédez à toohello [centre de développement Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="fafa5-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="fafa5-108">Vous n’avez pas encore de kit ?</span><span class="sxs-lookup"><span data-stu-id="fafa5-108">Don't have a kit yet?</span></span> <span data-ttu-id="fafa5-109">Essayez [le simulateur en ligne Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fafa5-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="fafa5-110">Ou achetez un nouveau kit [ici](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="fafa5-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="fafa5-111">Procédure</span><span class="sxs-lookup"><span data-stu-id="fafa5-111">What you do</span></span>

* <span data-ttu-id="fafa5-112">Créez un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fafa5-112">Create an IoT hub.</span></span>
* <span data-ttu-id="fafa5-113">Inscrivez un appareil pour Pi dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="fafa5-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="fafa5-114">Configurez Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="fafa5-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="fafa5-115">Exécuter un exemple d’application sur le concentrateur de Pi toosend capteur données tooyour IoT.</span><span class="sxs-lookup"><span data-stu-id="fafa5-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="fafa5-116">Connectez framboises Pi tooan IoT concentrateur que vous créez.</span><span class="sxs-lookup"><span data-stu-id="fafa5-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="fafa5-117">Ensuite, vous exécutez un exemple d’application sur les données de température et humidité toocollect Pi à partir d’un capteur BME280.</span><span class="sxs-lookup"><span data-stu-id="fafa5-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="fafa5-118">Enfin, vous envoyez le hub IoT tooyour hello capteur données.</span><span class="sxs-lookup"><span data-stu-id="fafa5-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="fafa5-119">Contenu</span><span class="sxs-lookup"><span data-stu-id="fafa5-119">What you learn</span></span>

* <span data-ttu-id="fafa5-120">Comment toocreate un Azure IoT hub et obtenir votre nouvelle chaîne de connexion de périphérique.</span><span class="sxs-lookup"><span data-stu-id="fafa5-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="fafa5-121">Comment tooconnect Pi, avec un capteur BME280.</span><span class="sxs-lookup"><span data-stu-id="fafa5-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="fafa5-122">Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur Pi.</span><span class="sxs-lookup"><span data-stu-id="fafa5-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="fafa5-123">Comment le hub IoT tooyour toosend capteur données.</span><span class="sxs-lookup"><span data-stu-id="fafa5-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fafa5-124">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="fafa5-124">What you need</span></span>

![Ce dont vous avez besoin](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="fafa5-126">Hello framboises Pi 2 ou 3 de Pi framboises du tableau.</span><span class="sxs-lookup"><span data-stu-id="fafa5-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="fafa5-127">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="fafa5-127">An active Azure subscription.</span></span> <span data-ttu-id="fafa5-128">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="fafa5-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="fafa5-129">Un moniteur, un clavier USB et la souris qui se connectent tooPi.</span><span class="sxs-lookup"><span data-stu-id="fafa5-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="fafa5-130">Un Mac ou un PC exécutant Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="fafa5-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="fafa5-131">Une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="fafa5-131">An Internet connection.</span></span>
* <span data-ttu-id="fafa5-132">Une carte microSD d’au moins 16 Go.</span><span class="sxs-lookup"><span data-stu-id="fafa5-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="fafa5-133">Une USB-SD carte microSD carte tooburn hello système d’exploitation image ou sur une carte microSD de hello.</span><span class="sxs-lookup"><span data-stu-id="fafa5-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="fafa5-134">Une puissance de 2-amp 5-v fournir avec un câble USB micro de hello 6-pied.</span><span class="sxs-lookup"><span data-stu-id="fafa5-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="fafa5-135">Hello éléments suivants est facultatif :</span><span class="sxs-lookup"><span data-stu-id="fafa5-135">hello following items are optional:</span></span>

* <span data-ttu-id="fafa5-136">Un capteur de température, de pression et d’humidité Adafruit BME280 assemblé.</span><span class="sxs-lookup"><span data-stu-id="fafa5-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="fafa5-137">Une platine d’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="fafa5-137">A breadboard.</span></span>
* <span data-ttu-id="fafa5-138">6 câbles de liaison F/M.</span><span class="sxs-lookup"><span data-stu-id="fafa5-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="fafa5-139">Une LED de 10 mm diffuse.</span><span class="sxs-lookup"><span data-stu-id="fafa5-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="fafa5-140">Ces éléments sont facultatifs, car la prise en charge des exemples de code hello simulée des données de capteur.</span><span class="sxs-lookup"><span data-stu-id="fafa5-140">These items are optional because hello code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="fafa5-141">Configuration de Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="fafa5-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="fafa5-142">Installer le système d’exploitation de Raspbian hello de Pi</span><span class="sxs-lookup"><span data-stu-id="fafa5-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="fafa5-143">Préparer la carte microSD de hello pour l’installation de l’image de Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="fafa5-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="fafa5-144">Téléchargez Raspbian.</span><span class="sxs-lookup"><span data-stu-id="fafa5-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="fafa5-145">[Télécharger Raspbian Jessie avec le bureau](https://www.raspberrypi.org/downloads/raspbian/) (fichier .zip de hello).</span><span class="sxs-lookup"><span data-stu-id="fafa5-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="fafa5-146">Extraire le dossier de tooa hello Raspbian image sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="fafa5-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="fafa5-147">Installez Raspbian toohello microSD carte.</span><span class="sxs-lookup"><span data-stu-id="fafa5-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="fafa5-148">[Téléchargez et installez l’utilitaire graveur de hello Etcher SD carte](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="fafa5-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="fafa5-149">Exécutez Etcher et sélectionnez l’image Raspbian hello que vous avez extrait à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="fafa5-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="fafa5-150">Sélectionnez le lecteur de carte microSD hello.</span><span class="sxs-lookup"><span data-stu-id="fafa5-150">Select hello microSD card drive.</span></span> <span data-ttu-id="fafa5-151">Notez que Etcher peut avoir déjà sélectionné lecteur hello.</span><span class="sxs-lookup"><span data-stu-id="fafa5-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="fafa5-152">Cliquez sur le disque mémoire Flash tooinstall Raspbian toohello microSD carte.</span><span class="sxs-lookup"><span data-stu-id="fafa5-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="fafa5-153">Retirez hello microSD votre ordinateur lorsque l’installation est terminée.</span><span class="sxs-lookup"><span data-stu-id="fafa5-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="fafa5-154">Carte microSD de hello tooremove safe est directement car Etcher éjecte automatiquement ou démonte carte microSD de hello à l’achèvement.</span><span class="sxs-lookup"><span data-stu-id="fafa5-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="fafa5-155">Insérer carte microSD de hello Pi.</span><span class="sxs-lookup"><span data-stu-id="fafa5-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-spi"></a><span data-ttu-id="fafa5-156">Activer SSH et SPI</span><span class="sxs-lookup"><span data-stu-id="fafa5-156">Enable SSH and SPI</span></span>

1. <span data-ttu-id="fafa5-157">Connecter le moniteur de toohello Pi, clavier et souris, démarrer Pi, puis Raspbian à l’aide de `pi` en tant que nom d’utilisateur hello et `raspberry` comme mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="fafa5-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="fafa5-158">Cliquez sur hello icône Raspberry > **préférences** > **framboises Pi Configuration**.</span><span class="sxs-lookup"><span data-stu-id="fafa5-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![menu de préférences de Raspbian Hello](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="fafa5-160">Sur hello **Interfaces** onglet, définissez **SPI** et **SSH** trop**activer**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="fafa5-160">On hello **Interfaces** tab, set **SPI** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="fafa5-161">Si vous n’ayez des capteurs physiques et souhaitez que les données de capteur toouse simulée, cette étape est facultative.</span><span class="sxs-lookup"><span data-stu-id="fafa5-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Activer SPI et SSH sur Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="fafa5-163">tooenable SSH et SPI, vous trouverez plus de documents de référence sur [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) et [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="fafa5-163">tooenable SSH and SPI, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="fafa5-164">Se connecter hello capteur tooPi</span><span class="sxs-lookup"><span data-stu-id="fafa5-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="fafa5-165">Utilisez les fils de breadboard et cavaliers hello tooconnect une DEL et un tooPi BME280 comme suit.</span><span class="sxs-lookup"><span data-stu-id="fafa5-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="fafa5-166">Si vous n’avez capteur hello [ignorer cette section](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="fafa5-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Hello framboises Pi et capteur de connexion](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="fafa5-168">capteur de Hello BME280 pouvez collecter des données de température et humidité.</span><span class="sxs-lookup"><span data-stu-id="fafa5-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="fafa5-169">Et hello LED clignote s’il existe une communication entre l’appareil et hello cloud.</span><span class="sxs-lookup"><span data-stu-id="fafa5-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="fafa5-170">Pour les codes confidentiels de capteur, utilisez hello suivant câblage :</span><span class="sxs-lookup"><span data-stu-id="fafa5-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="fafa5-171">Début (capteur et LED)</span><span class="sxs-lookup"><span data-stu-id="fafa5-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="fafa5-172">Fin (carte)</span><span class="sxs-lookup"><span data-stu-id="fafa5-172">End (Board)</span></span>            | <span data-ttu-id="fafa5-173">Couleur du câble</span><span class="sxs-lookup"><span data-stu-id="fafa5-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="fafa5-174">LED VDD (broche 5G)</span><span class="sxs-lookup"><span data-stu-id="fafa5-174">LED VDD (Pin 5G)</span></span>         | <span data-ttu-id="fafa5-175">GPIO 4 (broche 7)</span><span class="sxs-lookup"><span data-stu-id="fafa5-175">GPIO 4 (Pin 7)</span></span>         | <span data-ttu-id="fafa5-176">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="fafa5-176">White cable</span></span>   |
| <span data-ttu-id="fafa5-177">LED GND (broche 6G)</span><span class="sxs-lookup"><span data-stu-id="fafa5-177">LED GND (Pin 6G)</span></span>         | <span data-ttu-id="fafa5-178">GND (broche 6)</span><span class="sxs-lookup"><span data-stu-id="fafa5-178">GND (Pin 6)</span></span>            | <span data-ttu-id="fafa5-179">Câble noir</span><span class="sxs-lookup"><span data-stu-id="fafa5-179">Black cable</span></span>   |
| <span data-ttu-id="fafa5-180">VDD (broche 18F)</span><span class="sxs-lookup"><span data-stu-id="fafa5-180">VDD (Pin 18F)</span></span>            | <span data-ttu-id="fafa5-181">ALIM 3,3V (broche 17)</span><span class="sxs-lookup"><span data-stu-id="fafa5-181">3.3V PWR (Pin 17)</span></span>      | <span data-ttu-id="fafa5-182">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="fafa5-182">White cable</span></span>   |
| <span data-ttu-id="fafa5-183">GND (broche 20F)</span><span class="sxs-lookup"><span data-stu-id="fafa5-183">GND (Pin 20F)</span></span>            | <span data-ttu-id="fafa5-184">GND (broche 20)</span><span class="sxs-lookup"><span data-stu-id="fafa5-184">GND (Pin 20)</span></span>           | <span data-ttu-id="fafa5-185">Câble noir</span><span class="sxs-lookup"><span data-stu-id="fafa5-185">Black cable</span></span>   |
| <span data-ttu-id="fafa5-186">SCK (broche 21F)</span><span class="sxs-lookup"><span data-stu-id="fafa5-186">SCK (Pin 21F)</span></span>            | <span data-ttu-id="fafa5-187">SPI0 SCLK (broche 23)</span><span class="sxs-lookup"><span data-stu-id="fafa5-187">SPI0 SCLK (Pin 23)</span></span>     | <span data-ttu-id="fafa5-188">Câble orange</span><span class="sxs-lookup"><span data-stu-id="fafa5-188">Orange cable</span></span>  |
| <span data-ttu-id="fafa5-189">SDO (broche 22F)</span><span class="sxs-lookup"><span data-stu-id="fafa5-189">SDO (Pin 22F)</span></span>            | <span data-ttu-id="fafa5-190">SPI0 MISO (broche 21)</span><span class="sxs-lookup"><span data-stu-id="fafa5-190">SPI0 MISO (Pin 21)</span></span>     | <span data-ttu-id="fafa5-191">Câble jaune</span><span class="sxs-lookup"><span data-stu-id="fafa5-191">Yellow cable</span></span>  |
| <span data-ttu-id="fafa5-192">SDI (broche 23F)</span><span class="sxs-lookup"><span data-stu-id="fafa5-192">SDI (Pin 23F)</span></span>            | <span data-ttu-id="fafa5-193">SPI0 MOSI (broche 19)</span><span class="sxs-lookup"><span data-stu-id="fafa5-193">SPI0 MOSI (Pin 19)</span></span>     | <span data-ttu-id="fafa5-194">Câble vert</span><span class="sxs-lookup"><span data-stu-id="fafa5-194">Green cable</span></span>   |
| <span data-ttu-id="fafa5-195">CS (broche 24F)</span><span class="sxs-lookup"><span data-stu-id="fafa5-195">CS (Pin 24F)</span></span>             | <span data-ttu-id="fafa5-196">SPI0 CS (broche 24)</span><span class="sxs-lookup"><span data-stu-id="fafa5-196">SPI0 CS (Pin 24)</span></span>       | <span data-ttu-id="fafa5-197">Câble bleu</span><span class="sxs-lookup"><span data-stu-id="fafa5-197">Blue cable</span></span>    |

<span data-ttu-id="fafa5-198">Cliquez sur tooview [framboises Pi 2 et 3 mappages de code confidentiel](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) de référence.</span><span class="sxs-lookup"><span data-stu-id="fafa5-198">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="fafa5-199">Une fois que vous avez connecté BME280 tooyour framboises Pi, elle doit être comme sous l’image.</span><span class="sxs-lookup"><span data-stu-id="fafa5-199">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Pi et BME280 connectés](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="fafa5-201">Connecter Pi toohello réseau</span><span class="sxs-lookup"><span data-stu-id="fafa5-201">Connect Pi toohello network</span></span>

<span data-ttu-id="fafa5-202">Pi sous tension à l’aide de câble USB micro de hello et alimentation hello.</span><span class="sxs-lookup"><span data-stu-id="fafa5-202">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="fafa5-203">Utilisez hello Ethernet câble tooconnect Pi tooyour câblé réseau ou suivez hello [instructions hello framboises Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) réseau sans fil de tooconnect Pi tooyour.</span><span class="sxs-lookup"><span data-stu-id="fafa5-203">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="fafa5-204">Une fois votre Pi a été correctement connecté toohello réseau, vous devez tootake note de hello [adresse IP de votre Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="fafa5-204">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Réseau de toowired connecté](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="fafa5-206">Exécuter un exemple d’application sur Pi</span><span class="sxs-lookup"><span data-stu-id="fafa5-206">Run a sample application on Pi</span></span>

### <a name="install-hello-prerequisite-packages"></a><span data-ttu-id="fafa5-207">Installer les packages de composants requis hello</span><span class="sxs-lookup"><span data-stu-id="fafa5-207">Install hello prerequisite packages</span></span>

1. <span data-ttu-id="fafa5-208">Utilisez une des hello suivant clients SSH à partir de votre ordinateur hôte ordinateur tooconnect tooyour framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="fafa5-208">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="fafa5-209">**Utilisateurs Windows**</span><span class="sxs-lookup"><span data-stu-id="fafa5-209">**Windows Users**</span></span>
   1. <span data-ttu-id="fafa5-210">Téléchargez et installez [PuTTY](http://www.putty.org/) pour Windows.</span><span class="sxs-lookup"><span data-stu-id="fafa5-210">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="fafa5-211">Copier l’adresse IP de hello de votre section Pi dans hello hôte nom (ou adresse IP) et sélectionnez SSH en tant que type de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="fafa5-211">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="fafa5-213">**Utilisateurs Mac et Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="fafa5-213">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="fafa5-214">Utilisez hello intégré client SSH sur Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="fafa5-214">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="fafa5-215">Vous devrez peut-être toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span><span class="sxs-lookup"><span data-stu-id="fafa5-215">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="fafa5-216">nom d’utilisateur par défaut de Hello est `pi` , et le mot de passe hello est `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="fafa5-216">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="fafa5-217">Installer les packages de composants requis hello pour hello Kit de développement logiciel de Microsoft Azure IoT appareil pour C et Cmake par hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="fafa5-217">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C and Cmake by running hello following commands:</span></span>

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


### <a name="configure-hello-sample-application"></a><span data-ttu-id="fafa5-218">Configurer l’application d’exemple hello</span><span class="sxs-lookup"><span data-stu-id="fafa5-218">Configure hello sample application</span></span>

1. <span data-ttu-id="fafa5-219">Pour cloner l’exemple d’application hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fafa5-219">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. <span data-ttu-id="fafa5-220">Ouvrez le fichier de configuration de hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="fafa5-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Fichier de configuration](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   <span data-ttu-id="fafa5-222">Deux éléments de type macros peuvent être configurés dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="fafa5-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="fafa5-223">Bonjour tout d’abord un est `INTERVAL`, qui définit l’intervalle de temps hello (en millisecondes) entre les deux messages toocloud d’envoi.</span><span class="sxs-lookup"><span data-stu-id="fafa5-223">hello first one is `INTERVAL`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="fafa5-224">Hello deuxième `SIMULATED_DATA`, qui est une valeur booléenne pour toouse indique si les données de capteur simulé ou non.</span><span class="sxs-lookup"><span data-stu-id="fafa5-224">hello second one `SIMULATED_DATA`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="fafa5-225">Si vous **n’avez pas capteur de hello**, affectez la valeur hello `SIMULATED_DATA` valeur trop`1` toomake hello exemple d’application, créer et utiliser des données de capteur simulé.</span><span class="sxs-lookup"><span data-stu-id="fafa5-225">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`1` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="fafa5-226">Enregistrez et quittez en appuyant sur Ctrl-O > Entrée > Ctrl-X.</span><span class="sxs-lookup"><span data-stu-id="fafa5-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="fafa5-227">Générer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="fafa5-227">Build and run hello sample application</span></span>

1. <span data-ttu-id="fafa5-228">Générer l’exemple d’application hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fafa5-228">Build hello sample application by running hello following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Sortie de la génération](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. <span data-ttu-id="fafa5-230">Exécuter l’exemple d’application hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fafa5-230">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="fafa5-231">Assurez-vous que vous copier-coller chaîne de connexion de périphérique hello dans des guillemets simples de hello.</span><span class="sxs-lookup"><span data-stu-id="fafa5-231">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="fafa5-232">Vous devez voir qu’affiche hello messages hello et les données de capteur envoyés tooyour IoT hub de sortie suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="fafa5-232">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Sortie - données de capteur envoyés à partir de framboises Pi tooyour IoT hub](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="fafa5-234">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fafa5-234">Next steps</span></span>

<span data-ttu-id="fafa5-235">Vous avez exécuté un exemple de données de capteur application toocollect et envoyez tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="fafa5-235">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="fafa5-236">messages de type hello toosee que votre Pi framboises a envoyé tooyour IoT hub ou envoyer des messages tooyour framboises Pi dans une interface de ligne de commande, consultez hello [gérer cloud appareil avec iothub-didacticiel de messagerie](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="fafa5-236">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
