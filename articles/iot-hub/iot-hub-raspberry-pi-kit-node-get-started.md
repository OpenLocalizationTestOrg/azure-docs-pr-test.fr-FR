---
title: toocloud aaaRaspberry Pi (Node.js) - se connecter un Pi framboises tooAzure IoT Hub | Documents Microsoft
description: "Découvrez comment toosetup et connectez-vous framboises Pi tooAzure IoT Hub pour la plateforme de cloud computing Azure framboises Pi toosend données toohello dans ce didacticiel."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot raspberry pi, raspberry pi iot hub, raspberry pi envoi données toocloud, raspberry pi toocloud"
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 57a15ab3984021a9c18ff0aa1316a4d4c6ebdec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a><span data-ttu-id="81a93-104">Se connecter framboises Pi tooAzure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="81a93-104">Connect Raspberry Pi tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="81a93-105">Dans ce didacticiel, commencer par découvrir hello les bases de l’utilisation de Pi framboises qui Raspbian est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="81a93-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="81a93-106">Vous apprendrez ensuite comment tooseamlessly connecter votre cloud toohello de périphériques à l’aide de [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="81a93-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="81a93-107">Pour obtenir des exemples de Windows 10 IoT Core, accédez à toohello [centre de développement Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="81a93-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="81a93-108">Vous n’avez pas encore de kit ?</span><span class="sxs-lookup"><span data-stu-id="81a93-108">Don't have a kit yet?</span></span> <span data-ttu-id="81a93-109">Essayez [le simulateur en ligne Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="81a93-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="81a93-110">Ou achetez un nouveau kit [ici](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="81a93-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>


## <a name="what-you-do"></a><span data-ttu-id="81a93-111">Procédure</span><span class="sxs-lookup"><span data-stu-id="81a93-111">What you do</span></span>

* <span data-ttu-id="81a93-112">Créez un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="81a93-112">Create an IoT hub.</span></span>
* <span data-ttu-id="81a93-113">Inscrivez un appareil pour Pi dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="81a93-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="81a93-114">Configurez Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="81a93-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="81a93-115">Exécuter un exemple d’application sur le concentrateur de Pi toosend capteur données tooyour IoT.</span><span class="sxs-lookup"><span data-stu-id="81a93-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="81a93-116">Connectez framboises Pi tooan IoT concentrateur que vous créez.</span><span class="sxs-lookup"><span data-stu-id="81a93-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="81a93-117">Ensuite, vous exécutez un exemple d’application sur les données de température et humidité toocollect Pi à partir d’un capteur BME280.</span><span class="sxs-lookup"><span data-stu-id="81a93-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="81a93-118">Enfin, vous envoyez le hub IoT tooyour hello capteur données.</span><span class="sxs-lookup"><span data-stu-id="81a93-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="81a93-119">Contenu</span><span class="sxs-lookup"><span data-stu-id="81a93-119">What you learn</span></span>

* <span data-ttu-id="81a93-120">Comment toocreate un Azure IoT hub et obtenir votre nouvelle chaîne de connexion de périphérique.</span><span class="sxs-lookup"><span data-stu-id="81a93-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="81a93-121">Comment tooconnect Pi, avec un capteur BME280.</span><span class="sxs-lookup"><span data-stu-id="81a93-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="81a93-122">Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur Pi.</span><span class="sxs-lookup"><span data-stu-id="81a93-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="81a93-123">Comment le hub IoT tooyour toosend capteur données.</span><span class="sxs-lookup"><span data-stu-id="81a93-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="81a93-124">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="81a93-124">What you need</span></span>

![Ce dont vous avez besoin](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="81a93-126">Hello framboises Pi 2 ou 3 de Pi framboises du tableau.</span><span class="sxs-lookup"><span data-stu-id="81a93-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="81a93-127">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="81a93-127">An active Azure subscription.</span></span> <span data-ttu-id="81a93-128">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="81a93-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="81a93-129">Un moniteur, un clavier USB et la souris qui se connectent tooPi.</span><span class="sxs-lookup"><span data-stu-id="81a93-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="81a93-130">Un Mac ou un PC exécutant Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="81a93-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="81a93-131">Une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="81a93-131">An Internet connection.</span></span>
* <span data-ttu-id="81a93-132">Une carte microSD d’au moins 16 Go.</span><span class="sxs-lookup"><span data-stu-id="81a93-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="81a93-133">Une USB-SD carte microSD carte tooburn hello système d’exploitation image ou sur une carte microSD de hello.</span><span class="sxs-lookup"><span data-stu-id="81a93-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="81a93-134">Une puissance de 2-amp 5-v fournir avec un câble USB micro de hello 6-pied.</span><span class="sxs-lookup"><span data-stu-id="81a93-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="81a93-135">Hello éléments suivants est facultatif :</span><span class="sxs-lookup"><span data-stu-id="81a93-135">hello following items are optional:</span></span>

* <span data-ttu-id="81a93-136">Un capteur de température, de pression et d’humidité Adafruit BME280 assemblé.</span><span class="sxs-lookup"><span data-stu-id="81a93-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="81a93-137">Une platine d’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="81a93-137">A breadboard.</span></span>
* <span data-ttu-id="81a93-138">6 câbles de liaison F/M.</span><span class="sxs-lookup"><span data-stu-id="81a93-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="81a93-139">Une LED de 10 mm diffuse.</span><span class="sxs-lookup"><span data-stu-id="81a93-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="81a93-140">Ces éléments sont facultatifs, car la prise en charge des exemples de code hello simulée des données de capteur.</span><span class="sxs-lookup"><span data-stu-id="81a93-140">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="81a93-141">Configuration de Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="81a93-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="81a93-142">Installer le système d’exploitation de Raspbian hello de Pi</span><span class="sxs-lookup"><span data-stu-id="81a93-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="81a93-143">Préparer la carte microSD de hello pour l’installation de l’image de Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="81a93-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="81a93-144">Téléchargez Raspbian.</span><span class="sxs-lookup"><span data-stu-id="81a93-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="81a93-145">[Télécharger Raspbian Jessie avec le bureau](https://www.raspberrypi.org/downloads/raspbian/) (fichier .zip de hello).</span><span class="sxs-lookup"><span data-stu-id="81a93-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="81a93-146">Extraire le dossier de tooa hello Raspbian image sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="81a93-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="81a93-147">Installez Raspbian toohello microSD carte.</span><span class="sxs-lookup"><span data-stu-id="81a93-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="81a93-148">[Téléchargez et installez l’utilitaire graveur de hello Etcher SD carte](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="81a93-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="81a93-149">Exécutez Etcher et sélectionnez l’image Raspbian hello que vous avez extrait à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="81a93-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="81a93-150">Sélectionnez le lecteur de carte microSD hello.</span><span class="sxs-lookup"><span data-stu-id="81a93-150">Select hello microSD card drive.</span></span> <span data-ttu-id="81a93-151">Notez que Etcher peut avoir déjà sélectionné lecteur hello.</span><span class="sxs-lookup"><span data-stu-id="81a93-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="81a93-152">Cliquez sur le disque mémoire Flash tooinstall Raspbian toohello microSD carte.</span><span class="sxs-lookup"><span data-stu-id="81a93-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="81a93-153">Retirez hello microSD votre ordinateur lorsque l’installation est terminée.</span><span class="sxs-lookup"><span data-stu-id="81a93-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="81a93-154">Carte microSD de hello tooremove safe est directement car Etcher éjecte automatiquement ou démonte carte microSD de hello à l’achèvement.</span><span class="sxs-lookup"><span data-stu-id="81a93-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="81a93-155">Insérer carte microSD de hello Pi.</span><span class="sxs-lookup"><span data-stu-id="81a93-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="81a93-156">Activer SSH et I2C</span><span class="sxs-lookup"><span data-stu-id="81a93-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="81a93-157">Connecter le moniteur de toohello Pi, clavier et souris, démarrer Pi, puis Raspbian à l’aide de `pi` en tant que nom d’utilisateur hello et `raspberry` comme mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="81a93-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="81a93-158">Cliquez sur hello icône Raspberry > **préférences** > **framboises Pi Configuration**.</span><span class="sxs-lookup"><span data-stu-id="81a93-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![menu de préférences de Raspbian Hello](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="81a93-160">Sur hello **Interfaces** onglet, définissez **I2C** et **SSH** trop**activer**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="81a93-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="81a93-161">Si vous n’ayez des capteurs physiques et souhaitez que les données de capteur toouse simulée, cette étape est facultative.</span><span class="sxs-lookup"><span data-stu-id="81a93-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Activer I2C et SSH sur Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="81a93-163">tooenable SSH et I2C, vous trouverez plus de documents de référence sur [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) et [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="81a93-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="81a93-164">Se connecter hello capteur tooPi</span><span class="sxs-lookup"><span data-stu-id="81a93-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="81a93-165">Utilisez les fils de breadboard et cavaliers hello tooconnect une DEL et un tooPi BME280 comme suit.</span><span class="sxs-lookup"><span data-stu-id="81a93-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="81a93-166">Si vous n’avez capteur hello [ignorer cette section](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="81a93-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Hello framboises Pi et capteur de connexion](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="81a93-168">capteur de Hello BME280 pouvez collecter des données de température et humidité.</span><span class="sxs-lookup"><span data-stu-id="81a93-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="81a93-169">Et hello LED clignote s’il existe une communication entre l’appareil et hello cloud.</span><span class="sxs-lookup"><span data-stu-id="81a93-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="81a93-170">Pour les codes confidentiels de capteur, utilisez hello suivant câblage :</span><span class="sxs-lookup"><span data-stu-id="81a93-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="81a93-171">Début (capteur et LED)</span><span class="sxs-lookup"><span data-stu-id="81a93-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="81a93-172">Fin (carte)</span><span class="sxs-lookup"><span data-stu-id="81a93-172">End (Board)</span></span>            | <span data-ttu-id="81a93-173">Couleur du câble</span><span class="sxs-lookup"><span data-stu-id="81a93-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="81a93-174">VDD (broche 5G)</span><span class="sxs-lookup"><span data-stu-id="81a93-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="81a93-175">ALIM 3,3 V (broche 1)</span><span class="sxs-lookup"><span data-stu-id="81a93-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="81a93-176">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="81a93-176">White cable</span></span>   |
| <span data-ttu-id="81a93-177">GND (broche 7G)</span><span class="sxs-lookup"><span data-stu-id="81a93-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="81a93-178">GND (broche 6)</span><span class="sxs-lookup"><span data-stu-id="81a93-178">GND (Pin 6)</span></span>            | <span data-ttu-id="81a93-179">Câble marron</span><span class="sxs-lookup"><span data-stu-id="81a93-179">Brown cable</span></span>   |
| <span data-ttu-id="81a93-180">SDI (broche 10G)</span><span class="sxs-lookup"><span data-stu-id="81a93-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="81a93-181">I2C1 SDA (broche 3)</span><span class="sxs-lookup"><span data-stu-id="81a93-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="81a93-182">Câble rouge</span><span class="sxs-lookup"><span data-stu-id="81a93-182">Red cable</span></span>     |
| <span data-ttu-id="81a93-183">SCK (broche 8G)</span><span class="sxs-lookup"><span data-stu-id="81a93-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="81a93-184">I2C1 SCL (broche 5)</span><span class="sxs-lookup"><span data-stu-id="81a93-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="81a93-185">Câble orange</span><span class="sxs-lookup"><span data-stu-id="81a93-185">Orange cable</span></span>  |
| <span data-ttu-id="81a93-186">LED VDD (broche 18F)</span><span class="sxs-lookup"><span data-stu-id="81a93-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="81a93-187">GPIO 24 (broche 18)</span><span class="sxs-lookup"><span data-stu-id="81a93-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="81a93-188">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="81a93-188">White cable</span></span>   |
| <span data-ttu-id="81a93-189">LED GND (broche 17F)</span><span class="sxs-lookup"><span data-stu-id="81a93-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="81a93-190">GND (broche 20)</span><span class="sxs-lookup"><span data-stu-id="81a93-190">GND (Pin 20)</span></span>           | <span data-ttu-id="81a93-191">Câble noir</span><span class="sxs-lookup"><span data-stu-id="81a93-191">Black cable</span></span>   |

<span data-ttu-id="81a93-192">Cliquez sur tooview [framboises Pi 2 et 3 mappages de code confidentiel](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) de référence.</span><span class="sxs-lookup"><span data-stu-id="81a93-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="81a93-193">Une fois que vous avez connecté BME280 tooyour framboises Pi, elle doit être comme sous l’image.</span><span class="sxs-lookup"><span data-stu-id="81a93-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Pi et BME280 connectés](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="81a93-195">Connecter Pi toohello réseau</span><span class="sxs-lookup"><span data-stu-id="81a93-195">Connect Pi toohello network</span></span>

<span data-ttu-id="81a93-196">Pi sous tension à l’aide de câble USB micro de hello et alimentation hello.</span><span class="sxs-lookup"><span data-stu-id="81a93-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="81a93-197">Utilisez hello Ethernet câble tooconnect Pi tooyour câblé réseau ou suivez hello [instructions hello framboises Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) réseau sans fil de tooconnect Pi tooyour.</span><span class="sxs-lookup"><span data-stu-id="81a93-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="81a93-198">Une fois votre Pi a été correctement connecté toohello réseau, vous devez tootake note de hello [adresse IP de votre Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="81a93-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Réseau de toowired connecté](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="81a93-200">Assurez-vous que Pi est connecté toohello même réseau que votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="81a93-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="81a93-201">Par exemple, si votre ordinateur est connecté tooa les réseau sans fil pendant que Pi est connecté tooa réseau câblé, vous verrez ne peut-être pas hello IP adresse dans la sortie de devdisco hello.</span><span class="sxs-lookup"><span data-stu-id="81a93-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="81a93-202">Exécuter un exemple d’application sur Pi</span><span class="sxs-lookup"><span data-stu-id="81a93-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a><span data-ttu-id="81a93-203">Cloner l’exemple d’application et installer les packages de composants requis hello</span><span class="sxs-lookup"><span data-stu-id="81a93-203">Clone sample application and install hello prerequisite packages</span></span>

1. <span data-ttu-id="81a93-204">Utilisez une des hello suivant clients SSH à partir de votre ordinateur hôte ordinateur tooconnect tooyour framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="81a93-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="81a93-205">**Utilisateurs Windows**</span><span class="sxs-lookup"><span data-stu-id="81a93-205">**Windows Users**</span></span>
   1. <span data-ttu-id="81a93-206">Téléchargez et installez [PuTTY](http://www.putty.org/) pour Windows.</span><span class="sxs-lookup"><span data-stu-id="81a93-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="81a93-207">Copier l’adresse IP de hello de votre section Pi dans hello hôte nom (ou adresse IP) et sélectionnez SSH en tant que type de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="81a93-207">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="81a93-209">**Utilisateurs Mac et Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="81a93-209">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="81a93-210">Utilisez hello intégré client SSH sur Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="81a93-210">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="81a93-211">Vous devrez peut-être toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span><span class="sxs-lookup"><span data-stu-id="81a93-211">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="81a93-212">nom d’utilisateur par défaut de Hello est `pi` , et le mot de passe hello est `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="81a93-212">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="81a93-213">Installation de Node.js et NPM tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="81a93-213">Install Node.js and NPM tooyour Pi.</span></span>
   
   <span data-ttu-id="81a93-214">Tout d’abord, vous devez vérifier votre version de Node.js avec hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="81a93-214">First you should check your Node.js version with hello following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="81a93-215">Version de hello est inférieure à 4.x ou s’il n’existe aucune Node.js sur votre Pi, puis exécutez hello suivant tooinstall de commande ou de mettre à jour de Node.js.</span><span class="sxs-lookup"><span data-stu-id="81a93-215">If hello version is lower than 4.x or there is no Node.js on your Pi, then run hello following command tooinstall or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="81a93-216">Pour cloner l’exemple d’application hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="81a93-216">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="81a93-217">Installez tous les packages en hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="81a93-217">Install all packages by hello following command.</span></span> <span data-ttu-id="81a93-218">Cela inclut Azure IoT device SDK, la bibliothèque de capteur BME280 et la bibliothèque de câblage de Pi.</span><span class="sxs-lookup"><span data-stu-id="81a93-218">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="81a93-219">Il peut prendre plusieurs minutes toofinish ce processus d’installation en fonction de votre connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="81a93-219">It might take several minutes toofinish this installation process depending on your network connection.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="81a93-220">Configurer l’application d’exemple hello</span><span class="sxs-lookup"><span data-stu-id="81a93-220">Configure hello sample application</span></span>

1. <span data-ttu-id="81a93-221">Ouvrez le fichier de configuration de hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="81a93-221">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Fichier de configuration](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="81a93-223">Deux éléments peuvent être configurés dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="81a93-223">There are two items in this file you can configurate.</span></span> <span data-ttu-id="81a93-224">Bonjour tout d’abord un est `interval`, qui définit l’intervalle de temps hello (en millisecondes) entre les deux messages toocloud d’envoi.</span><span class="sxs-lookup"><span data-stu-id="81a93-224">hello first one is `interval`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="81a93-225">Hello deuxième `simulatedData`, qui est une valeur booléenne pour toouse indique si les données de capteur simulé ou non.</span><span class="sxs-lookup"><span data-stu-id="81a93-225">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="81a93-226">Si vous **n’avez pas capteur de hello**, affectez la valeur hello `simulatedData` valeur trop`true` toomake hello exemple d’application, créer et utiliser des données de capteur simulé.</span><span class="sxs-lookup"><span data-stu-id="81a93-226">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="81a93-227">Enregistrez et quittez en appuyant sur Ctrl-O > Entrée > Ctrl-X.</span><span class="sxs-lookup"><span data-stu-id="81a93-227">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="81a93-228">Exécutez l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="81a93-228">Run hello sample application</span></span>

<span data-ttu-id="81a93-229">Exécuter l’exemple d’application hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="81a93-229">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<YOUR AZURE IOT HUB DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="81a93-230">Assurez-vous que vous copier-coller chaîne de connexion de périphérique hello dans des guillemets simples de hello.</span><span class="sxs-lookup"><span data-stu-id="81a93-230">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="81a93-231">Vous devez voir qu’affiche hello messages hello et les données de capteur envoyés tooyour IoT hub de sortie suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="81a93-231">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Sortie - données de capteur envoyés à partir de framboises Pi tooyour IoT hub](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="81a93-233">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="81a93-233">Next steps</span></span>

<span data-ttu-id="81a93-234">Vous avez exécuté un exemple de données de capteur application toocollect et envoyez tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="81a93-234">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="81a93-235">messages de type hello toosee que votre Pi framboises a envoyé tooyour IoT hub ou envoyer des messages tooyour framboises Pi dans une interface de ligne de commande, consultez hello [gérer cloud appareil avec iothub-didacticiel de messagerie](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="81a93-235">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
