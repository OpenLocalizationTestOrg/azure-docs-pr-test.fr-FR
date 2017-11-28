---
title: Administration de l'interface utilisateur web de StorSimple Virtual Array | Microsoft Docs
description: "Décrit comment effectuer des tâches d'administration de base sur l'appareil avec l'interface utilisateur web de StorSimple Virtual Array."
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
ms.openlocfilehash: 989e7b697f9b527df549fb32be18edd1d3c8d224
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-web-ui-to-administer-your-storsimple-virtual-array"></a><span data-ttu-id="40a5d-103">Utiliser l'interface utilisateur web pour gérer votre StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="40a5d-103">Use the Web UI to administer your StorSimple Virtual Array</span></span>
![flux du processus d'installation](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="40a5d-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="40a5d-105">Overview</span></span>
<span data-ttu-id="40a5d-106">Les didacticiels de cet article s'appliquent à Microsoft Azure StorSimple Virtual Array (également appelé appareil virtuel StorSimple local) exécutant la version de mise à la disposition générale (mars 2016).</span><span class="sxs-lookup"><span data-stu-id="40a5d-106">The tutorials in this article apply to the Microsoft Azure StorSimple Virtual Array (also known as the StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="40a5d-107">Cet article décrit certains des flux de travail et certaines tâches de gestion complexes qui peuvent être effectués sur StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="40a5d-107">This article describes some of the complex workflows and management tasks that can be performed on the StorSimple Virtual Array.</span></span> <span data-ttu-id="40a5d-108">Vous pouvez gérer StorSimple Virtual Array à l’aide de l'interface utilisateur du service StorSimple Manager (également appelée interface utilisateur du portail) et de l'interface utilisateur web locale de l'appareil.</span><span class="sxs-lookup"><span data-stu-id="40a5d-108">You can manage the StorSimple Virtual Array using the StorSimple Manager service UI (referred to as the portal UI) and the local web UI for the device.</span></span> <span data-ttu-id="40a5d-109">Cet article se concentre sur les tâches que vous pouvez effectuer à l'aide de l'interface utilisateur web.</span><span class="sxs-lookup"><span data-stu-id="40a5d-109">This article focuses on the tasks that you can perform using the web UI.</span></span>

<span data-ttu-id="40a5d-110">Cet article inclut les didacticiels suivants :</span><span class="sxs-lookup"><span data-stu-id="40a5d-110">This article includes the following tutorials:</span></span>

* <span data-ttu-id="40a5d-111">Obtenir la clé de chiffrement des données de service</span><span class="sxs-lookup"><span data-stu-id="40a5d-111">Get the service data encryption key</span></span>
* <span data-ttu-id="40a5d-112">Résoudre les erreurs d'installation de l'interface utilisateur web</span><span class="sxs-lookup"><span data-stu-id="40a5d-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="40a5d-113">Générer un package de journaux</span><span class="sxs-lookup"><span data-stu-id="40a5d-113">Generate a log package</span></span>
* <span data-ttu-id="40a5d-114">Arrêter ou redémarrer votre appareil</span><span class="sxs-lookup"><span data-stu-id="40a5d-114">Shut down or restart your device</span></span>

## <a name="get-the-service-data-encryption-key"></a><span data-ttu-id="40a5d-115">Obtenir la clé de chiffrement des données de service</span><span class="sxs-lookup"><span data-stu-id="40a5d-115">Get the service data encryption key</span></span>
<span data-ttu-id="40a5d-116">Une clé de chiffrement des données de service est générée lorsque vous enregistrez votre premier appareil auprès du service StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="40a5d-116">A service data encryption key is generated when you register your first device with the StorSimple Manager service.</span></span> <span data-ttu-id="40a5d-117">Cette clé et la clé d'enregistrement de service sont ensuite requises pour l'inscription d'appareils supplémentaires avec le service StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="40a5d-117">This key is then required with the service registration key to register additional devices with the StorSimple Manager service.</span></span>

<span data-ttu-id="40a5d-118">Si vous avez égaré votre clé de chiffrement des données de service, procédez comme suit dans l'interface utilisateur web locale de l'appareil inscrit auprès du service pour la récupérer.</span><span class="sxs-lookup"><span data-stu-id="40a5d-118">If you have misplaced your service data encryption key and need to retrieve it, perform the following steps in the local web UI of the device registered with your service.</span></span>

#### <a name="to-get-the-service-data-encryption-key"></a><span data-ttu-id="40a5d-119">Pour obtenir la clé de chiffrement des données de service</span><span class="sxs-lookup"><span data-stu-id="40a5d-119">To get the service data encryption key</span></span>
1. <span data-ttu-id="40a5d-120">Connectez-vous à l'interface utilisateur web locale.</span><span class="sxs-lookup"><span data-stu-id="40a5d-120">Connect to the local web UI.</span></span> <span data-ttu-id="40a5d-121">Accédez à **Configuration** > **Paramètres du Cloud**.</span><span class="sxs-lookup"><span data-stu-id="40a5d-121">Go to **Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="40a5d-122">En bas de la page, cliquez sur **Obtenir la clé de chiffrement de données du service**.</span><span class="sxs-lookup"><span data-stu-id="40a5d-122">At the bottom of the page, click **Get service data encryption key**.</span></span> <span data-ttu-id="40a5d-123">Une clé s'affiche.</span><span class="sxs-lookup"><span data-stu-id="40a5d-123">A key will appear.</span></span> <span data-ttu-id="40a5d-124">Copiez et enregistrez cette clé.</span><span class="sxs-lookup"><span data-stu-id="40a5d-124">Copy and save this key.</span></span>
   
    ![obtenir la clé de chiffrement des données du service 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="40a5d-126">Résoudre les erreurs d'installation de l'interface utilisateur web</span><span class="sxs-lookup"><span data-stu-id="40a5d-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="40a5d-127">Dans certains cas, lorsque vous configurez l'appareil via l'interface utilisateur web locale, vous pouvez rencontrer les erreurs.</span><span class="sxs-lookup"><span data-stu-id="40a5d-127">In some instances when you configure the device through the local web UI, you might run into errors.</span></span> <span data-ttu-id="40a5d-128">Pour diagnostiquer et résoudre de telles erreurs, vous pouvez exécuter les tests de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="40a5d-128">To diagnose and troubleshoot such errors, you can run the diagnostics tests.</span></span>

#### <a name="to-run-the-diagnostic-tests"></a><span data-ttu-id="40a5d-129">Pour exécuter les tests de diagnostic</span><span class="sxs-lookup"><span data-stu-id="40a5d-129">To run the diagnostic tests</span></span>
1. <span data-ttu-id="40a5d-130">Dans l’interface utilisateur web locale, accédez à **Dépannage** > **Tests de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="40a5d-130">In the local web UI, go to **Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![exécuter les diagnostics 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="40a5d-132">En bas de la page, cliquez sur **Exécuter les tests de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="40a5d-132">At the bottom of the page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="40a5d-133">Cette opération lance des tests pour diagnostiquer les éventuels problèmes sur votre réseau, appareil, proxy web, horodatage ou paramètres cloud.</span><span class="sxs-lookup"><span data-stu-id="40a5d-133">This will initiate tests to diagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="40a5d-134">Vous serez averti que des tests sont en cours sur l'appareil.</span><span class="sxs-lookup"><span data-stu-id="40a5d-134">You will be notified that the device is running tests.</span></span>
3. <span data-ttu-id="40a5d-135">Une fois les tests terminés, les résultats seront affichés.</span><span class="sxs-lookup"><span data-stu-id="40a5d-135">After the tests have completed, the results will be displayed.</span></span> <span data-ttu-id="40a5d-136">L'exemple suivant illustre les résultats des tests de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="40a5d-136">The following example shows the results of diagnostic tests.</span></span> <span data-ttu-id="40a5d-137">Notez que les paramètres du proxy web n'étaient pas configurés sur cet appareil et, par conséquent, le test de proxy web n'a pas été exécuté.</span><span class="sxs-lookup"><span data-stu-id="40a5d-137">Note that the web proxy settings were not configured on this device, and therefore, the web proxy test was not run.</span></span> <span data-ttu-id="40a5d-138">Tous les autres tests pour les paramètres réseau, le serveur DNS et les paramètres d'heure ont été effectués.</span><span class="sxs-lookup"><span data-stu-id="40a5d-138">All the other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![exécuter les diagnostics 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="40a5d-140">Générer un package de journaux</span><span class="sxs-lookup"><span data-stu-id="40a5d-140">Generate a log package</span></span>
<span data-ttu-id="40a5d-141">Un package de journaux contient tous les journaux pertinents qui peuvent aider l'équipe de support technique de Microsoft à résoudre les problèmes des appareils.</span><span class="sxs-lookup"><span data-stu-id="40a5d-141">A log package is comprised of all the relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="40a5d-142">Dans cette version, vous pouvez générer un package de journaux via l'interface utilisateur web locale.</span><span class="sxs-lookup"><span data-stu-id="40a5d-142">In this release, a log package can be generated via the local web UI.</span></span>

#### <a name="to-generate-the-log-package"></a><span data-ttu-id="40a5d-143">Pour générer le package de journaux</span><span class="sxs-lookup"><span data-stu-id="40a5d-143">To generate the log package</span></span>
1. <span data-ttu-id="40a5d-144">Dans l’interface utilisateur web locale, accédez à **Dépannage** > **Journaux système**.</span><span class="sxs-lookup"><span data-stu-id="40a5d-144">In the local web UI, go to **Troubleshooting** > **System logs**.</span></span>
   
    ![générer un package de journaux 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="40a5d-146">En bas de la page, cliquez sur **Créer un package de journaux**.</span><span class="sxs-lookup"><span data-stu-id="40a5d-146">At the bottom of the page, click **Create log package**.</span></span> <span data-ttu-id="40a5d-147">Un package des journaux système sera créé.</span><span class="sxs-lookup"><span data-stu-id="40a5d-147">A package of the system logs will be created.</span></span> <span data-ttu-id="40a5d-148">Cette opération prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="40a5d-148">This will take a couple of minutes.</span></span>
   
    ![générer un package de journaux 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="40a5d-150">Vous serez averti une fois le package créé et la page sera actualisée pour indiquer l'heure et la date de création du package.</span><span class="sxs-lookup"><span data-stu-id="40a5d-150">You will be notified after the package is successfully created, and the page will be updated to indicate the time and date when the package was created.</span></span>
   
    ![générer un package de journaux 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="40a5d-152">Cliquez sur **Télécharger le package de journaux**.</span><span class="sxs-lookup"><span data-stu-id="40a5d-152">Click **Download log package**.</span></span> <span data-ttu-id="40a5d-153">Un package zippé sera téléchargé sur votre système.</span><span class="sxs-lookup"><span data-stu-id="40a5d-153">A zipped package will be downloaded on your system.</span></span>
   
    ![générer un package de journaux 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="40a5d-155">Vous pouvez décompresser le package de journaux téléchargé et afficher les fichiers journaux système.</span><span class="sxs-lookup"><span data-stu-id="40a5d-155">You can unzip the downloaded log package and view the system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="40a5d-156">Arrêter et redémarrer votre appareil</span><span class="sxs-lookup"><span data-stu-id="40a5d-156">Shut down and restart your device</span></span>
<span data-ttu-id="40a5d-157">Vous pouvez arrêter ou redémarrer votre appareil virtuel à l'aide de l'interface utilisateur web locale.</span><span class="sxs-lookup"><span data-stu-id="40a5d-157">You can shut down or restart your virtual device using the local web UI.</span></span> <span data-ttu-id="40a5d-158">Avant de redémarrer, nous vous recommandons de mettre les volumes ou les partages hors connexion sur l’ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="40a5d-158">We recommend that before you restart, take the volumes or shares offline on the host and then the device.</span></span> <span data-ttu-id="40a5d-159">Vous réduisez ainsi toute possibilité d’altération des données.</span><span class="sxs-lookup"><span data-stu-id="40a5d-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="to-shut-down-your-virtual-device"></a><span data-ttu-id="40a5d-160">Pour arrêter votre appareil virtuel</span><span class="sxs-lookup"><span data-stu-id="40a5d-160">To shut down your virtual device</span></span>
1. <span data-ttu-id="40a5d-161">Dans l’interface utilisateur web locale, accédez à **Maintenance** > **Paramètres d'alimentation**.</span><span class="sxs-lookup"><span data-stu-id="40a5d-161">In the local web UI, go to **Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="40a5d-162">Au bas de la page, cliquez sur **Arrêt**.</span><span class="sxs-lookup"><span data-stu-id="40a5d-162">At the bottom of the page, click **Shutdown**.</span></span>
   
    ![arrêter l'appareil 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="40a5d-164">Un avertissement s’affiche indiquant qu’un arrêt de l’appareil va interrompre toutes les E/S qui étaient en cours, ce qui entraîne une interruption du service.</span><span class="sxs-lookup"><span data-stu-id="40a5d-164">A warning will appear stating that a shutdown of the device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="40a5d-165">Cliquez sur l’icône en forme de coche </span><span class="sxs-lookup"><span data-stu-id="40a5d-165">Click the check icon</span></span> ![icône en forme de coche](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="40a5d-167">.</span><span class="sxs-lookup"><span data-stu-id="40a5d-167">.</span></span>
   
    ![avertissement d'arrêt de l'appareil](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="40a5d-169">Vous serez averti que l'arrêt a été initié.</span><span class="sxs-lookup"><span data-stu-id="40a5d-169">You will be notified that the shutdown has been initiated.</span></span>
   
    ![arrêt de l'appareil initié](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="40a5d-171">L'appareil va s'arrêter.</span><span class="sxs-lookup"><span data-stu-id="40a5d-171">The device will now shut down.</span></span> <span data-ttu-id="40a5d-172">Si vous souhaitez démarrer votre appareil, vous devrez le faire par le biais du Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="40a5d-172">If you want to start your device, you will need to do that through the Hyper-V Manager.</span></span>

#### <a name="to-restart-your-virtual-device"></a><span data-ttu-id="40a5d-173">Pour redémarrer votre appareil virtuel</span><span class="sxs-lookup"><span data-stu-id="40a5d-173">To restart your virtual device</span></span>
1. <span data-ttu-id="40a5d-174">Dans l’interface utilisateur web locale, accédez à **Maintenance** > **Paramètres d'alimentation**.</span><span class="sxs-lookup"><span data-stu-id="40a5d-174">In the local web UI, go to **Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="40a5d-175">En bas de la page, cliquez sur **Redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="40a5d-175">At the bottom of the page, click **Restart**.</span></span>
   
    ![redémarrer l'appareil](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="40a5d-177">Un avertissement s'affiche indiquant qu'un redémarrage de l'appareil va interrompre toutes les E/S qui étaient en cours, ce qui entraîne une interruption du service.</span><span class="sxs-lookup"><span data-stu-id="40a5d-177">A warning will appear stating that restarting the device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="40a5d-178">Cliquez sur l’icône en forme de coche </span><span class="sxs-lookup"><span data-stu-id="40a5d-178">Click the check icon</span></span> ![icône en forme de coche](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="40a5d-180">.</span><span class="sxs-lookup"><span data-stu-id="40a5d-180">.</span></span>
   
    ![avertissement de redémarrage](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="40a5d-182">Vous serez averti que le redémarrage a été initié.</span><span class="sxs-lookup"><span data-stu-id="40a5d-182">You will be notified that the restart has been initiated.</span></span>
   
    ![redémarrage initié](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="40a5d-184">Lorsque le redémarrage est en cours, la connexion à l'interface utilisateur s'interrompt.</span><span class="sxs-lookup"><span data-stu-id="40a5d-184">While the restart is in progress, you will lose the connection to the UI.</span></span> <span data-ttu-id="40a5d-185">Vous pouvez surveiller le redémarrage en actualisant périodiquement l'interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="40a5d-185">You can monitor the restart by refreshing the UI periodically.</span></span> <span data-ttu-id="40a5d-186">Vous pouvez également surveiller l'état du redémarrage de l'appareil avec le Gestionnaire Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="40a5d-186">Alternatively, you can monitor the device restart status through the Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40a5d-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="40a5d-187">Next steps</span></span>
<span data-ttu-id="40a5d-188">Découvrez comment [utiliser le service StorSimple Manager pour gérer votre appareil](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="40a5d-188">Learn how to [use the StorSimple Manager service to manage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

