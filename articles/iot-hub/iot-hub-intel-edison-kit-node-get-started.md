---
title: "Intel Edison vers le cloud (Node.js) - Connecter Intel Edison à Azure IoT Hub | Microsoft Docs"
description: "Dans ce didacticiel, découvrez comment configurer et connecter Intel Edison à Azure IoT Hub pour lui permettre d’envoyer des données à la plateforme cloud Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot intel edison, intel edison iot hub, intel edison envoyer des données vers le cloud, intel edison vers le cloud"
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5a31efba704045196b5563f7bc467c773bea7805
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-intel-edison-to-azure-iot-hub-nodejs"></a><span data-ttu-id="52813-104">Connecter Intel Edison à Azure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="52813-104">Connect Intel Edison to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="52813-105">Dans ce didacticiel, vous commencez par découvrir les principes fondamentaux de l’utilisation d’Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="52813-105">In this tutorial, you begin by learning the basics of working with Intel Edison.</span></span> <span data-ttu-id="52813-106">Vous apprenez ensuite à connecter en toute transparence vos appareils au cloud avec [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="52813-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="52813-107">Vous n’avez pas encore de kit ?</span><span class="sxs-lookup"><span data-stu-id="52813-107">Don't have a kit yet?</span></span> <span data-ttu-id="52813-108">Démarrer [ici](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="52813-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="52813-109">Procédure</span><span class="sxs-lookup"><span data-stu-id="52813-109">What you do</span></span>

* <span data-ttu-id="52813-110">Configurez Intel Edison et les modules Grove.</span><span class="sxs-lookup"><span data-stu-id="52813-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="52813-111">Créez un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="52813-111">Create an IoT hub.</span></span>
* <span data-ttu-id="52813-112">Inscrivez un appareil pour Edison dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="52813-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="52813-113">Exécutez un exemple d’application sur Edison pour envoyer des données de capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="52813-113">Run a sample application on Edison to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="52813-114">Connectez Intel Edison à un IoT Hub créé à cette fin.</span><span class="sxs-lookup"><span data-stu-id="52813-114">Connect Intel Edison to an IoT hub that you create.</span></span> <span data-ttu-id="52813-115">Exécutez ensuite un exemple d’application sur Edison pour collecter des données de température et d’humidité provenant d’un capteur de température Grove.</span><span class="sxs-lookup"><span data-stu-id="52813-115">Then you run a sample application on Edison to collect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="52813-116">Enfin, envoyez les données du capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="52813-116">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="52813-117">Contenu</span><span class="sxs-lookup"><span data-stu-id="52813-117">What you learn</span></span>

* <span data-ttu-id="52813-118">Création d’un Azure IoT Hub et obtention de la chaîne de connexion de votre nouvel appareil.</span><span class="sxs-lookup"><span data-stu-id="52813-118">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="52813-119">Connexion d’Edison à un capteur de température Grove.</span><span class="sxs-lookup"><span data-stu-id="52813-119">How to connect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="52813-120">Collecte des données du capteur en exécutant un exemple d’application sur Edison.</span><span class="sxs-lookup"><span data-stu-id="52813-120">How to collect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="52813-121">Envoi des données du capteur à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="52813-121">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="52813-122">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="52813-122">What you need</span></span>

![Ce dont vous avez besoin](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* <span data-ttu-id="52813-124">La carte Intel Edison</span><span class="sxs-lookup"><span data-stu-id="52813-124">The Intel Edison board</span></span>
* <span data-ttu-id="52813-125">Carte d’extension Arduino</span><span class="sxs-lookup"><span data-stu-id="52813-125">Arduino expansion board</span></span>
* <span data-ttu-id="52813-126">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="52813-126">An active Azure subscription.</span></span> <span data-ttu-id="52813-127">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="52813-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="52813-128">Un Mac ou un PC exécutant Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="52813-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="52813-129">Une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="52813-129">An Internet connection.</span></span>
* <span data-ttu-id="52813-130">Un câble USB Micro B vers Type A</span><span class="sxs-lookup"><span data-stu-id="52813-130">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="52813-131">Une alimentation en courant continu (CC).</span><span class="sxs-lookup"><span data-stu-id="52813-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="52813-132">La puissance nominale de l’alimentation doit être :</span><span class="sxs-lookup"><span data-stu-id="52813-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="52813-133">7-15 V CC</span><span class="sxs-lookup"><span data-stu-id="52813-133">7-15V DC</span></span>
  - <span data-ttu-id="52813-134">Au moins 1 500 mA</span><span class="sxs-lookup"><span data-stu-id="52813-134">At least 1500mA</span></span>
  - <span data-ttu-id="52813-135">La broche centrale/intérieure doit être le pôle positif de l’alimentation</span><span class="sxs-lookup"><span data-stu-id="52813-135">The center/inner pin should be the positive pole of the power supply</span></span>

<span data-ttu-id="52813-136">Les éléments suivants sont facultatifs :</span><span class="sxs-lookup"><span data-stu-id="52813-136">The following items are optional:</span></span>

* <span data-ttu-id="52813-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="52813-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="52813-138">Capteur de température Grove</span><span class="sxs-lookup"><span data-stu-id="52813-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="52813-139">Câble Grove</span><span class="sxs-lookup"><span data-stu-id="52813-139">Grove Cable</span></span>
* <span data-ttu-id="52813-140">Les barres de séparation ou vis incluses dans l’emballage, y compris deux vis permettant de fixer le module sur la carte d’extension et quatre jeux de vis et séparateurs en plastique.</span><span class="sxs-lookup"><span data-stu-id="52813-140">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="52813-141">Ces éléments sont facultatifs, car l’exemple de code prend en charge les données de capteur simulées.</span><span class="sxs-lookup"><span data-stu-id="52813-141">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="52813-142">Configuration d’Intel Edison</span><span class="sxs-lookup"><span data-stu-id="52813-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="52813-143">Assembler votre carte</span><span class="sxs-lookup"><span data-stu-id="52813-143">Assemble your board</span></span>

<span data-ttu-id="52813-144">Cette section présente les étapes permettant de connecter votre module Intel® Edison à votre carte d’extension.</span><span class="sxs-lookup"><span data-stu-id="52813-144">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="52813-145">Placez le module Intel® Edison à l’intérieur du cadre blanc sur votre carte d’extension, en alignant les trous du module avec les vis de la carte d’extension.</span><span class="sxs-lookup"><span data-stu-id="52813-145">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="52813-146">Appuyez sur le module juste en dessous de l’indication `What will you make?` jusqu'à entendre un clic.</span><span class="sxs-lookup"><span data-stu-id="52813-146">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![assemblage de carte 2](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="52813-148">Utilisez les deux écrous hexagonaux (inclus dans le package) pour fixer le module sur la carte d’extension.</span><span class="sxs-lookup"><span data-stu-id="52813-148">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![assemblage de carte 3](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="52813-150">Insérez une vis dans un des quatre trous situés dans les coins de la carte d’extension.</span><span class="sxs-lookup"><span data-stu-id="52813-150">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="52813-151">Faites tourner et fixez un des séparateurs en plastique blancs sur la vis.</span><span class="sxs-lookup"><span data-stu-id="52813-151">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![assemblage de carte 4](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="52813-153">Répétez l'opération pour les trois autres séparateurs situés dans les coins.</span><span class="sxs-lookup"><span data-stu-id="52813-153">Repeat for the other three corner spacers.</span></span>

   ![assemblage de carte 5](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

<span data-ttu-id="52813-155">Votre carte est maintenant assemblée.</span><span class="sxs-lookup"><span data-stu-id="52813-155">Now your board is assembled.</span></span>

   ![carte assemblée](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-the-grove-base-shield-and-the-temperature-sensor"></a><span data-ttu-id="52813-157">Connecter le module Grove Base Shield et le capteur de température</span><span class="sxs-lookup"><span data-stu-id="52813-157">Connect the Grove Base Shield and the temperature sensor</span></span>

1. <span data-ttu-id="52813-158">Placez le module Grove Base Shield sur votre carte.</span><span class="sxs-lookup"><span data-stu-id="52813-158">Place the Grove Base Shield on to your board.</span></span> <span data-ttu-id="52813-159">Assurez-vous que toutes les broches sont bien insérées dans votre carte.</span><span class="sxs-lookup"><span data-stu-id="52813-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="52813-161">Utilisez un câble Grove pour connecter le capteur de température Grove sur le port **A0** du module Grove Base Shield.</span><span class="sxs-lookup"><span data-stu-id="52813-161">Use Grove Cable to connect Grove temperature sensor onto the Grove Base Shield **A0** port.</span></span>

   ![Connexion au capteur de température](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Connexion d’Edison et du capteur](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

<span data-ttu-id="52813-164">Votre capteur est maintenant prêt.</span><span class="sxs-lookup"><span data-stu-id="52813-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="52813-165">Mise sous tension d’Edison</span><span class="sxs-lookup"><span data-stu-id="52813-165">Power up Edison</span></span>

1. <span data-ttu-id="52813-166">Branchez le bloc d’alimentation.</span><span class="sxs-lookup"><span data-stu-id="52813-166">Plug in the power supply.</span></span>

   ![Branchement du bloc d'alimentation](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. <span data-ttu-id="52813-168">Une LED verte (marquée DS1 sur la carte d’extension Arduino*) doit s’allumer et rester allumée.</span><span class="sxs-lookup"><span data-stu-id="52813-168">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="52813-169">Attendez une minute que la carte finisse de démarrer.</span><span class="sxs-lookup"><span data-stu-id="52813-169">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="52813-170">Si vous ne disposez pas d’un bloc d’alimentation CC, vous pouvez toujours alimenter la carte via un port USB.</span><span class="sxs-lookup"><span data-stu-id="52813-170">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="52813-171">Consultez la section `Connect Edison to your computer` pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="52813-171">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="52813-172">Cette procédure de mise sous tension de votre carte peut entraîner un comportement imprévisible de la carte, en particulier si vous utilisez un réseau Wi-Fi ou des moteurs d’entraînement.</span><span class="sxs-lookup"><span data-stu-id="52813-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-to-your-computer"></a><span data-ttu-id="52813-173">Connexion d’Edison à votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="52813-173">Connect Edison to your computer</span></span>

1. <span data-ttu-id="52813-174">Basculez le microcommutateur vers les deux ports micro-USB afin de placer Edison est en mode appareil.</span><span class="sxs-lookup"><span data-stu-id="52813-174">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="52813-175">Veuillez vous reporter [ici](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode) pour connaître les différences entre le mode appareil et le mode hôte.</span><span class="sxs-lookup"><span data-stu-id="52813-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Basculement du microcommutateur vers le bas](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="52813-177">Connectez le câble micro USB au port micro USB du haut.</span><span class="sxs-lookup"><span data-stu-id="52813-177">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Port micro USB du haut](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="52813-179">Branchez l’autre extrémité du câble USB à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="52813-179">Plug the other end of USB cable into your computer.</span></span>

   ![USB de l’ordinateur](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="52813-181">Vous saurez que votre carte est entièrement initialisée lorsque l’ordinateur monte un nouveau lecteur (comme lorsque vous insérez une carte SD dans votre ordinateur).</span><span class="sxs-lookup"><span data-stu-id="52813-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="52813-182">Téléchargement et exécution de l’outil de configuration</span><span class="sxs-lookup"><span data-stu-id="52813-182">Download and run the configuration tool</span></span>
<span data-ttu-id="52813-183">Consultez [ce lien](https://software.intel.com/en-us/iot/hardware/edison/downloads) répertorié sous le titre `Installers` pour obtenir le dernier outil de configuration.</span><span class="sxs-lookup"><span data-stu-id="52813-183">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="52813-184">Exécutez l’outil et suivez ses instructions à l'écran en cliquant sur Suivant si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="52813-184">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="52813-185">Flashage du microprogramme</span><span class="sxs-lookup"><span data-stu-id="52813-185">Flash firmware</span></span>
1. <span data-ttu-id="52813-186">Sur la page `Set up options`, cliquez sur `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="52813-186">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="52813-187">Sélectionnez l’image à flasher sur votre carte en effectuant l’une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="52813-187">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="52813-188">Pour télécharger et flasher votre carte avec la dernière image de microprogramme disponible d’Intel, sélectionnez `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="52813-188">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="52813-189">Pour flasher votre carte avec une image que vous avez déjà enregistrée sur votre ordinateur, sélectionnez `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="52813-189">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="52813-190">Recherchez et sélectionnez l’image à flasher sur votre carte.</span><span class="sxs-lookup"><span data-stu-id="52813-190">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="52813-191">L’outil d’installation tente de flasher votre carte.</span><span class="sxs-lookup"><span data-stu-id="52813-191">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="52813-192">L’ensemble du processus de flashage peut prendre jusqu’à 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="52813-192">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="52813-193">Définition du mot de passe</span><span class="sxs-lookup"><span data-stu-id="52813-193">Set password</span></span>
1. <span data-ttu-id="52813-194">Sur la page `Set up options`, cliquez sur `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="52813-194">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="52813-195">Vous pouvez attribuer un nom personnalisé à votre carte Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="52813-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="52813-196">Cette étape est facultative.</span><span class="sxs-lookup"><span data-stu-id="52813-196">This is optional.</span></span>
3. <span data-ttu-id="52813-197">Tapez un mot de passe pour votre carte, puis cliquez sur `Set password`.</span><span class="sxs-lookup"><span data-stu-id="52813-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="52813-198">Notez le mot de passe, qui sera utilisé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="52813-198">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="52813-199">Connexion Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="52813-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="52813-200">Sur la page `Set up options`, cliquez sur `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="52813-200">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="52813-201">Attendez environ une minute que votre ordinateur recherche les réseaux Wi-Fi disponibles.</span><span class="sxs-lookup"><span data-stu-id="52813-201">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="52813-202">Dans la liste déroulante `Detected Networks`, sélectionnez votre réseau.</span><span class="sxs-lookup"><span data-stu-id="52813-202">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="52813-203">Dans la liste déroulante `Security`, sélectionnez le type de sécurité du réseau.</span><span class="sxs-lookup"><span data-stu-id="52813-203">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="52813-204">Indiquez vos identifiant et mot de passe, puis cliquez sur `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="52813-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="52813-205">Notez l’adresse IP, qui sera utilisée ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="52813-205">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="52813-206">Assurez-vous qu’Edison est connecté au même réseau que votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="52813-206">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="52813-207">Votre ordinateur se connecte à votre Edison à l’aide de l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="52813-207">Your computer connects to your Edison by using the IP address.</span></span>

   ![Connexion au capteur de température](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

<span data-ttu-id="52813-209">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="52813-209">Congratulations!</span></span> <span data-ttu-id="52813-210">Vous avez réussi à configurer Edison.</span><span class="sxs-lookup"><span data-stu-id="52813-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="52813-211">Exécution d’un exemple d’application sur Intel Edison</span><span class="sxs-lookup"><span data-stu-id="52813-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-the-azure-iot-device-sdk"></a><span data-ttu-id="52813-212">Préparer le SDK Azure IoT Device</span><span class="sxs-lookup"><span data-stu-id="52813-212">Prepare the Azure IoT Device SDK</span></span>

1. <span data-ttu-id="52813-213">Utilisez l’un des clients SSH suivants à partir de votre ordinateur hôte pour vous connecter à votre Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="52813-213">Use one of the following SSH clients from your host computer to connect to your Intel Edison.</span></span> <span data-ttu-id="52813-214">L’adresse IP est obtenue à partir de l’outil de configuration et le mot de passe est celui que vous avez défini dans cet outil.</span><span class="sxs-lookup"><span data-stu-id="52813-214">The IP address is from the configuration tool and the password is the one you've set in that tool.</span></span>
    - <span data-ttu-id="52813-215">[PuTTY](http://www.putty.org/) pour Windows.</span><span class="sxs-lookup"><span data-stu-id="52813-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="52813-216">Le client SSH intégré sur Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="52813-216">The built-in SSH client on Ubuntu or macOS.</span></span>

2. <span data-ttu-id="52813-217">Clonez l’exemple d’application cliente sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="52813-217">Clone the sample client app to your device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. <span data-ttu-id="52813-218">Accédez ensuite au dossier de référentiel pour exécuter la commande suivante afin d’installer tous les packages (la procédure peut prendre quelques minutes).</span><span class="sxs-lookup"><span data-stu-id="52813-218">Then navigate to the repo folder to run the following command to install all packages, it may take serval minutes to complete.</span></span>
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-the-sample-application"></a><span data-ttu-id="52813-219">Configurer et exécuter l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="52813-219">Configure and run the sample application</span></span>

1. <span data-ttu-id="52813-220">Ouvrez le fichier de configuration en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="52813-220">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Fichier de configuration](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   <span data-ttu-id="52813-222">Deux éléments de type macros peuvent être configurés dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="52813-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="52813-223">Le premier est `INTERVAL`, qui définit le délai entre deux messages envoyés au cloud.</span><span class="sxs-lookup"><span data-stu-id="52813-223">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="52813-224">Le deuxième est `simulatedData`, qui est une valeur booléenne pour l’utilisation ou non des données de capteur simulées.</span><span class="sxs-lookup"><span data-stu-id="52813-224">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="52813-225">Si vous **ne disposez pas du capteur**, définissez la valeur `simulatedData` sur `true` pour que l’exemple d’application crée et utilise des données de capteur simulées.</span><span class="sxs-lookup"><span data-stu-id="52813-225">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="52813-226">Enregistrez et quittez en appuyant sur Ctrl-O > Entrée > Ctrl-X.</span><span class="sxs-lookup"><span data-stu-id="52813-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>


1. <span data-ttu-id="52813-227">Exécutez l’exemple d’application en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52813-227">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="52813-228">Assurez-vous de copier-coller la chaîne de connexion de l’appareil entre les guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="52813-228">Make sure you copy-paste the device connection string into the single quotes.</span></span>

<span data-ttu-id="52813-229">Vous devriez voir le résultat suivant, qui affiche les données de capteur et les messages envoyés à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="52813-229">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Sortie : données de capteur envoyées depuis Intel Edison vers votre IoT Hub](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="52813-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="52813-231">Next steps</span></span>

<span data-ttu-id="52813-232">Vous avez exécuté un exemple d’application pour collecter des données de capteur et les envoyer à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="52813-232">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
