---
title: "Se connecter tooAzure Intel Edison (nœud) IoT - leçon 1 : configurer l’appareil | Documents Microsoft"
description: "Configurez Intel Edison pour une première utilisation."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino configuré, connectez-vous arduino toopc, le programme d’installation arduino, arduino carte"
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
ms.openlocfilehash: c0609542a49924c979f71297d808c09acefca0bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="00f16-104">Configurer votre Intel Edison</span><span class="sxs-lookup"><span data-stu-id="00f16-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="00f16-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="00f16-105">What you will do</span></span>
<span data-ttu-id="00f16-106">Configurer Intel Edison pour la première utilisation en assemblant tableau hello, en cours de l’installation de configuration outil tooyour bureau du système d’exploitation tooflash microprogramme Edison ensemble et son mot de passe connectez-la tooWi Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="00f16-106">Configure Intel Edison for first-time use by assembling hello board, powering it up and installing configuration tool tooyour desktop OS tooflash Edison's firmware, set its password and connect it tooWi-Fi.</span></span> <span data-ttu-id="00f16-107">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="00f16-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="00f16-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="00f16-108">What you will learn</span></span>
<span data-ttu-id="00f16-109">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="00f16-109">In this article, you will learn:</span></span>

* <span data-ttu-id="00f16-110">Comment tooassemble Edison board et mettez-le sous tension.</span><span class="sxs-lookup"><span data-stu-id="00f16-110">How tooassemble Edison board and power it up.</span></span>
* <span data-ttu-id="00f16-111">Comment les microprogrammes tooflash Edison, mot de passe et vous y connecter Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="00f16-111">How tooflash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="00f16-112">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="00f16-112">What you need</span></span>
<span data-ttu-id="00f16-113">toocomplete cette opération, vous devez hello pièces suivantes à partir de votre Intel Edison Starter Kit :</span><span class="sxs-lookup"><span data-stu-id="00f16-113">toocomplete this operation, you need hello following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="00f16-114">Module Intel® Edison</span><span class="sxs-lookup"><span data-stu-id="00f16-114">Intel® Edison module</span></span>
* <span data-ttu-id="00f16-115">Carte d’extension Arduino</span><span class="sxs-lookup"><span data-stu-id="00f16-115">Arduino expansion board</span></span>
* <span data-ttu-id="00f16-116">Les barres d’espacement ni vis inclus dans le package hello, y compris des deux vis toofasten hello toohello expansion carte et quatre ensembles de vis et des séparateurs en plastique.</span><span class="sxs-lookup"><span data-stu-id="00f16-116">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="00f16-117">Un câble USB d’un de tooType Micro B</span><span class="sxs-lookup"><span data-stu-id="00f16-117">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="00f16-118">Une alimentation en courant continu (CC).</span><span class="sxs-lookup"><span data-stu-id="00f16-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="00f16-119">La puissance nominale de l’alimentation doit être :</span><span class="sxs-lookup"><span data-stu-id="00f16-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="00f16-120">7-15 V CC</span><span class="sxs-lookup"><span data-stu-id="00f16-120">7-15V DC</span></span>
  - <span data-ttu-id="00f16-121">Au moins 1 500 mA</span><span class="sxs-lookup"><span data-stu-id="00f16-121">At least 1500mA</span></span>
  - <span data-ttu-id="00f16-122">code confidentiel de Hello center/interne doit être pôle positif de hello d’alimentation hello</span><span class="sxs-lookup"><span data-stu-id="00f16-122">hello center/inner pin should be hello positive pole of hello power supply</span></span>

  ![Éléments de votre Starter Kit](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="00f16-124">Vous aurez également besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="00f16-124">You also need:</span></span>

* <span data-ttu-id="00f16-125">Un ordinateur exécutant Windows, Mac ou Linux.</span><span class="sxs-lookup"><span data-stu-id="00f16-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="00f16-126">Une connexion sans fil pour tooconnect Edison à.</span><span class="sxs-lookup"><span data-stu-id="00f16-126">A wireless connection for Edison tooconnect to.</span></span>
* <span data-ttu-id="00f16-127">Un outil de configuration toodownload de connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="00f16-127">An Internet connection toodownload configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="00f16-128">Assembler votre carte</span><span class="sxs-lookup"><span data-stu-id="00f16-128">Assemble your board</span></span>

<span data-ttu-id="00f16-129">Cette section contient les étapes tooattach votre carte Intel® Edison tooyour d’extension.</span><span class="sxs-lookup"><span data-stu-id="00f16-129">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="00f16-130">Placez le module Intel® Edison hello hiérarchique de hello blanc dans votre tableau d’extension, de trous hello sur le module de hello avec vis hello sur la carte d’extension de hello s’aligne.</span><span class="sxs-lookup"><span data-stu-id="00f16-130">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="00f16-131">Appuyez sur le module hello juste en dessous des mots hello `What will you make?` jusqu'à ce que vous pensez qu’un composant logiciel enfichable.</span><span class="sxs-lookup"><span data-stu-id="00f16-131">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![assemblage de carte 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="00f16-133">Utilisez hello deux fruits hex (inclus dans le package de hello) toosecure hello toohello expansion carte.</span><span class="sxs-lookup"><span data-stu-id="00f16-133">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![assemblage de carte 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="00f16-135">Insérer une vis de l’une des quatre trous de coin hello sur la carte d’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="00f16-135">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="00f16-136">Torsion et renforcer un des séparateurs de plastique hello blanc sur vis de hello.</span><span class="sxs-lookup"><span data-stu-id="00f16-136">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![assemblage de carte 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="00f16-138">Répétez cette opération pour hello autres séparateurs trois angle.</span><span class="sxs-lookup"><span data-stu-id="00f16-138">Repeat for hello other three corner spacers.</span></span>

   ![assemblage de carte 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="00f16-140">Votre carte est maintenant assemblée.</span><span class="sxs-lookup"><span data-stu-id="00f16-140">Now your board is assembled.</span></span>

   ![carte assemblée](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="00f16-142">Mise sous tension d’Edison</span><span class="sxs-lookup"><span data-stu-id="00f16-142">Power up Edison</span></span>

1. <span data-ttu-id="00f16-143">Branchez alimentation hello.</span><span class="sxs-lookup"><span data-stu-id="00f16-143">Plug in hello power supply.</span></span>

   ![Branchement du bloc d'alimentation](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="00f16-145">Une DEL verte (étiquetée DS1 sur hello Arduino * de carte d’extension) doit s’allumer et restent allumée.</span><span class="sxs-lookup"><span data-stu-id="00f16-145">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="00f16-146">Patientez une minute pour toofinish de tableau hello le démarrage.</span><span class="sxs-lookup"><span data-stu-id="00f16-146">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="00f16-147">Si vous ne disposez pas d’une alimentation de contrôleur de domaine, vous pouvez toujours de carte hello l’alimentation via un port USB.</span><span class="sxs-lookup"><span data-stu-id="00f16-147">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="00f16-148">Consultez la section `Connect Edison tooyour computer` pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="00f16-148">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="00f16-149">Cette procédure de mise sous tension de votre carte peut entraîner un comportement imprévisible de la carte, en particulier si vous utilisez un réseau Wi-Fi ou des moteurs d’entraînement.</span><span class="sxs-lookup"><span data-stu-id="00f16-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="00f16-150">Connectez Edison tooyour ordinateur</span><span class="sxs-lookup"><span data-stu-id="00f16-150">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="00f16-151">Basculer vers le bas microrupteur hello vers hello deux micro ports USB, afin que Edison est en mode de périphérique.</span><span class="sxs-lookup"><span data-stu-id="00f16-151">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="00f16-152">Veuillez vous reporter [ici](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode) pour connaître les différences entre le mode appareil et le mode hôte.</span><span class="sxs-lookup"><span data-stu-id="00f16-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Basculer vers le bas microrupteur de hello](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="00f16-154">Branchez les câbles USB micro hello le port USB supérieur micro hello.</span><span class="sxs-lookup"><span data-stu-id="00f16-154">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Port micro USB du haut](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="00f16-156">Plug hello l’autre extrémité du câble USB à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="00f16-156">Plug hello other end of USB cable into your computer.</span></span>

   ![USB de l’ordinateur](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="00f16-158">Vous saurez que votre carte est entièrement initialisée lorsque l’ordinateur monte un nouveau lecteur (comme lorsque vous insérez une carte SD dans votre ordinateur).</span><span class="sxs-lookup"><span data-stu-id="00f16-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="00f16-159">Téléchargez et exécutez l’outil de configuration hello</span><span class="sxs-lookup"><span data-stu-id="00f16-159">Download and run hello configuration tool</span></span>
<span data-ttu-id="00f16-160">Obtenir hello dernier outil de configuration à partir de [ce lien](https://software.intel.com/en-us/iot/hardware/edison/downloads) répertoriés sous hello `Installers` titre.</span><span class="sxs-lookup"><span data-stu-id="00f16-160">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="00f16-161">Exécutez l’outil de hello et suivez sa à l’écran des instructions, en cliquant sur Suivant si nécessaire</span><span class="sxs-lookup"><span data-stu-id="00f16-161">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="00f16-162">Flashage du microprogramme</span><span class="sxs-lookup"><span data-stu-id="00f16-162">Flash firmware</span></span>
1. <span data-ttu-id="00f16-163">Sur hello `Set up options` , cliquez sur `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="00f16-163">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="00f16-164">Sélectionnez tooflash d’image hello sur votre carte mère en effectuant l’une des manières suivantes les hello :</span><span class="sxs-lookup"><span data-stu-id="00f16-164">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="00f16-165">toodownload et flash votre carte mère avec hello dernière image de microprogramme auprès d’Intel, sélectionnez `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="00f16-165">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="00f16-166">sélectionner de votre tableau avec une image que vous avez déjà enregistré sur votre ordinateur, tooflash `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="00f16-166">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="00f16-167">Parcourir tooand hello sélectionnez image de carte de tooyour tooflash.</span><span class="sxs-lookup"><span data-stu-id="00f16-167">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="00f16-168">outil de configuration Hello va tenter de tooflash votre carte mère.</span><span class="sxs-lookup"><span data-stu-id="00f16-168">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="00f16-169">processus clignotant Hello peut prendre jusqu'à too10 minutes.</span><span class="sxs-lookup"><span data-stu-id="00f16-169">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="00f16-170">Définition du mot de passe</span><span class="sxs-lookup"><span data-stu-id="00f16-170">Set password</span></span>
1. <span data-ttu-id="00f16-171">Sur hello `Set up options` , cliquez sur `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="00f16-171">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="00f16-172">Vous pouvez attribuer un nom personnalisé à votre carte Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="00f16-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="00f16-173">Cette étape est facultative.</span><span class="sxs-lookup"><span data-stu-id="00f16-173">This is optional.</span></span>
3. <span data-ttu-id="00f16-174">Tapez un mot de passe pour votre carte, puis cliquez sur `Set password`.</span><span class="sxs-lookup"><span data-stu-id="00f16-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="00f16-175">Démarquer hello un mot de passe qui sera utilisé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="00f16-175">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="00f16-176">Connexion Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="00f16-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="00f16-177">Sur hello `Set up options` , cliquez sur `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="00f16-177">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="00f16-178">Attente d’une minute tooone sous la forme d’analyses de votre ordinateur pour les réseaux Wi-Fi disponibles.</span><span class="sxs-lookup"><span data-stu-id="00f16-178">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="00f16-179">À partir de hello `Detected Networks` liste déroulante, sélectionnez votre réseau.</span><span class="sxs-lookup"><span data-stu-id="00f16-179">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="00f16-180">À partir de hello `Security` liste déroulante, le type de sécurité du réseau : sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="00f16-180">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="00f16-181">Indiquez vos identifiant et mot de passe, puis cliquez sur `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="00f16-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="00f16-182">Démarquer hello adresse IP, qui est utilisée ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="00f16-182">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="00f16-183">Assurez-vous que Edison est connecté toohello même réseau que votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="00f16-183">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="00f16-184">Votre ordinateur connecte tooyour Edison en utilisant l’adresse IP de hello.</span><span class="sxs-lookup"><span data-stu-id="00f16-184">Your computer connects tooyour Edison by using hello IP address.</span></span>

<span data-ttu-id="00f16-185">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="00f16-185">Congratulations!</span></span> <span data-ttu-id="00f16-186">Vous avez réussi à configurer Edison.</span><span class="sxs-lookup"><span data-stu-id="00f16-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="00f16-187">Résumé</span><span class="sxs-lookup"><span data-stu-id="00f16-187">Summary</span></span>
<span data-ttu-id="00f16-188">Dans cet article, vous avez appris comment tooassemble hello du tableau de Edison, flash son microprogramme, le mot de passe le programme d’installation et le connecter tooWi Wi-Fi en utilisant l’outil de configuration.</span><span class="sxs-lookup"><span data-stu-id="00f16-188">In this article, you’ve learned how tooassemble hello Edison board, flash its firmware, setup password and connect it tooWi-Fi by using configuration tool.</span></span> <span data-ttu-id="00f16-189">Notez que hello que voyant ne s’allume encore.</span><span class="sxs-lookup"><span data-stu-id="00f16-189">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="00f16-190">la tâche suivante Hello est tooinstall hello outils et nécessaires logiciel en vue d’un exemple d’application en cours d’exécution sur Edison.</span><span class="sxs-lookup"><span data-stu-id="00f16-190">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00f16-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="00f16-191">Next steps</span></span>
<span data-ttu-id="00f16-192">[Obtenir les outils de hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="00f16-192">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md