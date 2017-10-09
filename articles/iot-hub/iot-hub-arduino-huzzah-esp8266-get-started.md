---
title: aaaESP8266 toocloud - se connecter de contour HUZZAH ESP8266 tooAzure IoT Hub | Documents Microsoft
description: "Découvrez comment toosetup et connectez-vous Adafruit estompe HUZZAH ESP8266 tooAzure IoT Hub pour qu’il plateforme de cloud computing Azure toosend données toohello dans ce didacticiel."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="30f3c-103">Se connecter Adafruit estompe HUZZAH ESP8266 tooAzure IoT Hub dans le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="30f3c-103">Connect Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connexion entre un capteur DHT22, une carte Feather HUZZAH ESP8266 et IoT Hub](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="30f3c-105">Procédure</span><span class="sxs-lookup"><span data-stu-id="30f3c-105">What you do</span></span>


<span data-ttu-id="30f3c-106">Se connecter Adafruit estompe HUZZAH ESP8266 tooan IoT hub que vous créez.</span><span class="sxs-lookup"><span data-stu-id="30f3c-106">Connect Adafruit Feather HUZZAH ESP8266 tooan IoT hub that you create.</span></span> <span data-ttu-id="30f3c-107">Puis, vous exécutez un exemple d’application sur ESP8266 toocollect hello température et humidité les données à partir d’un capteur DHT22.</span><span class="sxs-lookup"><span data-stu-id="30f3c-107">Then you run a sample application on ESP8266 toocollect hello temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="30f3c-108">Enfin, vous envoyez le hub IoT tooyour hello capteur données.</span><span class="sxs-lookup"><span data-stu-id="30f3c-108">Finally, you send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="30f3c-109">Si vous utilisez des autres cartes ESP8266, vous pouvez toujours suivre ces étapes tooconnect il tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="30f3c-109">If you're using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="30f3c-110">Selon la carte hello ESP8266 vous utilisez, vous devrez peut-être tooreconfigure hello `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="30f3c-110">Depending on hello ESP8266 board you're using, you might need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="30f3c-111">Par exemple, si vous utilisez ESP8266 de AI-Thinker, vous pouvez modifier à partir `0` trop`2`.</span><span class="sxs-lookup"><span data-stu-id="30f3c-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` too`2`.</span></span> <span data-ttu-id="30f3c-112">Vous n’avez pas encore de kit ?</span><span class="sxs-lookup"><span data-stu-id="30f3c-112">Don't have a kit yet?</span></span> <span data-ttu-id="30f3c-113">Obtenir à partir de hello [site Web Azure](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="30f3c-113">Get it from hello [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="30f3c-114">Contenu</span><span class="sxs-lookup"><span data-stu-id="30f3c-114">What you learn</span></span>

* <span data-ttu-id="30f3c-115">Comment toocreate un IoT hub et inscrire un appareil pour estompe HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="30f3c-115">How toocreate an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="30f3c-116">Comment tooconnect estompe HUZZAH ESP8266 avec capteur de hello et votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="30f3c-116">How tooconnect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
* <span data-ttu-id="30f3c-117">Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur le contour HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="30f3c-117">How toocollect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="30f3c-118">Comment toosend hello tooyour IoT hub capteur données</span><span class="sxs-lookup"><span data-stu-id="30f3c-118">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="30f3c-119">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="30f3c-119">What you need</span></span>

![Parties nécessaires pour hello didacticiel.](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="30f3c-121">toocomplete cette opération, vous devez hello pièces suivantes à partir de votre contour HUZZAH ESP8266 Starter Kit :</span><span class="sxs-lookup"><span data-stu-id="30f3c-121">toocomplete this operation, you need hello following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="30f3c-122">Hello estompe HUZZAH ESP8266 carte</span><span class="sxs-lookup"><span data-stu-id="30f3c-122">hello Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="30f3c-123">Un câble USB d’un de tooType Micro USB</span><span class="sxs-lookup"><span data-stu-id="30f3c-123">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="30f3c-124">Vous devez également hello suivant choses pour votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="30f3c-124">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="30f3c-125">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="30f3c-125">An active Azure subscription.</span></span> <span data-ttu-id="30f3c-126">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="30f3c-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="30f3c-127">Un Mac ou un PC exécutant Windows ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="30f3c-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="30f3c-128">Réseau sans fil pour tooconnect estompe HUZZAH ESP8266 à.</span><span class="sxs-lookup"><span data-stu-id="30f3c-128">Wireless network for Feather HUZZAH ESP8266 tooconnect to.</span></span>
* <span data-ttu-id="30f3c-129">Outil de configuration Internet connexion toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="30f3c-129">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="30f3c-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="30f3c-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="30f3c-131">Les versions antérieures ne fonctionnent pas avec la bibliothèque de AzureIoT hello.</span><span class="sxs-lookup"><span data-stu-id="30f3c-131">Earlier versions don't work with hello AzureIoT library.</span></span>

<span data-ttu-id="30f3c-132">Hello éléments suivants sont facultatifs au cas où vous n’avez pas un capteur.</span><span class="sxs-lookup"><span data-stu-id="30f3c-132">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="30f3c-133">Vous avez également option hello d’utilisation des données de capteur simulé.</span><span class="sxs-lookup"><span data-stu-id="30f3c-133">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="30f3c-134">Un capteur de température et d’humidité Adafruit DHT22</span><span class="sxs-lookup"><span data-stu-id="30f3c-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="30f3c-135">Une platine d’expérimentation</span><span class="sxs-lookup"><span data-stu-id="30f3c-135">A breadboard</span></span>
* <span data-ttu-id="30f3c-136">Des câbles de liaison M/M</span><span class="sxs-lookup"><span data-stu-id="30f3c-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a><span data-ttu-id="30f3c-137">Se connecter estompe HUZZAH ESP8266 avec capteur de hello et votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="30f3c-137">Connect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
<span data-ttu-id="30f3c-138">Dans cette section, vous vous connectez tooyour du tableau capteurs de hello.</span><span class="sxs-lookup"><span data-stu-id="30f3c-138">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="30f3c-139">Puis vous connectez votre ordinateur tooyour de périphérique pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="30f3c-139">Then you plug in your device tooyour computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a><span data-ttu-id="30f3c-140">Se connecter à un DHT22 température et humidité capteur tooFeather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="30f3c-140">Connect a DHT22 temperature and humidity sensor tooFeather HUZZAH ESP8266</span></span>

<span data-ttu-id="30f3c-141">Utilisez hello breadboard et cavaliers fils toomake hello connexion comme suit.</span><span class="sxs-lookup"><span data-stu-id="30f3c-141">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="30f3c-142">Si vous n’avez pas de capteur, ignorez cette section. Vous pourrez utiliser des données de capteur simulées à la place.</span><span class="sxs-lookup"><span data-stu-id="30f3c-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Schéma des connexions](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="30f3c-144">Pour les codes confidentiels de capteur, utilisez hello suivant câblage :</span><span class="sxs-lookup"><span data-stu-id="30f3c-144">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="30f3c-145">Début (capteur)</span><span class="sxs-lookup"><span data-stu-id="30f3c-145">Start (Sensor)</span></span>           | <span data-ttu-id="30f3c-146">Fin (carte)</span><span class="sxs-lookup"><span data-stu-id="30f3c-146">End (Board)</span></span>           | <span data-ttu-id="30f3c-147">Couleur du câble</span><span class="sxs-lookup"><span data-stu-id="30f3c-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="30f3c-148">VDD (broche 31F)</span><span class="sxs-lookup"><span data-stu-id="30f3c-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="30f3c-149">3V (broche 58H)</span><span class="sxs-lookup"><span data-stu-id="30f3c-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="30f3c-150">Câble rouge</span><span class="sxs-lookup"><span data-stu-id="30f3c-150">Red cable</span></span>     |
| <span data-ttu-id="30f3c-151">DATA (broche 32F)</span><span class="sxs-lookup"><span data-stu-id="30f3c-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="30f3c-152">GPIO 2 (broche 46A)</span><span class="sxs-lookup"><span data-stu-id="30f3c-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="30f3c-153">Câble bleu</span><span class="sxs-lookup"><span data-stu-id="30f3c-153">Blue cable</span></span>    |
| <span data-ttu-id="30f3c-154">GND (broche 34F)</span><span class="sxs-lookup"><span data-stu-id="30f3c-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="30f3c-155">GND (broche 56I)</span><span class="sxs-lookup"><span data-stu-id="30f3c-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="30f3c-156">Câble noir</span><span class="sxs-lookup"><span data-stu-id="30f3c-156">Black cable</span></span>   |

<span data-ttu-id="30f3c-157">Pour plus d’informations, consultez [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) (Configuration du capteur Adafruit DHT22) et [Adafruit Feather HUZZAH ESP8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts) (Disposition des broches de l’Adafruit Feather HUZZAH ESP8266).</span><span class="sxs-lookup"><span data-stu-id="30f3c-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="30f3c-158">Votre carte Feather HUZZAH ESP8266 devrait à présent être connectée à un capteur opérationnel.</span><span class="sxs-lookup"><span data-stu-id="30f3c-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Connexion du capteur DHT22 à la carte Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a><span data-ttu-id="30f3c-160">Estompe HUZZAH ESP8266 tooyour ordinateur connecté</span><span class="sxs-lookup"><span data-stu-id="30f3c-160">Connect Feather HUZZAH ESP8266 tooyour computer</span></span>

<span data-ttu-id="30f3c-161">Comme le montre l’illustration suivante, utilisez l’ordinateur de tooyour estompe HUZZAH ESP8266 USB d’un câble tooconnect hello Micro USB tooType.</span><span class="sxs-lookup"><span data-stu-id="30f3c-161">As shown next, use hello Micro USB tooType A USB cable tooconnect Feather HUZZAH ESP8266 tooyour computer.</span></span>

![Estompe Huzzah tooyour ordinateur connecté](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="30f3c-163">Ajouter des autorisations de port série (Ubuntu uniquement)</span><span class="sxs-lookup"><span data-stu-id="30f3c-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="30f3c-164">Si vous utilisez Ubuntu, assurez-vous que vous avez hello autorisations toooperate sur hello USB port de contour HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="30f3c-164">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="30f3c-165">autorisations de port série tooadd, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="30f3c-165">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="30f3c-166">Exécutez hello suivant de commandes à partir d’un terminal :</span><span class="sxs-lookup"><span data-stu-id="30f3c-166">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="30f3c-167">Vous obtenez hello suivant sorties :</span><span class="sxs-lookup"><span data-stu-id="30f3c-167">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="30f3c-168">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="30f3c-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="30f3c-169">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="30f3c-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="30f3c-170">Dans la sortie de hello, notez que `uucp` ou `dialout` est le nom du propriétaire de groupe de hello port USB hello.</span><span class="sxs-lookup"><span data-stu-id="30f3c-170">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="30f3c-171">Ajouter groupe toohello hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="30f3c-171">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="30f3c-172">`<group-owner-name>`est le nom de propriétaire de groupe de hello que vous avez obtenu à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="30f3c-172">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="30f3c-173">`<username>` est le nom de votre utilisateur Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="30f3c-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="30f3c-174">Déconnectez-vous d’Ubuntu et puis reconnectez-vous pour hello modification tooappear.</span><span class="sxs-lookup"><span data-stu-id="30f3c-174">Sign out of Ubuntu, and then sign in again for hello change tooappear.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="30f3c-175">Collecter des données de capteur et les envoyer tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="30f3c-175">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="30f3c-176">Dans cette section, vous allez déployer et exécuter un exemple d’application sur la carte Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="30f3c-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="30f3c-177">exemple d’application Hello clignote hello LED sur estompe HUZZAH ESP8266 et envoie la température de hello et les données de l’humidité collectés hello DHT22 capteur tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="30f3c-177">hello sample application blinks hello LED on Feather HUZZAH ESP8266, and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="30f3c-178">Obtenir un exemple d’application hello à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="30f3c-178">Get hello sample application from GitHub</span></span>

<span data-ttu-id="30f3c-179">exemple d’application Hello est hébergé sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="30f3c-179">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="30f3c-180">Clonez le dépôt d’exemples hello qui contient l’exemple d’application hello à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="30f3c-180">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="30f3c-181">dépôt d’exemples tooclone hello, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="30f3c-181">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="30f3c-182">Ouvrez une invite de commandes ou une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="30f3c-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="30f3c-183">Accédez tooa dossier dans lequel toobe d’application exemple hello stockée.</span><span class="sxs-lookup"><span data-stu-id="30f3c-183">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="30f3c-184">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="30f3c-184">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="30f3c-185">Installer le package de hello pour estompe HUZZAH ESP8266 Bonjour Arduino IDE :</span><span class="sxs-lookup"><span data-stu-id="30f3c-185">Install hello package for Feather HUZZAH ESP8266 in hello Arduino IDE:</span></span>

1. <span data-ttu-id="30f3c-186">Ouvrez le dossier hello où l’application d’exemple hello est stockée.</span><span class="sxs-lookup"><span data-stu-id="30f3c-186">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="30f3c-187">Ouvrez le fichier de app.ino de hello dans le dossier de l’application hello Bonjour Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="30f3c-187">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Ouvrez l’application d’exemple hello dans Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="30f3c-189">Bonjour Arduino IDE, cliquez sur **fichier** > **préférences**.</span><span class="sxs-lookup"><span data-stu-id="30f3c-189">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="30f3c-190">Bonjour **préférences** boîte de dialogue, cliquez sur toohello de hello icône suivant **URL du Gestionnaire de cartes supplémentaires** boîte.</span><span class="sxs-lookup"><span data-stu-id="30f3c-190">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="30f3c-191">Dans la fenêtre contextuelle de hello, entrez hello suivant l’URL, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="30f3c-191">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Url du package point tooa dans Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="30f3c-193">Bonjour **préférences** boîte de dialogue, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="30f3c-193">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="30f3c-194">Cliquez sur **Outils** > **Type de carte** > **Gestionnaire de carte**, puis recherchez « esp8266 ».</span><span class="sxs-lookup"><span data-stu-id="30f3c-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="30f3c-195">Le gestionnaire de cartes indique que ESP8266 est installé avec une version 2.2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="30f3c-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![Hello esp8266 package est installé](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="30f3c-197">Cliquez sur **Outils** > **Type de carte** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="30f3c-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="30f3c-198">Installer les bibliothèques nécessaires</span><span class="sxs-lookup"><span data-stu-id="30f3c-198">Install necessary libraries</span></span>

1. <span data-ttu-id="30f3c-199">Bonjour Arduino IDE, cliquez sur **multiensembles** > **inclure une bibliothèque** > **gérer les bibliothèques**.</span><span class="sxs-lookup"><span data-stu-id="30f3c-199">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="30f3c-200">Rechercher le nom de bibliothèque un par un.</span><span class="sxs-lookup"><span data-stu-id="30f3c-200">Search for hello following library names one by one.</span></span> <span data-ttu-id="30f3c-201">Pour chacune des bibliothèques trouvées, cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="30f3c-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="30f3c-202">Vous n’avez pas de capteur DHT22 ?</span><span class="sxs-lookup"><span data-stu-id="30f3c-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="30f3c-203">exemple d’application Hello permettre simuler des données de la température et humidité au cas où vous n’avez pas un capteur DHT22 réel.</span><span class="sxs-lookup"><span data-stu-id="30f3c-203">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="30f3c-204">tooset des données toouse simulée l’application exemple hello, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="30f3c-204">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="30f3c-205">Ouvrez hello `config.h` fichier Bonjour `app` dossier.</span><span class="sxs-lookup"><span data-stu-id="30f3c-205">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="30f3c-206">Recherchez hello ligne de code suivante et remplacez valeur hello `false` trop`true`:</span><span class="sxs-lookup"><span data-stu-id="30f3c-206">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurer hello exemples application toouse simulée de données](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="30f3c-208">Enregistrez le fichier hello avec `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="30f3c-208">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a><span data-ttu-id="30f3c-209">Déployer hello exemple application tooFeather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="30f3c-209">Deploy hello sample application tooFeather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="30f3c-210">Bonjour Arduino IDE, cliquez sur **outil** > **Port**, puis cliquez sur les ports série hello pour estompe HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="30f3c-210">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="30f3c-211">Cliquez sur **multiensembles** > **télécharger** toobuild et déployer hello exemple application tooFeather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="30f3c-211">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="30f3c-212">Entrer vos informations d’identification</span><span class="sxs-lookup"><span data-stu-id="30f3c-212">Enter your credentials</span></span>

<span data-ttu-id="30f3c-213">Après avoir hello téléchargement se termine correctement, suivez ces étapes tooenter vos informations d’identification :</span><span class="sxs-lookup"><span data-stu-id="30f3c-213">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="30f3c-214">Bonjour Arduino IDE, cliquez sur **outils** > **moniteur série**.</span><span class="sxs-lookup"><span data-stu-id="30f3c-214">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="30f3c-215">Dans la fenêtre de l’analyseur série hello, notez hello deux listes déroulantes, dans le coin inférieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="30f3c-215">In hello serial monitor window, notice hello two drop-down lists in hello lower-right corner.</span></span>
1. <span data-ttu-id="30f3c-216">Sélectionnez **aucun guillemet de fin de ligne** pour la liste déroulante gauche hello.</span><span class="sxs-lookup"><span data-stu-id="30f3c-216">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="30f3c-217">Sélectionnez **115 200 bauds** pour la liste déroulante droite hello.</span><span class="sxs-lookup"><span data-stu-id="30f3c-217">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="30f3c-218">Dans la zone d’entrée de hello situé en haut de hello de fenêtre du moniteur série hello, entrez hello informations suivantes si vous êtes invité à tooprovide, puis cliquez sur **envoyer**.</span><span class="sxs-lookup"><span data-stu-id="30f3c-218">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="30f3c-219">SSID Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="30f3c-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="30f3c-220">Mot de passe Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="30f3c-220">Wi-Fi password</span></span>
   * <span data-ttu-id="30f3c-221">Chaîne de connexion de l’appareil</span><span class="sxs-lookup"><span data-stu-id="30f3c-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="30f3c-222">informations d’identification de Hello sont stockées dans hello EEPROM de contour HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="30f3c-222">hello credential information is stored in hello EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="30f3c-223">Si vous cliquez sur le bouton de réinitialisation hello sur hello estompe HUZZAH ESP8266 tableau, exemple d’application hello vous demande si vous souhaitez que les informations de hello tooerase.</span><span class="sxs-lookup"><span data-stu-id="30f3c-223">If you click hello reset button on hello Feather HUZZAH ESP8266 board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="30f3c-224">Entrez `Y` les informations de hello toohave effacées.</span><span class="sxs-lookup"><span data-stu-id="30f3c-224">Enter `Y` toohave hello information erased.</span></span> <span data-ttu-id="30f3c-225">Vous demande des informations de hello tooprovide une deuxième fois.</span><span class="sxs-lookup"><span data-stu-id="30f3c-225">You are asked tooprovide hello information a second time.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="30f3c-226">Vérifiez l’application d’exemple hello s’exécute correctement</span><span class="sxs-lookup"><span data-stu-id="30f3c-226">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="30f3c-227">Si vous voyez suivant de hello de sortie à partir de la fenêtre de l’analyseur série hello et hello clignote LED sur estompe HUZZAH ESP8266, exemple d’application hello s’exécute correctement.</span><span class="sxs-lookup"><span data-stu-id="30f3c-227">If you see hello following output from hello serial monitor window and hello blinking LED on Feather HUZZAH ESP8266, hello sample application is running successfully.</span></span>

![Sortie finale dans l’IDE Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="30f3c-229">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30f3c-229">Next steps</span></span>

<span data-ttu-id="30f3c-230">Vous avez connecté un contour HUZZAH ESP8266 tooyour IoT hub et envoyé hello capturée capteur données tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="30f3c-230">You have successfully connected a Feather HUZZAH ESP8266 tooyour IoT hub, and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

