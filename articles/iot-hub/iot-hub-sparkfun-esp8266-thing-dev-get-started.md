---
title: aaaESP8266 toocloud - se connecter Sparkfun ESP8266 chose Dev tooAzure IoT Hub | Documents Microsoft
description: "Découvrez comment toosetup et connectez-vous de plateforme de cloud computing Azure toosend données toohello Sparkfun ESP8266 chose Dev tooAzure IoT Hub pour qu’il dans ce didacticiel."
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
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="4e4df-103">Se connecter Sparkfun ESP8266 chose Dev tooAzure IoT Hub dans le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="4e4df-103">Connect Sparkfun ESP8266 Thing Dev tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![connexion entre un capteur DHT22, Thing Dev et IoT Hub](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="4e4df-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="4e4df-105">What you will do</span></span>

<span data-ttu-id="4e4df-106">Se connecter Sparkfun ESP8266 chose Dev tooan IoT hub, que vous allez créer.</span><span class="sxs-lookup"><span data-stu-id="4e4df-106">Connect Sparkfun ESP8266 Thing Dev tooan IoT hub you will create.</span></span> <span data-ttu-id="4e4df-107">Puis exécutez un exemple d’application sur les données de température et humidité toocollect ESP8266 à partir d’un capteur DHT22.</span><span class="sxs-lookup"><span data-stu-id="4e4df-107">Then run a sample application on ESP8266 toocollect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="4e4df-108">Enfin, envoyez le hub IoT tooyour hello capteur données.</span><span class="sxs-lookup"><span data-stu-id="4e4df-108">Finally, send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="4e4df-109">Si vous utilisez des autres cartes ESP8266, vous pouvez toujours suivre ces étapes tooconnect il tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4e4df-109">If you are using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="4e4df-110">Selon la carte hello ESP8266 que vous utilisez, vous devrez peut-être tooreconfigure hello `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="4e4df-110">Depending on hello ESP8266 board you are using, you may need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="4e4df-111">Par exemple, si vous utilisez ESP8266 de AI-Thinker, vous pouvez le changer à partir de `0` trop`2`.</span><span class="sxs-lookup"><span data-stu-id="4e4df-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` too`2`.</span></span> <span data-ttu-id="4e4df-112">Vous n’avez pas encore de kit ? Cliquez [ici](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="4e4df-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4e4df-113">Contenu</span><span class="sxs-lookup"><span data-stu-id="4e4df-113">What you will learn</span></span>

* <span data-ttu-id="4e4df-114">Comment toocreate un IoT hub et inscrire un appareil d’espace réservé de chose pour</span><span class="sxs-lookup"><span data-stu-id="4e4df-114">How toocreate an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="4e4df-115">Comment tooconnect chose Dev avec capteur de hello et votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4e4df-115">How tooconnect Thing Dev with hello sensor and your computer.</span></span>
* <span data-ttu-id="4e4df-116">Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur l’élément réservé</span><span class="sxs-lookup"><span data-stu-id="4e4df-116">How toocollect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="4e4df-117">Comment toosend hello tooyour IoT hub capteur données.</span><span class="sxs-lookup"><span data-stu-id="4e4df-117">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="4e4df-118">Éléments requis</span><span class="sxs-lookup"><span data-stu-id="4e4df-118">What you will need</span></span>

![Parties nécessaires pour hello didacticiel.](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="4e4df-120">toocomplete cette opération, vous devez hello pièces suivantes à partir de votre Starter Kit de développement de chose :</span><span class="sxs-lookup"><span data-stu-id="4e4df-120">toocomplete this operation, you need hello following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="4e4df-121">Hello Sparkfun ESP8266 chose Dev tableau.</span><span class="sxs-lookup"><span data-stu-id="4e4df-121">hello Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="4e4df-122">Un Micro USB tooType un câble.</span><span class="sxs-lookup"><span data-stu-id="4e4df-122">A Micro USB tooType A USB cable.</span></span>

<span data-ttu-id="4e4df-123">Éléments de hello suivants sont également nécessaires pour votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="4e4df-123">You also need hello following for your development environment:</span></span>

* <span data-ttu-id="4e4df-124">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="4e4df-124">An active Azure subscription.</span></span> <span data-ttu-id="4e4df-125">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4e4df-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="4e4df-126">Un Mac ou un PC exécutant Windows ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="4e4df-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="4e4df-127">Réseau sans fil pour tooconnect Sparkfun ESP8266 chose Dev à.</span><span class="sxs-lookup"><span data-stu-id="4e4df-127">Wireless network for Sparkfun ESP8266 Thing Dev tooconnect to.</span></span>
* <span data-ttu-id="4e4df-128">Outil de configuration Internet connexion toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="4e4df-128">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="4e4df-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (ou ultérieure), les versions antérieures ne fonctionnent pas avec la bibliothèque de AzureIoT hello.</span><span class="sxs-lookup"><span data-stu-id="4e4df-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with hello AzureIoT library.</span></span>

<span data-ttu-id="4e4df-130">Hello éléments suivants sont facultatifs au cas où vous n’avez pas un capteur.</span><span class="sxs-lookup"><span data-stu-id="4e4df-130">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="4e4df-131">Vous avez également option hello d’utilisation des données de capteur simulé.</span><span class="sxs-lookup"><span data-stu-id="4e4df-131">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="4e4df-132">Un capteur de température et d’humidité Adafruit DHT22.</span><span class="sxs-lookup"><span data-stu-id="4e4df-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="4e4df-133">Une platine d’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="4e4df-133">A breadboard.</span></span>
* <span data-ttu-id="4e4df-134">Des câbles de liaison M/M.</span><span class="sxs-lookup"><span data-stu-id="4e4df-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a><span data-ttu-id="4e4df-135">Se connecter ESP8266 chose Dev avec capteur de hello et votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="4e4df-135">Connect ESP8266 Thing Dev with hello sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a><span data-ttu-id="4e4df-136">Se connecter à un capteur de température et humidité DHT22 tooESP8266 chose Dev</span><span class="sxs-lookup"><span data-stu-id="4e4df-136">Connect a DHT22 temperature and humidity sensor tooESP8266 Thing Dev</span></span>

<span data-ttu-id="4e4df-137">Utilisez hello breadboard et cavaliers fils toomake hello connexion comme suit.</span><span class="sxs-lookup"><span data-stu-id="4e4df-137">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="4e4df-138">Si vous n’avez pas de capteur, ignorez cette section. Vous pourrez utiliser des données de capteur simulées à la place.</span><span class="sxs-lookup"><span data-stu-id="4e4df-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Schéma des connexions](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="4e4df-140">Pour les codes confidentiels de capteur, nous allons utiliser hello suivant câblage :</span><span class="sxs-lookup"><span data-stu-id="4e4df-140">For sensor pins, we will use hello following wiring:</span></span>

| <span data-ttu-id="4e4df-141">Début (capteur)</span><span class="sxs-lookup"><span data-stu-id="4e4df-141">Start (Sensor)</span></span>           | <span data-ttu-id="4e4df-142">Fin (carte)</span><span class="sxs-lookup"><span data-stu-id="4e4df-142">End (Board)</span></span>           | <span data-ttu-id="4e4df-143">Couleur du câble</span><span class="sxs-lookup"><span data-stu-id="4e4df-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="4e4df-144">VDD (broche 27F)</span><span class="sxs-lookup"><span data-stu-id="4e4df-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="4e4df-145">3V (broche 8A)</span><span class="sxs-lookup"><span data-stu-id="4e4df-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="4e4df-146">Câble rouge</span><span class="sxs-lookup"><span data-stu-id="4e4df-146">Red cable</span></span>     |
| <span data-ttu-id="4e4df-147">DATA (broche 28F)</span><span class="sxs-lookup"><span data-stu-id="4e4df-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="4e4df-148">GPIO 2 (broche 9A)</span><span class="sxs-lookup"><span data-stu-id="4e4df-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="4e4df-149">Câble blanc</span><span class="sxs-lookup"><span data-stu-id="4e4df-149">White cable</span></span>    |
| <span data-ttu-id="4e4df-150">GND (broche 30F)</span><span class="sxs-lookup"><span data-stu-id="4e4df-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="4e4df-151">GND (broche 7J)</span><span class="sxs-lookup"><span data-stu-id="4e4df-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="4e4df-152">Câble noir</span><span class="sxs-lookup"><span data-stu-id="4e4df-152">Black cable</span></span>   |


- <span data-ttu-id="4e4df-153">Pour en savoir plus, consultez les [détails de la configuration du capteur DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) et les [spécifications relatives à la carte Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711).</span><span class="sxs-lookup"><span data-stu-id="4e4df-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="4e4df-154">Votre carte Sparkfun ESP8266 Thing Dev devrait à présent être connectée à un capteur opérationnel.</span><span class="sxs-lookup"><span data-stu-id="4e4df-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![connecter un capteur dht22 à la carte ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a><span data-ttu-id="4e4df-156">Se connecter Sparkfun ESP8266 chose Dev tooyour ordinateur</span><span class="sxs-lookup"><span data-stu-id="4e4df-156">Connect Sparkfun ESP8266 Thing Dev tooyour computer</span></span>

<span data-ttu-id="4e4df-157">Utilisez hello Micro USB tooType USB d’un câble tooconnect Sparkfun ESP8266 chose tooyour ordinateur Dev comme suit.</span><span class="sxs-lookup"><span data-stu-id="4e4df-157">Use hello Micro USB tooType A USB cable tooconnect Sparkfun ESP8266 Thing Dev tooyour computer as follows.</span></span>

![estompe huzzah tooyour ordinateur connecté](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="4e4df-159">Ajouter des autorisations de port série (Ubuntu uniquement)</span><span class="sxs-lookup"><span data-stu-id="4e4df-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="4e4df-160">Si vous utilisez Ubuntu, assurez-vous qu’utilisateur normal a hello autorisations toooperate sur hello USB port de Sparkfun ESP8266 chose dev.</span><span class="sxs-lookup"><span data-stu-id="4e4df-160">If you use Ubuntu, make sure a normal user has hello permissions toooperate on hello USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="4e4df-161">autorisations de port série tooadd pour un utilisateur normal, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4e4df-161">tooadd serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="4e4df-162">Exécutez hello suivant de commandes à partir d’un terminal :</span><span class="sxs-lookup"><span data-stu-id="4e4df-162">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="4e4df-163">Vous obtenez hello suivant sorties :</span><span class="sxs-lookup"><span data-stu-id="4e4df-163">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="4e4df-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="4e4df-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="4e4df-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="4e4df-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="4e4df-166">Dans la sortie de hello, notez `uucp` ou `dialout` qui est hello propriétaire du nom du groupe de hello port USB.</span><span class="sxs-lookup"><span data-stu-id="4e4df-166">In hello output, notice `uucp` or `dialout` that is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="4e4df-167">Ajouter groupe toohello hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4e4df-167">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="4e4df-168">`<group-owner-name>`est le nom de propriétaire de groupe de hello que vous avez obtenu à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="4e4df-168">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="4e4df-169">`<username>` est le nom de votre utilisateur Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="4e4df-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="4e4df-170">Fermez la session Ubuntu, qu’elle contient à nouveau pour modifier un effet de tootake hello.</span><span class="sxs-lookup"><span data-stu-id="4e4df-170">Log out Ubuntu and log in it again for hello change tootake effect.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="4e4df-171">Collecter des données de capteur et les envoyer tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="4e4df-171">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="4e4df-172">Dans cette section, vous allez déployer et exécuter un exemple d’application sur la carte Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="4e4df-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="4e4df-173">exemple d’application Hello clignote hello LED sur Sparkfun ESP8266 chose Dev et envoie la température de hello et les données de l’humidité collectés hello DHT22 capteur tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4e4df-173">hello sample application blinks hello LED on Sparkfun ESP8266 Thing Dev and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="4e4df-174">Obtenir un exemple d’application hello à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="4e4df-174">Get hello sample application from GitHub</span></span>

<span data-ttu-id="4e4df-175">exemple d’application Hello est hébergé sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="4e4df-175">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="4e4df-176">Clonez le dépôt d’exemples hello qui contient l’exemple d’application hello à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="4e4df-176">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="4e4df-177">dépôt d’exemples tooclone hello, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4e4df-177">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="4e4df-178">Ouvrez une invite de commandes ou une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="4e4df-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="4e4df-179">Accédez tooa dossier dans lequel toobe d’application exemple hello stockée.</span><span class="sxs-lookup"><span data-stu-id="4e4df-179">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="4e4df-180">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4e4df-180">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="4e4df-181">Installer le package de hello pour le développement de chose Sparkfun ESP8266 dans Arduino IDE :</span><span class="sxs-lookup"><span data-stu-id="4e4df-181">Install hello package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="4e4df-182">Ouvrez le dossier hello où l’application d’exemple hello est stockée.</span><span class="sxs-lookup"><span data-stu-id="4e4df-182">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="4e4df-183">Ouvrez le fichier de app.ino de hello dans le dossier de l’application hello dans Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="4e4df-183">Open hello app.ino file in hello app folder in Arduino IDE.</span></span>

   ![Ouvrez l’application d’exemple hello dans arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="4e4df-185">Bonjour Arduino IDE, cliquez sur **fichier** > **préférences**.</span><span class="sxs-lookup"><span data-stu-id="4e4df-185">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="4e4df-186">Bonjour **préférences** boîte de dialogue, cliquez sur toohello de hello icône suivant **URL du Gestionnaire de cartes supplémentaires** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="4e4df-186">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="4e4df-187">Dans la fenêtre contextuelle de hello, entrez hello suivant l’URL, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e4df-187">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![url du package point tooa dans arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="4e4df-189">Bonjour **préférences** boîte de dialogue, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e4df-189">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="4e4df-190">Cliquez sur **Outils** > **Type de carte** > **Gestionnaire de carte**, puis recherchez « esp8266 ».</span><span class="sxs-lookup"><span data-stu-id="4e4df-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="4e4df-191">La version 2.2.0 ou ultérieure du package ESP8266 doit être installée.</span><span class="sxs-lookup"><span data-stu-id="4e4df-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![Hello esp8266 package est installé](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="4e4df-193">Cliquez sur **Outils** > **Carte** > **Sparkfun ESP8266 Thing Dev**.</span><span class="sxs-lookup"><span data-stu-id="4e4df-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="4e4df-194">Installer les bibliothèques nécessaires</span><span class="sxs-lookup"><span data-stu-id="4e4df-194">Install necessary libraries</span></span>

1. <span data-ttu-id="4e4df-195">Bonjour Arduino IDE, cliquez sur **multiensembles** > **inclure une bibliothèque** > **gérer les bibliothèques**.</span><span class="sxs-lookup"><span data-stu-id="4e4df-195">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="4e4df-196">Rechercher le nom de bibliothèque un par un.</span><span class="sxs-lookup"><span data-stu-id="4e4df-196">Search for hello following library names one by one.</span></span> <span data-ttu-id="4e4df-197">Pour chaque bibliothèque hello vous trouvez, cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="4e4df-197">For each of hello library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="4e4df-198">Vous n’avez pas de capteur DHT22 ?</span><span class="sxs-lookup"><span data-stu-id="4e4df-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="4e4df-199">exemple d’application Hello permettre simuler des données de la température et humidité au cas où vous n’avez pas un capteur DHT22 réel.</span><span class="sxs-lookup"><span data-stu-id="4e4df-199">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="4e4df-200">données de toouse simulée d’application d’exemple hello tooenable, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4e4df-200">tooenable hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="4e4df-201">Ouvrez hello `config.h` fichier Bonjour `app` dossier.</span><span class="sxs-lookup"><span data-stu-id="4e4df-201">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="4e4df-202">Recherchez hello ligne de code suivante et remplacez valeur hello `false` trop`true`:</span><span class="sxs-lookup"><span data-stu-id="4e4df-202">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurer hello exemples application toouse simulée de données](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="4e4df-204">Enregistrez avec `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="4e4df-204">Save with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a><span data-ttu-id="4e4df-205">Déployer hello exemple application tooSparkfun ESP8266 chose Dev</span><span class="sxs-lookup"><span data-stu-id="4e4df-205">Deploy hello sample application tooSparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="4e4df-206">Bonjour Arduino IDE, cliquez sur **outil** > **Port**, puis cliquez sur les ports série hello pour Sparkfun ESP8266 chose réservé</span><span class="sxs-lookup"><span data-stu-id="4e4df-206">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="4e4df-207">Cliquez sur **multiensembles** > **télécharger** toobuild et déployer hello exemple application tooSparkfun ESP8266 chose réservé</span><span class="sxs-lookup"><span data-stu-id="4e4df-207">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooSparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="4e4df-208">Si vous utilisez macOS, vous obtiendrez probablement hello suivant des messages lors du téléchargement.</span><span class="sxs-lookup"><span data-stu-id="4e4df-208">If you are using macOS you could probably see hello following messages during uploading.</span></span> <span data-ttu-id="4e4df-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="4e4df-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="4e4df-210">Ouvrez la fenêtre ternimal et terminer ci-dessous actions toosolve ce problème.</span><span class="sxs-lookup"><span data-stu-id="4e4df-210">Please open your ternimal window and finish below actions toosolve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="4e4df-211">Entrer vos informations d’identification</span><span class="sxs-lookup"><span data-stu-id="4e4df-211">Enter your credentials</span></span>

<span data-ttu-id="4e4df-212">Une fois le téléchargement de hello se termine correctement, suivez hello étapes tooenter vos informations d’identification :</span><span class="sxs-lookup"><span data-stu-id="4e4df-212">After hello upload completes successfully, follow hello steps tooenter your credentials:</span></span>

1. <span data-ttu-id="4e4df-213">Bonjour Arduino IDE, cliquez sur **outils** > **moniteur série**.</span><span class="sxs-lookup"><span data-stu-id="4e4df-213">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="4e4df-214">Dans la fenêtre de l’analyseur série hello, notez hello deux listes déroulantes, sur hello coin inférieur droit.</span><span class="sxs-lookup"><span data-stu-id="4e4df-214">In hello serial monitor window, notice hello two drop-down lists on hello bottom right corner.</span></span>
1. <span data-ttu-id="4e4df-215">Sélectionnez **aucun guillemet de fin de ligne** pour la liste déroulante gauche hello.</span><span class="sxs-lookup"><span data-stu-id="4e4df-215">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="4e4df-216">Sélectionnez **115 200 bauds** pour la liste déroulante droite hello.</span><span class="sxs-lookup"><span data-stu-id="4e4df-216">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="4e4df-217">Dans la zone d’entrée de hello situé en haut de hello de fenêtre du moniteur série hello, entrez hello informations suivantes si vous êtes invité à tooprovide, puis cliquez sur **envoyer**.</span><span class="sxs-lookup"><span data-stu-id="4e4df-217">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="4e4df-218">SSID Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="4e4df-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="4e4df-219">Mot de passe Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="4e4df-219">Wi-Fi password</span></span>
   * <span data-ttu-id="4e4df-220">Chaîne de connexion de l’appareil</span><span class="sxs-lookup"><span data-stu-id="4e4df-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="4e4df-221">informations d’identification de Hello sont stockées dans hello EEPROM de Sparkfun ESP8266 chose dev.</span><span class="sxs-lookup"><span data-stu-id="4e4df-221">hello credential information is stored in hello EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="4e4df-222">Si vous cliquez sur le bouton de réinitialisation hello sur hello Sparkfun ESP8266 chose Dev tableau, exemple d’application hello vous demande si vous souhaitez que les informations de hello tooerase.</span><span class="sxs-lookup"><span data-stu-id="4e4df-222">If you click hello reset button on hello Sparkfun ESP8266 Thing Dev board, hello sample application asks you if you want tooerase hello information.</span></span> <span data-ttu-id="4e4df-223">Entrez `Y` toohave hello informations est effacée et vous êtes invité à nouveau les informations de hello tooprovide.</span><span class="sxs-lookup"><span data-stu-id="4e4df-223">Enter `Y` toohave hello information erased and you are asked tooprovide hello information again.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="4e4df-224">Vérifiez l’application d’exemple hello s’exécute correctement</span><span class="sxs-lookup"><span data-stu-id="4e4df-224">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="4e4df-225">Si vous voyez suivant de hello de sortie à partir de la fenêtre de l’analyseur série hello et hello clignote LED sur le développement de chose Sparkfun ESP8266, exemple d’application hello s’exécute correctement.</span><span class="sxs-lookup"><span data-stu-id="4e4df-225">If you see hello following output from hello serial monitor window and hello blinking LED on Sparkfun ESP8266 Thing Dev, hello sample application is running successfully.</span></span>

![Sortie finale dans l’IDE Arduino](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="4e4df-227">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e4df-227">Next steps</span></span>

<span data-ttu-id="4e4df-228">Vous avez connecté un Sparkfun ESP8266 chose Dev tooyour IoT hub et envoyé hello capturée capteur données tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4e4df-228">You have successfully connected a Sparkfun ESP8266 Thing Dev tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
