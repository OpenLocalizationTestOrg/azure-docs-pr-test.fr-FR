---
title: aaaIntel Edison toocloud (Node.js) - se connecter le Edison Intel tooAzure IoT Hub | Documents Microsoft
description: "Découvrez comment toosetup et connectez-vous Intel Edison tooAzure IoT Hub pour la plateforme de cloud computing Azure Intel Edison toosend données toohello dans ce didacticiel."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot intel edison, intel hub iot d’edison, intel edison envoyer des données toocloud, intel edison toocloud"
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfc3387efc532b4b83f0626a9cf61d12c2952af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-nodejs"></a><span data-ttu-id="627ba-104">Se connecter Intel Edison tooAzure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="627ba-104">Connect Intel Edison tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="627ba-105">Dans ce didacticiel, commencer par découvrir hello des bases de l’utilisation de Edison d’Intel.</span><span class="sxs-lookup"><span data-stu-id="627ba-105">In this tutorial, you begin by learning hello basics of working with Intel Edison.</span></span> <span data-ttu-id="627ba-106">Vous apprendrez ensuite comment tooseamlessly connecter votre cloud toohello de périphériques à l’aide de [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="627ba-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="627ba-107">Vous n’avez pas encore de kit ?</span><span class="sxs-lookup"><span data-stu-id="627ba-107">Don't have a kit yet?</span></span> <span data-ttu-id="627ba-108">Démarrer [ici](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="627ba-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="627ba-109">Procédure</span><span class="sxs-lookup"><span data-stu-id="627ba-109">What you do</span></span>

* <span data-ttu-id="627ba-110">Configurez Intel Edison et les modules Grove.</span><span class="sxs-lookup"><span data-stu-id="627ba-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="627ba-111">Créez un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="627ba-111">Create an IoT hub.</span></span>
* <span data-ttu-id="627ba-112">Inscrivez un appareil pour Edison dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="627ba-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="627ba-113">Exécuter un exemple d’application sur le concentrateur de Edison toosend capteur données tooyour IoT.</span><span class="sxs-lookup"><span data-stu-id="627ba-113">Run a sample application on Edison toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="627ba-114">Connectez Intel Edison tooan IoT concentrateur que vous créez.</span><span class="sxs-lookup"><span data-stu-id="627ba-114">Connect Intel Edison tooan IoT hub that you create.</span></span> <span data-ttu-id="627ba-115">Puis vous exécutez un exemple d’application sur Edison toocollect température et humidité les données à partir d’un capteur de température Grove.</span><span class="sxs-lookup"><span data-stu-id="627ba-115">Then you run a sample application on Edison toocollect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="627ba-116">Enfin, vous envoyez le hub IoT tooyour hello capteur données.</span><span class="sxs-lookup"><span data-stu-id="627ba-116">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="627ba-117">Contenu</span><span class="sxs-lookup"><span data-stu-id="627ba-117">What you learn</span></span>

* <span data-ttu-id="627ba-118">Comment toocreate un Azure IoT hub et obtenir votre nouvelle chaîne de connexion de périphérique.</span><span class="sxs-lookup"><span data-stu-id="627ba-118">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="627ba-119">Comment tooconnect Edison avec un capteur de température Grove.</span><span class="sxs-lookup"><span data-stu-id="627ba-119">How tooconnect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="627ba-120">Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur Edison.</span><span class="sxs-lookup"><span data-stu-id="627ba-120">How toocollect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="627ba-121">Comment le hub IoT tooyour toosend capteur données.</span><span class="sxs-lookup"><span data-stu-id="627ba-121">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="627ba-122">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="627ba-122">What you need</span></span>

![Ce dont vous avez besoin](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* <span data-ttu-id="627ba-124">Hello Conseil d’Intel Edison</span><span class="sxs-lookup"><span data-stu-id="627ba-124">hello Intel Edison board</span></span>
* <span data-ttu-id="627ba-125">Carte d’extension Arduino</span><span class="sxs-lookup"><span data-stu-id="627ba-125">Arduino expansion board</span></span>
* <span data-ttu-id="627ba-126">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="627ba-126">An active Azure subscription.</span></span> <span data-ttu-id="627ba-127">Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="627ba-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="627ba-128">Un Mac ou un PC exécutant Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="627ba-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="627ba-129">Une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="627ba-129">An Internet connection.</span></span>
* <span data-ttu-id="627ba-130">Un câble USB d’un de tooType Micro B</span><span class="sxs-lookup"><span data-stu-id="627ba-130">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="627ba-131">Une alimentation en courant continu (CC).</span><span class="sxs-lookup"><span data-stu-id="627ba-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="627ba-132">La puissance nominale de l’alimentation doit être :</span><span class="sxs-lookup"><span data-stu-id="627ba-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="627ba-133">7-15 V CC</span><span class="sxs-lookup"><span data-stu-id="627ba-133">7-15V DC</span></span>
  - <span data-ttu-id="627ba-134">Au moins 1 500 mA</span><span class="sxs-lookup"><span data-stu-id="627ba-134">At least 1500mA</span></span>
  - <span data-ttu-id="627ba-135">code confidentiel de Hello center/interne doit être pôle positif de hello d’alimentation hello</span><span class="sxs-lookup"><span data-stu-id="627ba-135">hello center/inner pin should be hello positive pole of hello power supply</span></span>

<span data-ttu-id="627ba-136">Hello éléments suivants est facultatif :</span><span class="sxs-lookup"><span data-stu-id="627ba-136">hello following items are optional:</span></span>

* <span data-ttu-id="627ba-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="627ba-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="627ba-138">Capteur de température Grove</span><span class="sxs-lookup"><span data-stu-id="627ba-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="627ba-139">Câble Grove</span><span class="sxs-lookup"><span data-stu-id="627ba-139">Grove Cable</span></span>
* <span data-ttu-id="627ba-140">Les barres d’espacement ni vis inclus dans le package hello, y compris des deux vis toofasten hello toohello expansion carte et quatre ensembles de vis et des séparateurs en plastique.</span><span class="sxs-lookup"><span data-stu-id="627ba-140">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="627ba-141">Ces éléments sont facultatifs, car la prise en charge des exemples de code hello simulée des données de capteur.</span><span class="sxs-lookup"><span data-stu-id="627ba-141">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="627ba-142">Configuration d’Intel Edison</span><span class="sxs-lookup"><span data-stu-id="627ba-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="627ba-143">Assembler votre carte</span><span class="sxs-lookup"><span data-stu-id="627ba-143">Assemble your board</span></span>

<span data-ttu-id="627ba-144">Cette section contient les étapes tooattach votre carte Intel® Edison tooyour d’extension.</span><span class="sxs-lookup"><span data-stu-id="627ba-144">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="627ba-145">Placez le module Intel® Edison hello hiérarchique de hello blanc dans votre tableau d’extension, de trous hello sur le module de hello avec vis hello sur la carte d’extension de hello s’aligne.</span><span class="sxs-lookup"><span data-stu-id="627ba-145">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="627ba-146">Appuyez sur le module hello juste en dessous des mots hello `What will you make?` jusqu'à ce que vous pensez qu’un composant logiciel enfichable.</span><span class="sxs-lookup"><span data-stu-id="627ba-146">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![assemblage de carte 2](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="627ba-148">Utilisez hello deux fruits hex (inclus dans le package de hello) toosecure hello toohello expansion carte.</span><span class="sxs-lookup"><span data-stu-id="627ba-148">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![assemblage de carte 3](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="627ba-150">Insérer une vis de l’une des quatre trous de coin hello sur la carte d’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="627ba-150">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="627ba-151">Torsion et renforcer un des séparateurs de plastique hello blanc sur vis de hello.</span><span class="sxs-lookup"><span data-stu-id="627ba-151">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![assemblage de carte 4](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="627ba-153">Répétez cette opération pour hello autres séparateurs trois angle.</span><span class="sxs-lookup"><span data-stu-id="627ba-153">Repeat for hello other three corner spacers.</span></span>

   ![assemblage de carte 5](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

<span data-ttu-id="627ba-155">Votre carte est maintenant assemblée.</span><span class="sxs-lookup"><span data-stu-id="627ba-155">Now your board is assembled.</span></span>

   ![carte assemblée](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a><span data-ttu-id="627ba-157">Se connecter hello Grove Base bouclier et capteur de température hello</span><span class="sxs-lookup"><span data-stu-id="627ba-157">Connect hello Grove Base Shield and hello temperature sensor</span></span>

1. <span data-ttu-id="627ba-158">Placez hello Grove Base bouclier sur tooyour carte.</span><span class="sxs-lookup"><span data-stu-id="627ba-158">Place hello Grove Base Shield on tooyour board.</span></span> <span data-ttu-id="627ba-159">Assurez-vous que toutes les broches sont bien insérées dans votre carte.</span><span class="sxs-lookup"><span data-stu-id="627ba-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="627ba-161">Capteur de température utilisez Grove câble tooconnect Grove sur hello Grove Base bouclier **A0** port.</span><span class="sxs-lookup"><span data-stu-id="627ba-161">Use Grove Cable tooconnect Grove temperature sensor onto hello Grove Base Shield **A0** port.</span></span>

   ![Se connecter tootemperature capteur](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Connexion d’Edison et du capteur](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

<span data-ttu-id="627ba-164">Votre capteur est maintenant prêt.</span><span class="sxs-lookup"><span data-stu-id="627ba-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="627ba-165">Mise sous tension d’Edison</span><span class="sxs-lookup"><span data-stu-id="627ba-165">Power up Edison</span></span>

1. <span data-ttu-id="627ba-166">Branchez alimentation hello.</span><span class="sxs-lookup"><span data-stu-id="627ba-166">Plug in hello power supply.</span></span>

   ![Branchement du bloc d'alimentation](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. <span data-ttu-id="627ba-168">Une DEL verte (étiquetée DS1 sur hello Arduino * de carte d’extension) doit s’allumer et restent allumée.</span><span class="sxs-lookup"><span data-stu-id="627ba-168">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="627ba-169">Patientez une minute pour toofinish de tableau hello le démarrage.</span><span class="sxs-lookup"><span data-stu-id="627ba-169">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="627ba-170">Si vous ne disposez pas d’une alimentation de contrôleur de domaine, vous pouvez toujours de carte hello l’alimentation via un port USB.</span><span class="sxs-lookup"><span data-stu-id="627ba-170">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="627ba-171">Consultez la section `Connect Edison tooyour computer` pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="627ba-171">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="627ba-172">Cette procédure de mise sous tension de votre carte peut entraîner un comportement imprévisible de la carte, en particulier si vous utilisez un réseau Wi-Fi ou des moteurs d’entraînement.</span><span class="sxs-lookup"><span data-stu-id="627ba-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="627ba-173">Connectez Edison tooyour ordinateur</span><span class="sxs-lookup"><span data-stu-id="627ba-173">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="627ba-174">Basculer vers le bas microrupteur hello vers hello deux micro ports USB, afin que Edison est en mode de périphérique.</span><span class="sxs-lookup"><span data-stu-id="627ba-174">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="627ba-175">Veuillez vous reporter [ici](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode) pour connaître les différences entre le mode appareil et le mode hôte.</span><span class="sxs-lookup"><span data-stu-id="627ba-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Basculer vers le bas microrupteur de hello](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="627ba-177">Branchez les câbles USB micro hello le port USB supérieur micro hello.</span><span class="sxs-lookup"><span data-stu-id="627ba-177">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Port micro USB du haut](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="627ba-179">Plug hello l’autre extrémité du câble USB à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="627ba-179">Plug hello other end of USB cable into your computer.</span></span>

   ![USB de l’ordinateur](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="627ba-181">Vous saurez que votre carte est entièrement initialisée lorsque l’ordinateur monte un nouveau lecteur (comme lorsque vous insérez une carte SD dans votre ordinateur).</span><span class="sxs-lookup"><span data-stu-id="627ba-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="627ba-182">Téléchargez et exécutez l’outil de configuration hello</span><span class="sxs-lookup"><span data-stu-id="627ba-182">Download and run hello configuration tool</span></span>
<span data-ttu-id="627ba-183">Obtenir hello dernier outil de configuration à partir de [ce lien](https://software.intel.com/en-us/iot/hardware/edison/downloads) répertoriés sous hello `Installers` titre.</span><span class="sxs-lookup"><span data-stu-id="627ba-183">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="627ba-184">Exécutez l’outil de hello et suivez sa à l’écran des instructions, en cliquant sur Suivant si nécessaire</span><span class="sxs-lookup"><span data-stu-id="627ba-184">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="627ba-185">Flashage du microprogramme</span><span class="sxs-lookup"><span data-stu-id="627ba-185">Flash firmware</span></span>
1. <span data-ttu-id="627ba-186">Sur hello `Set up options` , cliquez sur `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="627ba-186">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="627ba-187">Sélectionnez tooflash d’image hello sur votre carte mère en effectuant l’une des manières suivantes les hello :</span><span class="sxs-lookup"><span data-stu-id="627ba-187">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="627ba-188">toodownload et flash votre carte mère avec hello dernière image de microprogramme auprès d’Intel, sélectionnez `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="627ba-188">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="627ba-189">sélectionner de votre tableau avec une image que vous avez déjà enregistré sur votre ordinateur, tooflash `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="627ba-189">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="627ba-190">Parcourir tooand hello sélectionnez image de carte de tooyour tooflash.</span><span class="sxs-lookup"><span data-stu-id="627ba-190">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="627ba-191">outil de configuration Hello va tenter de tooflash votre carte mère.</span><span class="sxs-lookup"><span data-stu-id="627ba-191">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="627ba-192">processus clignotant Hello peut prendre jusqu'à too10 minutes.</span><span class="sxs-lookup"><span data-stu-id="627ba-192">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="627ba-193">Définition du mot de passe</span><span class="sxs-lookup"><span data-stu-id="627ba-193">Set password</span></span>
1. <span data-ttu-id="627ba-194">Sur hello `Set up options` , cliquez sur `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="627ba-194">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="627ba-195">Vous pouvez attribuer un nom personnalisé à votre carte Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="627ba-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="627ba-196">Cette étape est facultative.</span><span class="sxs-lookup"><span data-stu-id="627ba-196">This is optional.</span></span>
3. <span data-ttu-id="627ba-197">Tapez un mot de passe pour votre carte, puis cliquez sur `Set password`.</span><span class="sxs-lookup"><span data-stu-id="627ba-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="627ba-198">Démarquer hello un mot de passe qui sera utilisé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="627ba-198">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="627ba-199">Connexion Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="627ba-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="627ba-200">Sur hello `Set up options` , cliquez sur `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="627ba-200">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="627ba-201">Attente d’une minute tooone sous la forme d’analyses de votre ordinateur pour les réseaux Wi-Fi disponibles.</span><span class="sxs-lookup"><span data-stu-id="627ba-201">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="627ba-202">À partir de hello `Detected Networks` liste déroulante, sélectionnez votre réseau.</span><span class="sxs-lookup"><span data-stu-id="627ba-202">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="627ba-203">À partir de hello `Security` liste déroulante, le type de sécurité du réseau : sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="627ba-203">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="627ba-204">Indiquez vos identifiant et mot de passe, puis cliquez sur `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="627ba-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="627ba-205">Démarquer hello adresse IP, qui est utilisée ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="627ba-205">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="627ba-206">Assurez-vous que Edison est connecté toohello même réseau que votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="627ba-206">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="627ba-207">Votre ordinateur connecte tooyour Edison en utilisant l’adresse IP de hello.</span><span class="sxs-lookup"><span data-stu-id="627ba-207">Your computer connects tooyour Edison by using hello IP address.</span></span>

   ![Se connecter tootemperature capteur](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

<span data-ttu-id="627ba-209">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="627ba-209">Congratulations!</span></span> <span data-ttu-id="627ba-210">Vous avez réussi à configurer Edison.</span><span class="sxs-lookup"><span data-stu-id="627ba-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="627ba-211">Exécution d’un exemple d’application sur Intel Edison</span><span class="sxs-lookup"><span data-stu-id="627ba-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-hello-azure-iot-device-sdk"></a><span data-ttu-id="627ba-212">Préparer hello SDK de périphérique Azure IoT</span><span class="sxs-lookup"><span data-stu-id="627ba-212">Prepare hello Azure IoT Device SDK</span></span>

1. <span data-ttu-id="627ba-213">Utilisez une des hello suivant clients SSH à partir de votre ordinateur hôte ordinateur tooconnect tooyour Edison d’Intel.</span><span class="sxs-lookup"><span data-stu-id="627ba-213">Use one of hello following SSH clients from your host computer tooconnect tooyour Intel Edison.</span></span> <span data-ttu-id="627ba-214">adresse IP de Hello est à partir de l’outil de configuration hello et mot de passe hello hello que vous avez définie dans cet outil.</span><span class="sxs-lookup"><span data-stu-id="627ba-214">hello IP address is from hello configuration tool and hello password is hello one you've set in that tool.</span></span>
    - <span data-ttu-id="627ba-215">[PuTTY](http://www.putty.org/) pour Windows.</span><span class="sxs-lookup"><span data-stu-id="627ba-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="627ba-216">client Hello intégré SSH sur Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="627ba-216">hello built-in SSH client on Ubuntu or macOS.</span></span>

2. <span data-ttu-id="627ba-217">Clone hello exemple client tooyour périphérique d’application.</span><span class="sxs-lookup"><span data-stu-id="627ba-217">Clone hello sample client app tooyour device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. <span data-ttu-id="627ba-218">Il peut prendre un substance présentant minutes toocomplete, puis accédez toohello hello du toorun dossier de dépôt suivant commande tooinstall tous les packages.</span><span class="sxs-lookup"><span data-stu-id="627ba-218">Then navigate toohello repo folder toorun hello following command tooinstall all packages, it may take serval minutes toocomplete.</span></span>
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-hello-sample-application"></a><span data-ttu-id="627ba-219">Configurer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="627ba-219">Configure and run hello sample application</span></span>

1. <span data-ttu-id="627ba-220">Ouvrez le fichier de configuration de hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="627ba-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Fichier de configuration](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   <span data-ttu-id="627ba-222">Deux éléments de type macros peuvent être configurés dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="627ba-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="627ba-223">Bonjour tout d’abord un est `INTERVAL`, qui définit l’intervalle de temps hello entre les deux messages toocloud d’envoi.</span><span class="sxs-lookup"><span data-stu-id="627ba-223">hello first one is `INTERVAL`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="627ba-224">Hello deuxième `simulatedData`, qui est une valeur booléenne pour toouse indique si les données de capteur simulé ou non.</span><span class="sxs-lookup"><span data-stu-id="627ba-224">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="627ba-225">Si vous **n’avez pas capteur de hello**, affectez la valeur hello `simulatedData` valeur trop`true` toomake hello exemple d’application, créer et utiliser des données de capteur simulé.</span><span class="sxs-lookup"><span data-stu-id="627ba-225">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="627ba-226">Enregistrez et quittez en appuyant sur Ctrl-O > Entrée > Ctrl-X.</span><span class="sxs-lookup"><span data-stu-id="627ba-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>


1. <span data-ttu-id="627ba-227">Exécuter l’exemple d’application hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="627ba-227">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="627ba-228">Assurez-vous que vous copier-coller chaîne de connexion de périphérique hello dans des guillemets simples de hello.</span><span class="sxs-lookup"><span data-stu-id="627ba-228">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>

<span data-ttu-id="627ba-229">Vous devez voir qu’affiche hello messages hello et les données de capteur envoyés tooyour IoT hub de sortie suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="627ba-229">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Sortie - données de capteur envoyés à partir d’Intel Edison tooyour IoT hub](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="627ba-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="627ba-231">Next steps</span></span>

<span data-ttu-id="627ba-232">Vous avez exécuté un exemple de données de capteur application toocollect et envoyez tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="627ba-232">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
