---
title: "ESP8266 vers cloud - Connecter la carte Feather HUZZAH ESP8266 à Azure IoT Hub | Microsoft Docs"
description: "Ce didacticiel explique comment configurer la carte Adafruit Feather HUZZAH ESP8266 et la connecter à Azure IoT Hub pour envoyer des données à la plateforme cloud Azure."
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
ms.openlocfilehash: 6a450579c848fe6030a328ddf410f139baae2324
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="3a0fe-103">Connecter l’Adafruit Feather HUZZAH ESP8266 à Azure IoT Hub dans le cloud</span><span class="sxs-lookup"><span data-stu-id="3a0fe-103">Connect Adafruit Feather HUZZAH ESP8266 to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connexion entre un capteur DHT22, une carte Feather HUZZAH ESP8266 et IoT Hub](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="3a0fe-105">Procédure</span><span class="sxs-lookup"><span data-stu-id="3a0fe-105">What you do</span></span>


<span data-ttu-id="3a0fe-106">En premier lieu, vous connecterez l’Adafruit Feather HUZZAH ESP8266 à un IoT Hub créé à cette fin.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-106">Connect Adafruit Feather HUZZAH ESP8266 to an IoT hub that you create.</span></span> <span data-ttu-id="3a0fe-107">Ensuite, vous exécutez un exemple d’application sur l’ESP8266 pour collecter des données de température et d’humidité provenant d’un capteur DHT22.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-107">Then you run a sample application on ESP8266 to collect the temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="3a0fe-108">Enfin, vous enverrez les données du capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-108">Finally, you send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="3a0fe-109">Si vous utilisez une autre carte ESP8266, vous pouvez également suivre ces étapes pour la connecter à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-109">If you're using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="3a0fe-110">Selon la carte ESP8266 que vous utilisez, il se peut que vous deviez reconfigurer le paramètre `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-110">Depending on the ESP8266 board you're using, you might need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="3a0fe-111">Par exemple, si vous utilisez l’ESP8266 d’AI-Thinker, vous devrez peut-être remplacer la valeur `0` de ce paramètre par `2`.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` to `2`.</span></span> <span data-ttu-id="3a0fe-112">Vous n’avez pas encore de kit ?</span><span class="sxs-lookup"><span data-stu-id="3a0fe-112">Don't have a kit yet?</span></span> <span data-ttu-id="3a0fe-113">Obtenez-le depuis le [site web Azure](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="3a0fe-113">Get it from the [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="3a0fe-114">Contenu</span><span class="sxs-lookup"><span data-stu-id="3a0fe-114">What you learn</span></span>

* <span data-ttu-id="3a0fe-115">Création d’un IoT Hub et enregistrement d’un appareil pour la carte Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="3a0fe-115">How to create an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="3a0fe-116">Connexion du Feather HUZZAH ESP8266 au capteur et à votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="3a0fe-116">How to connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
* <span data-ttu-id="3a0fe-117">Collecte des données du capteur en exécutant un exemple d’application sur la carte Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="3a0fe-117">How to collect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="3a0fe-118">Envoi des données du capteur à votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3a0fe-118">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3a0fe-119">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="3a0fe-119">What you need</span></span>

![Composants requis pour le didacticiel](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="3a0fe-121">Pour cette opération, vous aurez besoin des composants suivants de votre Kit de démarrage Feather HUZZAH ESP8266 :</span><span class="sxs-lookup"><span data-stu-id="3a0fe-121">To complete this operation, you need the following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="3a0fe-122">La carte Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="3a0fe-122">The Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="3a0fe-123">Un câble Micro USB Micro B vers USB Type A</span><span class="sxs-lookup"><span data-stu-id="3a0fe-123">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="3a0fe-124">Vous aurez également besoin des éléments suivants pour votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="3a0fe-124">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="3a0fe-125">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-125">An active Azure subscription.</span></span> <span data-ttu-id="3a0fe-126">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="3a0fe-127">Un Mac ou un PC exécutant Windows ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="3a0fe-128">Un réseau sans fil auquel connecter la carte Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-128">Wireless network for Feather HUZZAH ESP8266 to connect to.</span></span>
* <span data-ttu-id="3a0fe-129">Une connexion Internet pour télécharger l’outil de configuration.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-129">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="3a0fe-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="3a0fe-131">Les versions antérieures ne fonctionneront pas avec la bibliothèque AzureIoT.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-131">Earlier versions don't work with the AzureIoT library.</span></span>

<span data-ttu-id="3a0fe-132">Les éléments suivants sont facultatifs si vous n’avez pas de capteur.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-132">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="3a0fe-133">Vous avez également la possibilité d’utiliser des données de capteur simulées.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-133">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="3a0fe-134">Un capteur de température et d’humidité Adafruit DHT22</span><span class="sxs-lookup"><span data-stu-id="3a0fe-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="3a0fe-135">Une platine d’expérimentation</span><span class="sxs-lookup"><span data-stu-id="3a0fe-135">A breadboard</span></span>
* <span data-ttu-id="3a0fe-136">Des câbles de liaison M/M</span><span class="sxs-lookup"><span data-stu-id="3a0fe-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-the-sensor-and-your-computer"></a><span data-ttu-id="3a0fe-137">Connecter la carte Feather HUZZAH ESP8266 au capteur et à votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="3a0fe-137">Connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
<span data-ttu-id="3a0fe-138">Dans cette section, vous connectez les capteurs à votre tableau.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-138">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="3a0fe-139">Puis vous connectez votre appareil à votre ordinateur pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-139">Then you plug in your device to your computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-huzzah-esp8266"></a><span data-ttu-id="3a0fe-140">Connecter un capteur de température et d’humidité DHT22 à la carte Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="3a0fe-140">Connect a DHT22 temperature and humidity sensor to Feather HUZZAH ESP8266</span></span>

<span data-ttu-id="3a0fe-141">Utilisez la platine d’expérimentation et les câbles de liaison pour effectuer la connexion comme suit.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-141">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="3a0fe-142">Si vous n’avez pas de capteur, ignorez cette section. Vous pourrez utiliser des données de capteur simulées à la place.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Schéma des connexions](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="3a0fe-144">Pour les broches du capteur, utilisez le câblage suivant :</span><span class="sxs-lookup"><span data-stu-id="3a0fe-144">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="3a0fe-145">Début (capteur)</span><span class="sxs-lookup"><span data-stu-id="3a0fe-145">Start (Sensor)</span></span>           | <span data-ttu-id="3a0fe-146">Fin (carte)</span><span class="sxs-lookup"><span data-stu-id="3a0fe-146">End (Board)</span></span>           | <span data-ttu-id="3a0fe-147">Couleur du câble</span><span class="sxs-lookup"><span data-stu-id="3a0fe-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="3a0fe-148">VDD (broche 31F)</span><span class="sxs-lookup"><span data-stu-id="3a0fe-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="3a0fe-149">3V (broche 58H)</span><span class="sxs-lookup"><span data-stu-id="3a0fe-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="3a0fe-150">Câble rouge</span><span class="sxs-lookup"><span data-stu-id="3a0fe-150">Red cable</span></span>     |
| <span data-ttu-id="3a0fe-151">DATA (broche 32F)</span><span class="sxs-lookup"><span data-stu-id="3a0fe-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="3a0fe-152">GPIO 2 (broche 46A)</span><span class="sxs-lookup"><span data-stu-id="3a0fe-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="3a0fe-153">Câble bleu</span><span class="sxs-lookup"><span data-stu-id="3a0fe-153">Blue cable</span></span>    |
| <span data-ttu-id="3a0fe-154">GND (broche 34F)</span><span class="sxs-lookup"><span data-stu-id="3a0fe-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="3a0fe-155">GND (broche 56I)</span><span class="sxs-lookup"><span data-stu-id="3a0fe-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="3a0fe-156">Câble noir</span><span class="sxs-lookup"><span data-stu-id="3a0fe-156">Black cable</span></span>   |

<span data-ttu-id="3a0fe-157">Pour plus d’informations, consultez [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) (Configuration du capteur Adafruit DHT22) et [Adafruit Feather HUZZAH ESP8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts) (Disposition des broches de l’Adafruit Feather HUZZAH ESP8266).</span><span class="sxs-lookup"><span data-stu-id="3a0fe-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="3a0fe-158">Votre carte Feather HUZZAH ESP8266 devrait à présent être connectée à un capteur opérationnel.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Connexion du capteur DHT22 à la carte Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-to-your-computer"></a><span data-ttu-id="3a0fe-160">Connexion de la carte Feather HUZZAH ESP8266 à votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="3a0fe-160">Connect Feather HUZZAH ESP8266 to your computer</span></span>

<span data-ttu-id="3a0fe-161">Comme présenté ensuite, à l’aide du câble Micro USB vers USB Type A, connectez la carte Feather HUZZAH ESP8266 à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-161">As shown next, use the Micro USB to Type A USB cable to connect Feather HUZZAH ESP8266 to your computer.</span></span>

![Connexion de la carte Feather Huzzah à votre ordinateur](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="3a0fe-163">Ajouter des autorisations de port série (Ubuntu uniquement)</span><span class="sxs-lookup"><span data-stu-id="3a0fe-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="3a0fe-164">Si vous utilisez Ubuntu, assurez-vous que vous disposez des autorisations nécessaires pour utiliser le port USB de la carte Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-164">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="3a0fe-165">Pour ajouter des autorisations de port série, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3a0fe-165">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="3a0fe-166">Dans un terminal, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a0fe-166">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="3a0fe-167">Vous obtenez l’une des sorties suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a0fe-167">You get one of the following outputs:</span></span>

   * <span data-ttu-id="3a0fe-168">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="3a0fe-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="3a0fe-169">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="3a0fe-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="3a0fe-170">Dans la sortie, `uucp` ou `dialout` correspond au nom du propriétaire du groupe du port USB.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-170">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="3a0fe-171">Ajoutez l’utilisateur au groupe en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3a0fe-171">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="3a0fe-172">`<group-owner-name>` est le nom du propriétaire du groupe que vous avez obtenu à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-172">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="3a0fe-173">`<username>` est le nom de votre utilisateur Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="3a0fe-174">Déconnectez-vous d’Ubuntu, puis reconnectez-vous pour que la modification prenne effet.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-174">Sign out of Ubuntu, and then sign in again for the change to appear.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="3a0fe-175">Collecter les données du capteur et les envoyer à votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3a0fe-175">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="3a0fe-176">Dans cette section, vous allez déployer et exécuter un exemple d’application sur la carte Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="3a0fe-177">L’exemple d’application fait clignoter la LED de la carte Feather HUZZAH ESP8266 et envoie les données de température et d’humidité collectées à partir du capteur DHT22 à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-177">The sample application blinks the LED on Feather HUZZAH ESP8266, and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="3a0fe-178">Obtenir l’exemple d’application à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="3a0fe-178">Get the sample application from GitHub</span></span>

<span data-ttu-id="3a0fe-179">L’exemple d’application est hébergé sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-179">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="3a0fe-180">Clonez l’exemple de référentiel contenant l’exemple d’application à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-180">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="3a0fe-181">Pour cloner l’exemple de référentiel, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3a0fe-181">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="3a0fe-182">Ouvrez une invite de commandes ou une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="3a0fe-183">Accédez au dossier à utiliser pour le stockage de l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-183">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="3a0fe-184">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3a0fe-184">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="3a0fe-185">Installez le package pour la carte Feather HUZZAH ESP8266 dans l’IDE Arduino :</span><span class="sxs-lookup"><span data-stu-id="3a0fe-185">Install the package for Feather HUZZAH ESP8266 in the Arduino IDE:</span></span>

1. <span data-ttu-id="3a0fe-186">Ouvrez le dossier où l’exemple d’application est stocké.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-186">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="3a0fe-187">Ouvrez le fichier app.ino dans le dossier app de l’IDE Arduino.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-187">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![Ouverture de l’exemple d’application dans l’IDE Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="3a0fe-189">Dans l’IDE Arduino, cliquez sur **Fichier** > **Préférences**.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-189">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="3a0fe-190">Dans la boîte de dialogue **Préférences**, cliquez sur l’icône en regard de la zone **URL de gestionnaire de cartes supplémentaires**.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-190">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="3a0fe-191">Dans la fenêtre contextuelle, entrez l’URL suivante, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-191">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Pointage vers l’URL d’un package dans l’IDE Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="3a0fe-193">Dans la boîte de dialogue **Préférences**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-193">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="3a0fe-194">Cliquez sur **Outils** > **Type de carte** > **Gestionnaire de carte**, puis recherchez « esp8266 ».</span><span class="sxs-lookup"><span data-stu-id="3a0fe-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="3a0fe-195">Le gestionnaire de cartes indique que ESP8266 est installé avec une version 2.2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![Le package ESP8266 est installé](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="3a0fe-197">Cliquez sur **Outils** > **Type de carte** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="3a0fe-198">Installer les bibliothèques nécessaires</span><span class="sxs-lookup"><span data-stu-id="3a0fe-198">Install necessary libraries</span></span>

1. <span data-ttu-id="3a0fe-199">Dans l’IDE Arduino, cliquez sur **Croquis** > **Inclure une bibliothèque** > **Gérer les bibliothèques**.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-199">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="3a0fe-200">Recherchez les noms de bibliothèque suivants un par un.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-200">Search for the following library names one by one.</span></span> <span data-ttu-id="3a0fe-201">Pour chacune des bibliothèques trouvées, cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="3a0fe-202">Vous n’avez pas de capteur DHT22 ?</span><span class="sxs-lookup"><span data-stu-id="3a0fe-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="3a0fe-203">L’exemple d’application permet de simuler des données de température et d’humidité si vous n’avez pas de capteur DHT22.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-203">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="3a0fe-204">Pour configurer l’utilisation de données simulées par l’exemple d’application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3a0fe-204">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="3a0fe-205">Ouvrez le fichier `config.h` dans le dossier `app`.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-205">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="3a0fe-206">Recherchez la ligne de code suivante et remplacez la valeur `false` par `true` :</span><span class="sxs-lookup"><span data-stu-id="3a0fe-206">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configuration de l’exemple d’application pour utiliser des données simulées](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="3a0fe-208">Enregistrez le fichier avec `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-208">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-huzzah-esp8266"></a><span data-ttu-id="3a0fe-209">Déployer l’exemple d’application sur la carte Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="3a0fe-209">Deploy the sample application to Feather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="3a0fe-210">Dans l’IDE Arduino, cliquez sur **outil** > **Port**, puis cliquez sur le port série pour la carte Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-210">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="3a0fe-211">Cliquez sur **Croquis** > **Téléverser** pour générer et déployer l’exemple d’application sur la carte Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-211">Click **Sketch** > **Upload** to build and deploy the sample application to Feather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="3a0fe-212">Entrer vos informations d’identification</span><span class="sxs-lookup"><span data-stu-id="3a0fe-212">Enter your credentials</span></span>

<span data-ttu-id="3a0fe-213">Une fois le chargement terminé, suivez cette procédure pour entrer vos informations d’identification :</span><span class="sxs-lookup"><span data-stu-id="3a0fe-213">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="3a0fe-214">Dans l’IDE Arduino, cliquez sur **Outils** > **Moniteur série**.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-214">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="3a0fe-215">Dans la fenêtre Moniteur série, vous pouvez remarquer la présence de deux listes déroulantes dans le coin inférieur droit.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-215">In the serial monitor window, notice the two drop-down lists in the lower-right corner.</span></span>
1. <span data-ttu-id="3a0fe-216">Pour la liste déroulante de gauche, sélectionnez **Pas de fin de ligne**.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-216">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="3a0fe-217">Pour la liste déroulante de droite, sélectionnez **115200 baud**.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-217">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="3a0fe-218">Dans la zone de saisie située en haut de la fenêtre Moniteur série, entrez les informations suivantes si elles vous sont demandées, puis cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-218">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="3a0fe-219">SSID Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="3a0fe-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="3a0fe-220">Mot de passe Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="3a0fe-220">Wi-Fi password</span></span>
   * <span data-ttu-id="3a0fe-221">Chaîne de connexion de l’appareil</span><span class="sxs-lookup"><span data-stu-id="3a0fe-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="3a0fe-222">Les informations d’identification sont stockées dans la mémoire EEPROM de la carte Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-222">The credential information is stored in the EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="3a0fe-223">Si vous cliquez sur le bouton de réinitialisation de la carte Feather HUZZAH ESP8266, l’exemple d’application vous demande si vous souhaitez effacer ces informations.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-223">If you click the reset button on the Feather HUZZAH ESP8266 board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="3a0fe-224">Entrez `Y` pour effacer les informations.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-224">Enter `Y` to have the information erased.</span></span> <span data-ttu-id="3a0fe-225">Vous êtes invité à fournir les informations une deuxième fois.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-225">You are asked to provide the information a second time.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="3a0fe-226">Vérifier que l’exemple d’application s’exécute correctement</span><span class="sxs-lookup"><span data-stu-id="3a0fe-226">Verify the sample application is running successfully</span></span>

<span data-ttu-id="3a0fe-227">Si vous voyez la sortie suivante dans la fenêtre Moniteur série et la LED clignoter sur la carte Feather HUZZAH ESP8266, l’exemple d’application s’exécute correctement.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-227">If you see the following output from the serial monitor window and the blinking LED on Feather HUZZAH ESP8266, the sample application is running successfully.</span></span>

![Sortie finale dans Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="3a0fe-229">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3a0fe-229">Next steps</span></span>

<span data-ttu-id="3a0fe-230">Vous avez correctement connecté une carte Feather HUZZAH ESP8266 à votre IoT Hub et envoyé les données de capteur collectées à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3a0fe-230">You have successfully connected a Feather HUZZAH ESP8266 to your IoT hub, and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

