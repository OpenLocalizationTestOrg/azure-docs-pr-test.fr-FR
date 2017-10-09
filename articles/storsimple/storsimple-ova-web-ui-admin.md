---
title: "web de tableau virtuel aaaStorSimple administration de l’interface utilisateur | Documents Microsoft"
description: "Décrit comment tâches d’administration de base des périphériques de tooperform via l’interface utilisateur web de StorSimple Virtual Array hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a><span data-ttu-id="33a8b-103">Utilisez tooadminister de l’interface utilisateur Web hello votre tableau virtuel StorSimple</span><span class="sxs-lookup"><span data-stu-id="33a8b-103">Use hello Web UI tooadminister your StorSimple Virtual Array</span></span>
![flux du processus d'installation](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="33a8b-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="33a8b-105">Overview</span></span>
<span data-ttu-id="33a8b-106">didacticiels Hello dans cet article s’appliquent toohello Microsoft Azure StorSimple Virtual Array (également appelé hello local périphérique virtuel StorSimple) en cours d’exécution mars 2016 (GA) version en disponibilité générale.</span><span class="sxs-lookup"><span data-stu-id="33a8b-106">hello tutorials in this article apply toohello Microsoft Azure StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="33a8b-107">Cet article décrit certains des flux de travail complexes hello et tâches de gestion qui peuvent être effectuées sur hello StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="33a8b-107">This article describes some of hello complex workflows and management tasks that can be performed on hello StorSimple Virtual Array.</span></span> <span data-ttu-id="33a8b-108">Vous pouvez gérer hello StorSimple Virtual Array à l’aide du service StorSimple Manager de hello UI (tooas référencé hello interface utilisateur du portail) et hello d’interface utilisateur web locale pour appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="33a8b-108">You can manage hello StorSimple Virtual Array using hello StorSimple Manager service UI (referred tooas hello portal UI) and hello local web UI for hello device.</span></span> <span data-ttu-id="33a8b-109">Cet article se concentre sur les tâches hello que vous pouvez effectuer à l’aide de l’interface utilisateur web de hello.</span><span class="sxs-lookup"><span data-stu-id="33a8b-109">This article focuses on hello tasks that you can perform using hello web UI.</span></span>

<span data-ttu-id="33a8b-110">Cet article inclut hello suivant didacticiels :</span><span class="sxs-lookup"><span data-stu-id="33a8b-110">This article includes hello following tutorials:</span></span>

* <span data-ttu-id="33a8b-111">Obtenir la clé de chiffrement de données de service hello</span><span class="sxs-lookup"><span data-stu-id="33a8b-111">Get hello service data encryption key</span></span>
* <span data-ttu-id="33a8b-112">Résoudre les erreurs d'installation de l'interface utilisateur web</span><span class="sxs-lookup"><span data-stu-id="33a8b-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="33a8b-113">Générer un package de journaux</span><span class="sxs-lookup"><span data-stu-id="33a8b-113">Generate a log package</span></span>
* <span data-ttu-id="33a8b-114">Arrêter ou redémarrer votre appareil</span><span class="sxs-lookup"><span data-stu-id="33a8b-114">Shut down or restart your device</span></span>

## <a name="get-hello-service-data-encryption-key"></a><span data-ttu-id="33a8b-115">Obtenir la clé de chiffrement de données de service hello</span><span class="sxs-lookup"><span data-stu-id="33a8b-115">Get hello service data encryption key</span></span>
<span data-ttu-id="33a8b-116">Une clé de chiffrement de données de service est générée lorsque vous enregistrez votre premier appareil auprès hello service StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="33a8b-116">A service data encryption key is generated when you register your first device with hello StorSimple Manager service.</span></span> <span data-ttu-id="33a8b-117">Cette clé est alors requise avec hello service d’inscription tooregister clé des unités supplémentaires dans hello service StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="33a8b-117">This key is then required with hello service registration key tooregister additional devices with hello StorSimple Manager service.</span></span>

<span data-ttu-id="33a8b-118">Si vous avez égaré votre clé de chiffrement de données de service et que vous avez besoin de tooretrieve, hello suivants comme suit dans hello local interface utilisateur web de périphérique de hello inscrits auprès du service.</span><span class="sxs-lookup"><span data-stu-id="33a8b-118">If you have misplaced your service data encryption key and need tooretrieve it, perform hello following steps in hello local web UI of hello device registered with your service.</span></span>

#### <a name="tooget-hello-service-data-encryption-key"></a><span data-ttu-id="33a8b-119">clé de chiffrement de données tooget hello service</span><span class="sxs-lookup"><span data-stu-id="33a8b-119">tooget hello service data encryption key</span></span>
1. <span data-ttu-id="33a8b-120">Se connecter toohello interface utilisateur web de locale.</span><span class="sxs-lookup"><span data-stu-id="33a8b-120">Connect toohello local web UI.</span></span> <span data-ttu-id="33a8b-121">Accédez trop**Configuration** > **paramètres Cloud**.</span><span class="sxs-lookup"><span data-stu-id="33a8b-121">Go too**Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="33a8b-122">Au bas de hello de page de hello, cliquez sur **clé de chiffrement de données de service Get**.</span><span class="sxs-lookup"><span data-stu-id="33a8b-122">At hello bottom of hello page, click **Get service data encryption key**.</span></span> <span data-ttu-id="33a8b-123">Une clé s'affiche.</span><span class="sxs-lookup"><span data-stu-id="33a8b-123">A key will appear.</span></span> <span data-ttu-id="33a8b-124">Copiez et enregistrez cette clé.</span><span class="sxs-lookup"><span data-stu-id="33a8b-124">Copy and save this key.</span></span>
   
    ![obtenir la clé de chiffrement des données du service 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="33a8b-126">Résoudre les erreurs d'installation de l'interface utilisateur web</span><span class="sxs-lookup"><span data-stu-id="33a8b-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="33a8b-127">Dans certains cas lorsque vous configurez le périphérique hello via web locale de hello l’interface utilisateur, vous pouvez exécuter des erreurs.</span><span class="sxs-lookup"><span data-stu-id="33a8b-127">In some instances when you configure hello device through hello local web UI, you might run into errors.</span></span> <span data-ttu-id="33a8b-128">toodiagnose et résoudre de telles erreurs, vous pouvez exécuter des tests de diagnostic hello.</span><span class="sxs-lookup"><span data-stu-id="33a8b-128">toodiagnose and troubleshoot such errors, you can run hello diagnostics tests.</span></span>

#### <a name="toorun-hello-diagnostic-tests"></a><span data-ttu-id="33a8b-129">tests de diagnostic de hello toorun</span><span class="sxs-lookup"><span data-stu-id="33a8b-129">toorun hello diagnostic tests</span></span>
1. <span data-ttu-id="33a8b-130">Dans l’interface utilisateur de web locale hello, accédez trop**dépannage** > **tests de Diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="33a8b-130">In hello local web UI, go too**Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![exécuter les diagnostics 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="33a8b-132">Au bas de hello de page de hello, cliquez sur **exécuter les Tests de Diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="33a8b-132">At hello bottom of hello page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="33a8b-133">Ceci lancera tests toodiagnose les éventuels problèmes de votre réseau, un périphérique, un proxy web, une heure ou un paramètres de cloud.</span><span class="sxs-lookup"><span data-stu-id="33a8b-133">This will initiate tests toodiagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="33a8b-134">Vous serez averti que cet appareil hello est en cours d’exécution des tests.</span><span class="sxs-lookup"><span data-stu-id="33a8b-134">You will be notified that hello device is running tests.</span></span>
3. <span data-ttu-id="33a8b-135">Une fois les tests hello terminées, les résultats hello seront affichera.</span><span class="sxs-lookup"><span data-stu-id="33a8b-135">After hello tests have completed, hello results will be displayed.</span></span> <span data-ttu-id="33a8b-136">Hello suivant montre les résultats de hello de tests de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="33a8b-136">hello following example shows hello results of diagnostic tests.</span></span> <span data-ttu-id="33a8b-137">Notez que les paramètres de proxy web hello non configurés sur ce périphérique, et par conséquent, test de proxy web hello n’a pas été exécutée.</span><span class="sxs-lookup"><span data-stu-id="33a8b-137">Note that hello web proxy settings were not configured on this device, and therefore, hello web proxy test was not run.</span></span> <span data-ttu-id="33a8b-138">Tous les hello autres tests pour les paramètres de réseau, serveur DNS, et les paramètres de temps ont réussi.</span><span class="sxs-lookup"><span data-stu-id="33a8b-138">All hello other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![exécuter les diagnostics 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="33a8b-140">Générer un package de journaux</span><span class="sxs-lookup"><span data-stu-id="33a8b-140">Generate a log package</span></span>
<span data-ttu-id="33a8b-141">Un package de journaux est composé de tous les journaux appropriés hello qui peuvent aider le Support technique de Microsoft à résoudre les problèmes de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="33a8b-141">A log package is comprised of all hello relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="33a8b-142">Dans cette version, un package de journaux peut être généré via l’interface utilisateur de web locale hello.</span><span class="sxs-lookup"><span data-stu-id="33a8b-142">In this release, a log package can be generated via hello local web UI.</span></span>

#### <a name="toogenerate-hello-log-package"></a><span data-ttu-id="33a8b-143">package de journaux hello toogenerate</span><span class="sxs-lookup"><span data-stu-id="33a8b-143">toogenerate hello log package</span></span>
1. <span data-ttu-id="33a8b-144">Dans l’interface utilisateur de web locale hello, accédez trop**dépannage** > **journaux système**.</span><span class="sxs-lookup"><span data-stu-id="33a8b-144">In hello local web UI, go too**Troubleshooting** > **System logs**.</span></span>
   
    ![générer un package de journaux 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="33a8b-146">Au bas de hello de page de hello, cliquez sur **créer un package journal**.</span><span class="sxs-lookup"><span data-stu-id="33a8b-146">At hello bottom of hello page, click **Create log package**.</span></span> <span data-ttu-id="33a8b-147">Un package de journaux du système hello va être créé.</span><span class="sxs-lookup"><span data-stu-id="33a8b-147">A package of hello system logs will be created.</span></span> <span data-ttu-id="33a8b-148">Cette opération prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="33a8b-148">This will take a couple of minutes.</span></span>
   
    ![générer un package de journaux 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="33a8b-150">Vous serez averti une fois hello package a été créé et hello page sera actualisée temps de hello tooindicate et date de création de package de hello.</span><span class="sxs-lookup"><span data-stu-id="33a8b-150">You will be notified after hello package is successfully created, and hello page will be updated tooindicate hello time and date when hello package was created.</span></span>
   
    ![générer un package de journaux 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="33a8b-152">Cliquez sur **Télécharger le package de journaux**.</span><span class="sxs-lookup"><span data-stu-id="33a8b-152">Click **Download log package**.</span></span> <span data-ttu-id="33a8b-153">Un package zippé sera téléchargé sur votre système.</span><span class="sxs-lookup"><span data-stu-id="33a8b-153">A zipped package will be downloaded on your system.</span></span>
   
    ![générer un package de journaux 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="33a8b-155">Vous pouvez décompresser le package de journaux téléchargé de hello et afficher les fichiers journaux du système hello.</span><span class="sxs-lookup"><span data-stu-id="33a8b-155">You can unzip hello downloaded log package and view hello system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="33a8b-156">Arrêter et redémarrer votre appareil</span><span class="sxs-lookup"><span data-stu-id="33a8b-156">Shut down and restart your device</span></span>
<span data-ttu-id="33a8b-157">Vous pouvez arrêter ou redémarrer votre appareil virtuel à l’aide de l’interface utilisateur de web local hello.</span><span class="sxs-lookup"><span data-stu-id="33a8b-157">You can shut down or restart your virtual device using hello local web UI.</span></span> <span data-ttu-id="33a8b-158">Nous recommandons que, avant de redémarrer, prendre des volumes de hello ou partages en mode hors connexion sur l’ordinateur hôte de hello et puis hello appareil.</span><span class="sxs-lookup"><span data-stu-id="33a8b-158">We recommend that before you restart, take hello volumes or shares offline on hello host and then hello device.</span></span> <span data-ttu-id="33a8b-159">Vous réduisez ainsi toute possibilité d’altération des données.</span><span class="sxs-lookup"><span data-stu-id="33a8b-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="tooshut-down-your-virtual-device"></a><span data-ttu-id="33a8b-160">tooshut vers le bas de votre appareil virtuel</span><span class="sxs-lookup"><span data-stu-id="33a8b-160">tooshut down your virtual device</span></span>
1. <span data-ttu-id="33a8b-161">Dans l’interface utilisateur de web locale hello, accédez trop**Maintenance** > **paramètres d’alimentation**.</span><span class="sxs-lookup"><span data-stu-id="33a8b-161">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="33a8b-162">Au bas de hello de page de hello, cliquez sur **arrêt**.</span><span class="sxs-lookup"><span data-stu-id="33a8b-162">At hello bottom of hello page, click **Shutdown**.</span></span>
   
    ![arrêter l'appareil 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="33a8b-164">Un avertissement s’affiche indiquant qu’un arrêt de l’appareil de hello interrompra d’e/s à qui étaient en cours d’exécution, ce qui entraîne un temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="33a8b-164">A warning will appear stating that a shutdown of hello device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="33a8b-165">Cliquez sur une icône de coche hello</span><span class="sxs-lookup"><span data-stu-id="33a8b-165">Click hello check icon</span></span> ![icône en forme de coche](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="33a8b-167">.</span><span class="sxs-lookup"><span data-stu-id="33a8b-167">.</span></span>
   
    ![avertissement d'arrêt de l'appareil](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="33a8b-169">Vous serez averti qu’un arrêt hello a été lancé.</span><span class="sxs-lookup"><span data-stu-id="33a8b-169">You will be notified that hello shutdown has been initiated.</span></span>
   
    ![arrêt de l'appareil initié](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="33a8b-171">Appareil de Hello va s’arrêter.</span><span class="sxs-lookup"><span data-stu-id="33a8b-171">hello device will now shut down.</span></span> <span data-ttu-id="33a8b-172">Si vous souhaitez toostart votre appareil, vous devez toodo qui, par le biais hello Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="33a8b-172">If you want toostart your device, you will need toodo that through hello Hyper-V Manager.</span></span>

#### <a name="toorestart-your-virtual-device"></a><span data-ttu-id="33a8b-173">toorestart votre appareil virtuel</span><span class="sxs-lookup"><span data-stu-id="33a8b-173">toorestart your virtual device</span></span>
1. <span data-ttu-id="33a8b-174">Dans l’interface utilisateur de web locale hello, accédez trop**Maintenance** > **paramètres d’alimentation**.</span><span class="sxs-lookup"><span data-stu-id="33a8b-174">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="33a8b-175">Au bas de hello de page de hello, cliquez sur **redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="33a8b-175">At hello bottom of hello page, click **Restart**.</span></span>
   
    ![redémarrer l'appareil](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="33a8b-177">Un avertissement s’affiche indiquant que cet appareil hello redémarrage interrompra tout IOs qui étaient en cours d’exécution, ce qui entraîne un temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="33a8b-177">A warning will appear stating that restarting hello device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="33a8b-178">Cliquez sur une icône de coche hello</span><span class="sxs-lookup"><span data-stu-id="33a8b-178">Click hello check icon</span></span> ![icône en forme de coche](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="33a8b-180">.</span><span class="sxs-lookup"><span data-stu-id="33a8b-180">.</span></span>
   
    ![avertissement de redémarrage](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="33a8b-182">Vous serez averti que le redémarrage hello a été lancé.</span><span class="sxs-lookup"><span data-stu-id="33a8b-182">You will be notified that hello restart has been initiated.</span></span>
   
    ![redémarrage initié](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="33a8b-184">Pendant le redémarrage de hello est en cours d’exécution, vous perdrez hello connexion toohello l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="33a8b-184">While hello restart is in progress, you will lose hello connection toohello UI.</span></span> <span data-ttu-id="33a8b-185">Vous pouvez surveiller hello redémarrage en actualisant hello UI régulièrement.</span><span class="sxs-lookup"><span data-stu-id="33a8b-185">You can monitor hello restart by refreshing hello UI periodically.</span></span> <span data-ttu-id="33a8b-186">Vous pouvez aussi surveiller état de redémarrage du périphérique hello via hello Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="33a8b-186">Alternatively, you can monitor hello device restart status through hello Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33a8b-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="33a8b-187">Next steps</span></span>
<span data-ttu-id="33a8b-188">Découvrez comment trop[utilisez hello toomanage du service StorSimple Manager de votre appareil](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="33a8b-188">Learn how too[use hello StorSimple Manager service toomanage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

