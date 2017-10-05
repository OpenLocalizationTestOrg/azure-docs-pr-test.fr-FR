---
title: "Connecter Intel Edison (Node) à Azure IoT - Leçon 1 : Configurer l’appareil | Microsoft Docs"
description: "Configurez Intel Edison pour une première utilisation."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "configuration arduino, connecter arduino à un pc, configurer arduino, carte arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 372c9b6d-e701-4ff6-8151-d262aa76aa55
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 87bf3a917af096e43a43a2143afa4bf43a72d7fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="5fd0c-104">Configurer votre Intel Edison</span><span class="sxs-lookup"><span data-stu-id="5fd0c-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5fd0c-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="5fd0c-105">What you will do</span></span>
<span data-ttu-id="5fd0c-106">Configurez Intel Edison pour une première utilisation en assemblant la carte, en la mettant sous tension et en installant l’outil de configuration sur le système d’exploitation de votre ordinateur afin de flasher le microprogramme d’Edison, de définir son mot de passe et de le connecter au réseau Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-106">Configure Intel Edison for first-time use by assembling the board, powering it up and installing configuration tool to your desktop OS to flash Edison's firmware, set its password and connect it to Wi-Fi.</span></span> <span data-ttu-id="5fd0c-107">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="5fd0c-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5fd0c-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="5fd0c-108">What you will learn</span></span>
<span data-ttu-id="5fd0c-109">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5fd0c-109">In this article, you will learn:</span></span>

* <span data-ttu-id="5fd0c-110">Comment assembler la carte Edison et la mettre sous tension.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-110">How to assemble Edison board and power it up.</span></span>
* <span data-ttu-id="5fd0c-111">Comment flasher le microprogramme d’Edison, définir un mot de passe et connecter le Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-111">How to flash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5fd0c-112">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="5fd0c-112">What you need</span></span>
<span data-ttu-id="5fd0c-113">Pour cette opération, vous aurez besoin des composants suivants de votre Kit de démarrage Intel Edison :</span><span class="sxs-lookup"><span data-stu-id="5fd0c-113">To complete this operation, you need the following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="5fd0c-114">Module Intel® Edison</span><span class="sxs-lookup"><span data-stu-id="5fd0c-114">Intel® Edison module</span></span>
* <span data-ttu-id="5fd0c-115">Carte d’extension Arduino</span><span class="sxs-lookup"><span data-stu-id="5fd0c-115">Arduino expansion board</span></span>
* <span data-ttu-id="5fd0c-116">Les barres de séparation ou vis incluses dans l’emballage, y compris deux vis permettant de fixer le module sur la carte d’extension et quatre jeux de vis et séparateurs en plastique.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-116">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="5fd0c-117">Un câble USB Micro B vers Type A</span><span class="sxs-lookup"><span data-stu-id="5fd0c-117">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="5fd0c-118">Une alimentation en courant continu (CC).</span><span class="sxs-lookup"><span data-stu-id="5fd0c-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="5fd0c-119">La puissance nominale de l’alimentation doit être :</span><span class="sxs-lookup"><span data-stu-id="5fd0c-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="5fd0c-120">7-15 V CC</span><span class="sxs-lookup"><span data-stu-id="5fd0c-120">7-15V DC</span></span>
  - <span data-ttu-id="5fd0c-121">Au moins 1 500 mA</span><span class="sxs-lookup"><span data-stu-id="5fd0c-121">At least 1500mA</span></span>
  - <span data-ttu-id="5fd0c-122">La broche centrale/intérieure doit être le pôle positif de l’alimentation</span><span class="sxs-lookup"><span data-stu-id="5fd0c-122">The center/inner pin should be the positive pole of the power supply</span></span>

  ![Éléments de votre Starter Kit](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="5fd0c-124">Vous aurez également besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5fd0c-124">You also need:</span></span>

* <span data-ttu-id="5fd0c-125">Un ordinateur exécutant Windows, Mac ou Linux.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="5fd0c-126">Une connexion sans fil pour la connexion d’Edison.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-126">A wireless connection for Edison to connect to.</span></span>
* <span data-ttu-id="5fd0c-127">Une connexion Internet pour télécharger l’outil de configuration.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-127">An Internet connection to download configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="5fd0c-128">Assembler votre carte</span><span class="sxs-lookup"><span data-stu-id="5fd0c-128">Assemble your board</span></span>

<span data-ttu-id="5fd0c-129">Cette section présente les étapes permettant de connecter votre module Intel® Edison à votre carte d’extension.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-129">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="5fd0c-130">Placez le module Intel® Edison à l’intérieur du cadre blanc sur votre carte d’extension, en alignant les trous du module avec les vis de la carte d’extension.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-130">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="5fd0c-131">Appuyez sur le module juste en dessous de l’indication `What will you make?` jusqu'à entendre un clic.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-131">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![assemblage de carte 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="5fd0c-133">Utilisez les deux écrous hexagonaux (inclus dans le package) pour fixer le module sur la carte d’extension.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-133">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![assemblage de carte 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="5fd0c-135">Insérez une vis dans un des quatre trous situés dans les coins de la carte d’extension.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-135">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="5fd0c-136">Faites tourner et fixez un des séparateurs en plastique blancs sur la vis.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-136">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![assemblage de carte 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="5fd0c-138">Répétez l'opération pour les trois autres séparateurs situés dans les coins.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-138">Repeat for the other three corner spacers.</span></span>

   ![assemblage de carte 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="5fd0c-140">Votre carte est maintenant assemblée.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-140">Now your board is assembled.</span></span>

   ![carte assemblée](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="5fd0c-142">Mise sous tension d’Edison</span><span class="sxs-lookup"><span data-stu-id="5fd0c-142">Power up Edison</span></span>

1. <span data-ttu-id="5fd0c-143">Branchez le bloc d’alimentation.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-143">Plug in the power supply.</span></span>

   ![Branchement du bloc d'alimentation](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="5fd0c-145">Une LED verte (marquée DS1 sur la carte d’extension Arduino*) doit s’allumer et rester allumée.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-145">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="5fd0c-146">Attendez une minute que la carte finisse de démarrer.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-146">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5fd0c-147">Si vous ne disposez pas d’un bloc d’alimentation CC, vous pouvez toujours alimenter la carte via un port USB.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-147">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="5fd0c-148">Consultez la section `Connect Edison to your computer` pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-148">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="5fd0c-149">Cette procédure de mise sous tension de votre carte peut entraîner un comportement imprévisible de la carte, en particulier si vous utilisez un réseau Wi-Fi ou des moteurs d’entraînement.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-to-your-computer"></a><span data-ttu-id="5fd0c-150">Connexion d’Edison à votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="5fd0c-150">Connect Edison to your computer</span></span>

1. <span data-ttu-id="5fd0c-151">Basculez le microcommutateur vers les deux ports micro-USB afin de placer Edison est en mode appareil.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-151">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="5fd0c-152">Veuillez vous reporter [ici](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode) pour connaître les différences entre le mode appareil et le mode hôte.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Basculement du microcommutateur vers le bas](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="5fd0c-154">Connectez le câble micro USB au port micro USB du haut.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-154">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Port micro USB du haut](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="5fd0c-156">Branchez l’autre extrémité du câble USB à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-156">Plug the other end of USB cable into your computer.</span></span>

   ![USB de l’ordinateur](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="5fd0c-158">Vous saurez que votre carte est entièrement initialisée lorsque l’ordinateur monte un nouveau lecteur (comme lorsque vous insérez une carte SD dans votre ordinateur).</span><span class="sxs-lookup"><span data-stu-id="5fd0c-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="5fd0c-159">Téléchargement et exécution de l’outil de configuration</span><span class="sxs-lookup"><span data-stu-id="5fd0c-159">Download and run the configuration tool</span></span>
<span data-ttu-id="5fd0c-160">Consultez [ce lien](https://software.intel.com/en-us/iot/hardware/edison/downloads) répertorié sous le titre `Installers` pour obtenir le dernier outil de configuration.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-160">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="5fd0c-161">Exécutez l’outil et suivez ses instructions à l'écran en cliquant sur Suivant si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-161">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="5fd0c-162">Flashage du microprogramme</span><span class="sxs-lookup"><span data-stu-id="5fd0c-162">Flash firmware</span></span>
1. <span data-ttu-id="5fd0c-163">Sur la page `Set up options`, cliquez sur `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-163">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="5fd0c-164">Sélectionnez l’image à flasher sur votre carte en effectuant l’une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="5fd0c-164">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="5fd0c-165">Pour télécharger et flasher votre carte avec la dernière image de microprogramme disponible d’Intel, sélectionnez `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-165">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="5fd0c-166">Pour flasher votre carte avec une image que vous avez déjà enregistrée sur votre ordinateur, sélectionnez `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-166">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="5fd0c-167">Recherchez et sélectionnez l’image à flasher sur votre carte.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-167">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="5fd0c-168">L’outil d’installation tente de flasher votre carte.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-168">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="5fd0c-169">L’ensemble du processus de flashage peut prendre jusqu’à 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-169">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="5fd0c-170">Définition du mot de passe</span><span class="sxs-lookup"><span data-stu-id="5fd0c-170">Set password</span></span>
1. <span data-ttu-id="5fd0c-171">Sur la page `Set up options`, cliquez sur `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-171">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="5fd0c-172">Vous pouvez attribuer un nom personnalisé à votre carte Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="5fd0c-173">Cette étape est facultative.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-173">This is optional.</span></span>
3. <span data-ttu-id="5fd0c-174">Tapez un mot de passe pour votre carte, puis cliquez sur `Set password`.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="5fd0c-175">Notez le mot de passe, qui sera utilisé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-175">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="5fd0c-176">Connexion Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="5fd0c-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="5fd0c-177">Sur la page `Set up options`, cliquez sur `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-177">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="5fd0c-178">Attendez environ une minute que votre ordinateur recherche les réseaux Wi-Fi disponibles.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-178">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="5fd0c-179">Dans la liste déroulante `Detected Networks`, sélectionnez votre réseau.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-179">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="5fd0c-180">Dans la liste déroulante `Security`, sélectionnez le type de sécurité du réseau.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-180">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="5fd0c-181">Indiquez vos identifiant et mot de passe, puis cliquez sur `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="5fd0c-182">Notez l’adresse IP, qui sera utilisée ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-182">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="5fd0c-183">Assurez-vous qu’Edison est connecté au même réseau que votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-183">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="5fd0c-184">Votre ordinateur se connecte à votre Edison à l’aide de l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-184">Your computer connects to your Edison by using the IP address.</span></span>

<span data-ttu-id="5fd0c-185">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="5fd0c-185">Congratulations!</span></span> <span data-ttu-id="5fd0c-186">Vous avez réussi à configurer Edison.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="5fd0c-187">Résumé</span><span class="sxs-lookup"><span data-stu-id="5fd0c-187">Summary</span></span>
<span data-ttu-id="5fd0c-188">Dans cet article, vous avez appris à assembler la carte Edison, flasher son microprogramme, définir un mot de passe et connecter la carte au réseau Wi-Fi à l’aide de l’outil de configuration.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-188">In this article, you’ve learned how to assemble the Edison board, flash its firmware, setup password and connect it to Wi-Fi by using configuration tool.</span></span> <span data-ttu-id="5fd0c-189">Notez que la LED n’est pas encore allumée.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-189">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="5fd0c-190">La tâche suivante consiste à installer les outils et le logiciel nécessaires en vue d’exécuter un exemple d’application sur Edison.</span><span class="sxs-lookup"><span data-stu-id="5fd0c-190">The next task is to install the necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fd0c-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5fd0c-191">Next steps</span></span>
<span data-ttu-id="5fd0c-192">[Obtenez les outils][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="5fd0c-192">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md