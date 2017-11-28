---
title: "M0 toocloud : connexion Wi-Fi de contour M0 tooAzure IoT Hub | Documents Microsoft"
description: "Découvrez comment tooset configurer et connecter Adafruit estompe M0 WiFi tooAzure plateforme de cloud computing Azure IoT Hub toosend données toohello dans ce didacticiel."
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
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="1d5b5-103">Connexion Wi-Fi de Adafruit estompe M0 tooAzure IoT Hub dans le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="1d5b5-103">Connect Adafruit Feather M0 WiFi tooAzure IoT Hub in hello cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connexion entre un capteur BME280, une carte Feather M0 WiFi et IoT Hub](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="1d5b5-105">Dans ce didacticiel, commencer par découvrir hello les bases de l’utilisation de votre tableau Arduino.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-105">In this tutorial, you begin by learning hello basics of working with your Arduino board.</span></span> <span data-ttu-id="1d5b5-106">Vous apprendrez ensuite comment tooseamlessly connecter votre cloud toohello de périphériques à l’aide de [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="1d5b5-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="1d5b5-107">Procédure</span><span class="sxs-lookup"><span data-stu-id="1d5b5-107">What you do</span></span>

<span data-ttu-id="1d5b5-108">Connexion Wi-Fi de Adafruit estompe M0 tooan IoT hub que vous créez.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-108">Connect Adafruit Feather M0 WiFi tooan IoT hub that you create.</span></span> <span data-ttu-id="1d5b5-109">Puis, vous exécutez un exemple d’application sur Wi-Fi M0 toocollect hello température et humidité les données à partir d’un BME280.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-109">Then you run a sample application on M0 WiFi toocollect hello temperature and humidity data from a BME280.</span></span> <span data-ttu-id="1d5b5-110">Enfin, vous envoyez le hub IoT tooyour hello capteur données.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-110">Finally, you send hello sensor data tooyour IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="1d5b5-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="1d5b5-111">What you learn</span></span>

* <span data-ttu-id="1d5b5-112">Comment toocreate un IoT hub et inscrire un appareil pour le Wi-Fi de contour M0</span><span class="sxs-lookup"><span data-stu-id="1d5b5-112">How toocreate an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="1d5b5-113">Comment tooconnect estompe M0 WiFi avec capteur de hello et votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="1d5b5-113">How tooconnect Feather M0 WiFi with hello sensor and your computer</span></span>
* <span data-ttu-id="1d5b5-114">Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur le contour M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="1d5b5-114">How toocollect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="1d5b5-115">Comment toosend hello tooyour IoT hub capteur données</span><span class="sxs-lookup"><span data-stu-id="1d5b5-115">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1d5b5-116">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="1d5b5-116">What you need</span></span>

![Parties nécessaires pour hello didacticiel.](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="1d5b5-118">toocomplete cette opération, vous devez hello pièces suivantes à partir de votre Starter Kit de contour M0 Wi-Fi :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-118">toocomplete this operation, you need hello following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="1d5b5-119">Hello estompe M0 WiFi tableau</span><span class="sxs-lookup"><span data-stu-id="1d5b5-119">hello Feather M0 WiFi board</span></span>
* <span data-ttu-id="1d5b5-120">Un câble USB d’un de tooType Micro USB</span><span class="sxs-lookup"><span data-stu-id="1d5b5-120">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="1d5b5-121">Vous devez également hello suivant choses pour votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-121">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="1d5b5-122">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-122">An active Azure subscription.</span></span> <span data-ttu-id="1d5b5-123">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="1d5b5-124">Un Mac ou un PC exécutant Windows ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="1d5b5-125">Un réseau sans fil pour tooconnect estompe M0 WiFi à.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-125">A wireless network for Feather M0 WiFi tooconnect to.</span></span>
* <span data-ttu-id="1d5b5-126">Un outil de configuration Internet connexion toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-126">An Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="1d5b5-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="1d5b5-128">Les versions antérieures ne fonctionnent pas avec la bibliothèque de Azure IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-128">Earlier versions don't work with hello Azure IoT Hub library.</span></span>

<span data-ttu-id="1d5b5-129">Si vous n’avez pas un capteur, hello éléments suivants est facultatif.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-129">If you don’t have a sensor, hello following items are optional.</span></span> <span data-ttu-id="1d5b5-130">Vous avez également option hello d’utilisation des données de capteur simulée :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-130">You also have hello option of using simulated sensor data:</span></span>

* <span data-ttu-id="1d5b5-131">Un capteur de température et d’humidité BME280</span><span class="sxs-lookup"><span data-stu-id="1d5b5-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="1d5b5-132">Une platine d’expérimentation</span><span class="sxs-lookup"><span data-stu-id="1d5b5-132">A breadboard</span></span>
* <span data-ttu-id="1d5b5-133">Des câbles de liaison M/M</span><span class="sxs-lookup"><span data-stu-id="1d5b5-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a><span data-ttu-id="1d5b5-134">Connexion Wi-Fi de contour M0 avec capteur de hello et votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="1d5b5-134">Connect Feather M0 WiFi with hello sensor and your computer</span></span>
<span data-ttu-id="1d5b5-135">Dans cette section, vous vous connectez tooyour du tableau capteurs de hello.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-135">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="1d5b5-136">Puis vous connectez votre ordinateur tooyour de périphérique pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-136">Then you plug in your device tooyour computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a><span data-ttu-id="1d5b5-137">Se connecter à un DHT22 température et humidité capteur tooFeather Wi-Fi M0</span><span class="sxs-lookup"><span data-stu-id="1d5b5-137">Connect a DHT22 temperature and humidity sensor tooFeather M0 WiFi</span></span>

<span data-ttu-id="1d5b5-138">Utilisez hello breadboard et cavaliers fils toomake hello la connexion.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-138">Use hello breadboard and jumper wires toomake hello connection.</span></span> <span data-ttu-id="1d5b5-139">Si vous n’avez pas de capteur, ignorez cette section. Vous pourrez utiliser des données de capteur simulées à la place.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Schéma des connexions](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="1d5b5-141">Pour les codes confidentiels de capteur, utilisez hello suivant câblage :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-141">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="1d5b5-142">Début (capteur)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-142">Start (sensor)</span></span>           | <span data-ttu-id="1d5b5-143">Fin (carte)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-143">End (board)</span></span>            | <span data-ttu-id="1d5b5-144">Couleur du câble</span><span class="sxs-lookup"><span data-stu-id="1d5b5-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="1d5b5-145">VDD (broche 27A)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="1d5b5-146">3V (broche 3A)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="1d5b5-147">Câble rouge</span><span class="sxs-lookup"><span data-stu-id="1d5b5-147">Red cable</span></span>     |
| <span data-ttu-id="1d5b5-148">GND (broche 29A)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="1d5b5-149">GND (broche 6A)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="1d5b5-150">Câble noir</span><span class="sxs-lookup"><span data-stu-id="1d5b5-150">Black cable</span></span>   |
| <span data-ttu-id="1d5b5-151">SCK (broche 30A)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="1d5b5-152">SCK (broche 12A)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="1d5b5-153">Câble jaune</span><span class="sxs-lookup"><span data-stu-id="1d5b5-153">Yellow cable</span></span>  |
| <span data-ttu-id="1d5b5-154">SDO (broche 31A)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="1d5b5-155">MI (broche 14A)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="1d5b5-156">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="1d5b5-156">White cable</span></span>   |
| <span data-ttu-id="1d5b5-157">SDI (broche 32A)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="1d5b5-158">M0 (broche 13A)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="1d5b5-159">Câble bleu</span><span class="sxs-lookup"><span data-stu-id="1d5b5-159">Blue cable</span></span>    |
| <span data-ttu-id="1d5b5-160">CS (broche 33A)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="1d5b5-161">GPIO 5 (broche 15J)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="1d5b5-162">Câble orange</span><span class="sxs-lookup"><span data-stu-id="1d5b5-162">Orange cable</span></span>  |

<span data-ttu-id="1d5b5-163">Pour plus d’informations, consultez [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) (Atelier sur le capteur de température, de pression barométrique et d’humidité Adafruit BME280) et [Adafruit Feather M0 WiFi Pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts) (Brochages de la carte Adafruit Feather M0 WiFi).</span><span class="sxs-lookup"><span data-stu-id="1d5b5-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="1d5b5-164">Votre carte Feather M0 WiFi devrait à présent être connectée à un capteur opérationnel.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![Connexion du capteur DHT22 à la carte Feather Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a><span data-ttu-id="1d5b5-166">Connexion Wi-Fi de contour M0 tooyour ordinateur</span><span class="sxs-lookup"><span data-stu-id="1d5b5-166">Connect Feather M0 WiFi tooyour computer</span></span>

<span data-ttu-id="1d5b5-167">Utilisez hello Micro tooType USB d’un câble tooconnect estompe M0 WiFi tooyour ordinateur USB, comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-167">Use hello Micro USB tooType A USB cable tooconnect Feather M0 WiFi tooyour computer, as shown:</span></span>

![Estompe Huzzah tooyour ordinateur connecté](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="1d5b5-169">Ajouter des autorisations de port série (Ubuntu uniquement)</span><span class="sxs-lookup"><span data-stu-id="1d5b5-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="1d5b5-170">Si vous utilisez Ubuntu, assurez-vous que vous avez hello autorisations toooperate sur hello USB port de contour M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-170">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="1d5b5-171">autorisations de port série tooadd, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-171">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="1d5b5-172">À un terminal, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-172">At a terminal, run hello following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="1d5b5-173">Vous obtenez hello suivant sorties :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-173">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="1d5b5-174">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="1d5b5-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="1d5b5-175">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="1d5b5-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="1d5b5-176">Dans la sortie de hello, notez que `uucp` ou `dialout` est le nom du propriétaire de groupe de hello port USB hello.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-176">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

2. <span data-ttu-id="1d5b5-177">tooadd hello toohello groupe d’utilisateurs, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-177">tooadd hello user toohello group, run hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="1d5b5-178">Dans l’étape précédente de hello, vous avez obtenu le nom du propriétaire du groupe hello `<group-owner-name>`.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-178">In hello previous step, you obtained hello group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="1d5b5-179">Votre nom d’utilisateur Ubuntu est `<username>`.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="1d5b5-180">Pour hello modification tooappear, déconnectez-vous d’Ubuntu et puis reconnectez-vous.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-180">For hello change tooappear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="1d5b5-181">Collecter des données de capteur et les envoyer tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="1d5b5-181">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="1d5b5-182">Dans cette section, vous allez déployer et exécuter un exemple d’application sur la carte Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="1d5b5-183">exemple d’application Hello rend hello blink LED sur estompe M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-183">hello sample application makes hello LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="1d5b5-184">Il envoie ensuite la température de hello et données de l’humidité collectés hello BME280 capteur tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-184">It then sends hello temperature and humidity data collected from hello BME280 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a><span data-ttu-id="1d5b5-185">Obtenir un exemple d’application hello à partir de GitHub et préparer hello Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="1d5b5-185">Get hello sample application from GitHub and prepare hello Arduino IDE</span></span>

<span data-ttu-id="1d5b5-186">exemple d’application Hello est hébergé sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-186">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="1d5b5-187">Clonez le dépôt d’exemples hello qui contient l’exemple d’application hello à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-187">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="1d5b5-188">dépôt d’exemples tooclone hello, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-188">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="1d5b5-189">Ouvrez une invite de commandes ou une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="1d5b5-190">Accédez tooa dossier dans lequel toobe d’application exemple hello stockée.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-190">Go tooa folder where you want hello sample application toobe stored.</span></span>
3. <span data-ttu-id="1d5b5-191">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-191">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a><span data-ttu-id="1d5b5-192">Installer hello pour le Wi-Fi de contour M0 Bonjour Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="1d5b5-192">Install hello package for Feather M0 WiFi in hello Arduino IDE</span></span>

1. <span data-ttu-id="1d5b5-193">Ouvrez le dossier hello où l’application d’exemple hello est stockée.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-193">Open hello folder where hello sample application is stored.</span></span>

2. <span data-ttu-id="1d5b5-194">Ouvrez le fichier de app.ino de hello dans le dossier de l’application hello Bonjour Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-194">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Ouvrez l’application d’exemple hello dans Arduino IDE](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="1d5b5-196">Cliquez sur **fichier** > **préférences** (Windows/Linux) ou **Arduino** > **préférences** (Mac) et la copie et Coller avec liaison ci-dessous hello en hello **URL du Gestionnaire de cartes supplémentaires** option Bonjour préférences Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste hello link below into hello **Additional Boards Manager URLs** option in hello Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="1d5b5-197">Cliquez sur **outils** > **tableau** > **Gestionnaire de cartes**, puis installez hello `Arduino SAMD Boards` version `1.6.2` ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-197">Click **Tools** > **Board** > **Boards Manager**, and then install hello `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="1d5b5-198">Ensuite, dans hello même fenêtre, installez `Adafruit SAMD Boards` définitions de fichier de carte tooadd hello du package.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-198">Then in hello same window, install `Adafruit SAMD Boards` package tooadd hello board file definitions.</span></span>

   ![Hello esp8266 package est installé](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="1d5b5-200">Cliquez sur **Outils** > **Carte** > **Adafruit M0 WiFi**.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="1d5b5-201">Installez les pilotes (pour Windows uniquement).</span><span class="sxs-lookup"><span data-stu-id="1d5b5-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="1d5b5-202">Lorsque vous branchez estompe M0 WiFi, vous devrez peut-être tooinstall un pilote.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-202">When you plug in Feather M0 WiFi, you might need tooinstall a driver.</span></span> <span data-ttu-id="1d5b5-203">Cliquez sur [hello lien de téléchargement sur la page Web de hello](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) programme d’installation du pilote toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-203">Click [hello download link on hello webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello driver installer.</span></span> <span data-ttu-id="1d5b5-204">Suivez hello étapes tooinstall hello pilotes.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-204">Follow hello steps tooinstall hello drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="1d5b5-205">Installer les bibliothèques nécessaires</span><span class="sxs-lookup"><span data-stu-id="1d5b5-205">Install necessary libraries</span></span>

1. <span data-ttu-id="1d5b5-206">Bonjour Arduino IDE, cliquez sur **multiensembles** > **inclure une bibliothèque** > **gérer les bibliothèques**.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-206">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="1d5b5-207">Rechercher le nom de bibliothèque un par un.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-207">Search for hello following library names one by one.</span></span> <span data-ttu-id="1d5b5-208">Pour chacune des bibliothèques trouvées, cliquez sur **Installer** :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="1d5b5-209">Installez manuellement `Adafruit_WINC1500`.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="1d5b5-210">Accédez trop[ce site Web](https://github.com/adafruit/Adafruit_WINC1500) et cliquez sur **Clone ou téléchargement** > **ZIP de téléchargement**.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-210">Go too[this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="1d5b5-211">Dans votre IDE Arduino, passez trop**multiensembles** > **inclure une bibliothèque** > **ajouter .zip bibliothèque** et ajoutez le fichier zip de hello.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-211">Then in your Arduino IDE, go too**Sketch** > **Include Library** > **Add .zip Library** and add hello zip file.</span></span>

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="1d5b5-212">Utilisez l’exemple d’application hello si vous n’avez pas un capteur BME280 réel</span><span class="sxs-lookup"><span data-stu-id="1d5b5-212">Use hello sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="1d5b5-213">Si vous n’avez pas un capteur BME280 réel, exemple d’application hello permettre simuler des données de la température et humidité.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-213">If you don’t have a real BME280 sensor, hello sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="1d5b5-214">tooset des données toouse simulée l’application exemple hello, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-214">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="1d5b5-215">Ouvrez hello `config.h` fichier Bonjour `app` dossier.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-215">Open hello `config.h` file in hello `app` folder.</span></span>

2. <span data-ttu-id="1d5b5-216">Recherchez hello ligne de code suivante et remplacez valeur hello `false` trop`true`:</span><span class="sxs-lookup"><span data-stu-id="1d5b5-216">Locate hello following line of code and change hello value from `false` too`true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![Configurer hello exemples application toouse simulée de données](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="1d5b5-218">Enregistrez le fichier hello avec `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-218">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a><span data-ttu-id="1d5b5-219">Déployer hello exemple application tooFeather Wi-Fi M0</span><span class="sxs-lookup"><span data-stu-id="1d5b5-219">Deploy hello sample application tooFeather M0 WiFi</span></span>

1. <span data-ttu-id="1d5b5-220">Bonjour Arduino IDE, cliquez sur **outil** > **Port**, puis cliquez sur les ports série hello pour le Wi-Fi de contour M0.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-220">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="1d5b5-221">Cliquez sur **multiensembles** > **télécharger** toobuild et déployer hello exemple application tooFeather Wi-Fi M0.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-221">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="1d5b5-222">Entrer vos informations d’identification</span><span class="sxs-lookup"><span data-stu-id="1d5b5-222">Enter your credentials</span></span>

<span data-ttu-id="1d5b5-223">Après avoir hello téléchargement se termine correctement, suivez ces étapes tooenter vos informations d’identification :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-223">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="1d5b5-224">Bonjour Arduino IDE, cliquez sur **outils** > **moniteur série**.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-224">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="1d5b5-225">Dans hello bas à droite de fenêtre du moniteur série hello, sélectionnez **aucun guillemet de fin de ligne** dans la liste déroulante de hello sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-225">In hello lower-right corner of hello serial monitor window, select **No line ending** in hello drop-down list on hello left.</span></span>
3. <span data-ttu-id="1d5b5-226">Sélectionnez **115 200 bauds** dans la liste déroulante hello hello droite.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-226">Select **115200 baud** in hello drop-down list on hello right.</span></span>
4. <span data-ttu-id="1d5b5-227">Dans la zone d’entrée de hello haut hello, entrez hello informations suivantes si vous êtes invité tooprovide, puis cliquez sur **envoyer**:</span><span class="sxs-lookup"><span data-stu-id="1d5b5-227">In hello input box at hello top, enter hello following information if you're asked tooprovide it, and click **Send**:</span></span>

   * <span data-ttu-id="1d5b5-228">SSID Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="1d5b5-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="1d5b5-229">Mot de passe Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="1d5b5-229">Wi-Fi password</span></span>
   * <span data-ttu-id="1d5b5-230">Chaîne de connexion de l’appareil</span><span class="sxs-lookup"><span data-stu-id="1d5b5-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="1d5b5-231">informations d’identification de Hello sont stockées dans hello EEPROM de contour M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-231">hello credential information is stored in hello EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="1d5b5-232">Si vous cliquez sur le bouton Réinitialiser hello hello estompe M0 WiFi tableau, exemple d’application hello vous demande si vous souhaitez que les informations de hello tooerase.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-232">If you click hello reset button on hello Feather M0 WiFi board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="1d5b5-233">Entrez `Y` plus d’informations tooerase hello.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-233">Enter `Y` tooerase hello information.</span></span> <span data-ttu-id="1d5b5-234">Vous devez indiquer les informations de hello tooprovide une deuxième fois.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-234">You're asked tooprovide hello information a second time.</span></span>

### <a name="verify-that-hello-sample-application-is-running-successfully"></a><span data-ttu-id="1d5b5-235">Vérifiez que les application d’exemple hello s’exécute avec succès</span><span class="sxs-lookup"><span data-stu-id="1d5b5-235">Verify that hello sample application is running successfully</span></span>

<span data-ttu-id="1d5b5-236">Si vous voyez suivant de hello la sortie à partir de la fenêtre de l’analyseur série hello et hello clignote LED sur estompe M0 Wi-Fi, exemple d’application hello est exécuté avec succès :</span><span class="sxs-lookup"><span data-stu-id="1d5b5-236">If you see hello following output from hello serial monitor window and hello blinking LED on Feather M0 WiFi, hello sample application is running successfully:</span></span>

![Sortie finale dans l’IDE Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="1d5b5-238">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1d5b5-238">Next steps</span></span>

<span data-ttu-id="1d5b5-239">Vous avez connecté le Wi-Fi de contour M0 tooyour IoT hub et envoyé hello capturée capteur données tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1d5b5-239">You have successfully connected Feather M0 WiFi tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

