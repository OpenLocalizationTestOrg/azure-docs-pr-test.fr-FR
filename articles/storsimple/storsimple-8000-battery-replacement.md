---
title: "Remplacer la batterie d’un appareil de la gamme Microsoft Azure StorSimple 8000 | Microsoft Docs"
description: "Décrit comment retirer, remplacer et entretenir le module de batterie de secours sur votre appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 174a3163082594ea6a49b7f5a78857848f8f0566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="17756-103">Remplacer le module de batterie de secours sur votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="17756-103">Replace the backup battery module on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="17756-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="17756-104">Overview</span></span>
<span data-ttu-id="17756-105">Le module d’alimentation et de refroidissement (PCM) du boîtier principal de votre appareil Microsoft Azure StorSimple dispose d’une batterie supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="17756-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="17756-106">Celle-ci fournit l’alimentation pour que l’appareil StorSimple puisse enregistrer des données en cas de perte d’alimentation au niveau du boîtier principal.</span><span class="sxs-lookup"><span data-stu-id="17756-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span></span> <span data-ttu-id="17756-107">Cette batterie est appelée *module de batterie de secours*.</span><span class="sxs-lookup"><span data-stu-id="17756-107">This battery pack is referred to as the *backup battery module*.</span></span> <span data-ttu-id="17756-108">Le module de batterie de secours existe uniquement pour le boîtier principal de votre appareil StorSimple (le boîtier EBOD ne contient pas de module de batterie de secours).</span><span class="sxs-lookup"><span data-stu-id="17756-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span></span>

<span data-ttu-id="17756-109">Ce didacticiel explique comment :</span><span class="sxs-lookup"><span data-stu-id="17756-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="17756-110">Retirer le module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="17756-110">Remove the backup battery module</span></span>
* <span data-ttu-id="17756-111">Installer un nouveau module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="17756-111">Install a new backup battery module</span></span>
* <span data-ttu-id="17756-112">Entretenir le module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="17756-112">Maintain the backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17756-113">Avant le retrait et le remplacement d’un module de batterie de secours, passez en revue les informations de sécurité dans l’ [Introduction au remplacement des composants matériels StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="17756-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-the-backup-battery-module"></a><span data-ttu-id="17756-114">Retirer le module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="17756-114">Remove the backup battery module</span></span>
<span data-ttu-id="17756-115">Le module de batterie de secours pour votre appareil StorSimple est une unité remplaçable sur site.</span><span class="sxs-lookup"><span data-stu-id="17756-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="17756-116">Avant son installation dans le module PCM, le module de batterie doit être conservé dans son emballage d’origine.</span><span class="sxs-lookup"><span data-stu-id="17756-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span></span> <span data-ttu-id="17756-117">Procédez comme suit pour supprimer la batterie de secours.</span><span class="sxs-lookup"><span data-stu-id="17756-117">Perform the following steps to remove the backup battery.</span></span>

#### <a name="to-remove-the-backup-battery-module"></a><span data-ttu-id="17756-118">Pour retirer le module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="17756-118">To remove the backup battery module</span></span>
1. <span data-ttu-id="17756-119">Dans le portail Azure, accédez à votre panneau de service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="17756-119">In the Azure portal, go to your StorSimple Device Manager service blade.</span></span> <span data-ttu-id="17756-120">Accédez à **Appareils**, puis sélectionnez votre appareil dans la listes des appareils.</span><span class="sxs-lookup"><span data-stu-id="17756-120">Go to **Devices** and then select your device from the list of devices.</span></span> <span data-ttu-id="17756-121">Accédez à **Surveiller** > **Intégrité matérielle**.</span><span class="sxs-lookup"><span data-stu-id="17756-121">Navigate to **Monitor** > **Hardware health**.</span></span> <span data-ttu-id="17756-122">Sous **Composants partagés**, regardez l’état de la batterie.</span><span class="sxs-lookup"><span data-stu-id="17756-122">Under **Shared Components**, look at the status of the battery.</span></span>
2. <span data-ttu-id="17756-123">Identifiez le PCM dans lequel la batterie est défectueuse.</span><span class="sxs-lookup"><span data-stu-id="17756-123">Identify the PCM in which the battery has failed.</span></span> <span data-ttu-id="17756-124">La figure 1 illustre l’arrière de l’appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="17756-124">Figure 1 shows the back of the StorSimple device.</span></span>
   
    ![Fond du panier des modules du boîtier principal de l’appareil](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="17756-126">**Figure 1** Arrière de l’appareil principal avec les modules PCM et de contrôleur</span><span class="sxs-lookup"><span data-stu-id="17756-126">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="17756-127">Étiquette</span><span class="sxs-lookup"><span data-stu-id="17756-127">Label</span></span> | <span data-ttu-id="17756-128">Description</span><span class="sxs-lookup"><span data-stu-id="17756-128">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="17756-129">1</span><span class="sxs-lookup"><span data-stu-id="17756-129">1</span></span> |<span data-ttu-id="17756-130">PCM 0</span><span class="sxs-lookup"><span data-stu-id="17756-130">PCM 0</span></span> |
   | <span data-ttu-id="17756-131">2</span><span class="sxs-lookup"><span data-stu-id="17756-131">2</span></span> |<span data-ttu-id="17756-132">PCM 1</span><span class="sxs-lookup"><span data-stu-id="17756-132">PCM 1</span></span> |
   | <span data-ttu-id="17756-133">3</span><span class="sxs-lookup"><span data-stu-id="17756-133">3</span></span> |<span data-ttu-id="17756-134">Contrôleur 0</span><span class="sxs-lookup"><span data-stu-id="17756-134">Controller 0</span></span> |
   | <span data-ttu-id="17756-135">4</span><span class="sxs-lookup"><span data-stu-id="17756-135">4</span></span> |<span data-ttu-id="17756-136">Contrôleur 1</span><span class="sxs-lookup"><span data-stu-id="17756-136">Controller 1</span></span> |
   
    <span data-ttu-id="17756-137">Comme l’illustre le numéro 3 dans la figure 2, le voyant LED de surveillance sur PCM 0 qui correspond à **Panne de batterie** doit être allumé.</span><span class="sxs-lookup"><span data-stu-id="17756-137">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span></span>
   
    ![Fond du panier du module PCM de l’appareil avec voyants LED de surveillance](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="17756-139">**Figure 2** Arrière du PCM avec les voyants LED de surveillance</span><span class="sxs-lookup"><span data-stu-id="17756-139">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="17756-140">Étiquette</span><span class="sxs-lookup"><span data-stu-id="17756-140">Label</span></span> | <span data-ttu-id="17756-141">Description</span><span class="sxs-lookup"><span data-stu-id="17756-141">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="17756-142">1</span><span class="sxs-lookup"><span data-stu-id="17756-142">1</span></span> |<span data-ttu-id="17756-143">Panne d’alimentation secteur</span><span class="sxs-lookup"><span data-stu-id="17756-143">AC power failure</span></span> |
   | <span data-ttu-id="17756-144">2</span><span class="sxs-lookup"><span data-stu-id="17756-144">2</span></span> |<span data-ttu-id="17756-145">Panne de ventilateur</span><span class="sxs-lookup"><span data-stu-id="17756-145">Fan failure</span></span> |
   | <span data-ttu-id="17756-146">3</span><span class="sxs-lookup"><span data-stu-id="17756-146">3</span></span> |<span data-ttu-id="17756-147">Panne de batterie</span><span class="sxs-lookup"><span data-stu-id="17756-147">Battery fault</span></span> |
   | <span data-ttu-id="17756-148">4</span><span class="sxs-lookup"><span data-stu-id="17756-148">4</span></span> |<span data-ttu-id="17756-149">PCM OK</span><span class="sxs-lookup"><span data-stu-id="17756-149">PCM OK</span></span> |
   | <span data-ttu-id="17756-150">5</span><span class="sxs-lookup"><span data-stu-id="17756-150">5</span></span> |<span data-ttu-id="17756-151">Panne d’alimentation secteur</span><span class="sxs-lookup"><span data-stu-id="17756-151">DC power failure</span></span> |
   | <span data-ttu-id="17756-152">6</span><span class="sxs-lookup"><span data-stu-id="17756-152">6</span></span> |<span data-ttu-id="17756-153">Batterie saine</span><span class="sxs-lookup"><span data-stu-id="17756-153">Battery healthy</span></span> |
3. <span data-ttu-id="17756-154">Pour retirer le PCM dont la batterie est défectueuse, suivez les étapes de la procédure [Retrait d’un PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="17756-154">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="17756-155">Une fois le PCM retiré, soulevez la poignée du module de batterie et faites-la pivoter vers le haut, comme l’illustre la figure ci-après, puis tirez dessus pour extraire la batterie.</span><span class="sxs-lookup"><span data-stu-id="17756-155">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span></span>
   
    ![Retrait de la batterie du module PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="17756-157">**Figure 3** Retrait de la batterie du PCM</span><span class="sxs-lookup"><span data-stu-id="17756-157">**Figure 3** Removing the battery from the PCM</span></span>
5. <span data-ttu-id="17756-158">Placez le module dans l’emballage de l’unité remplaçable sur site.</span><span class="sxs-lookup"><span data-stu-id="17756-158">Place the module in the field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="17756-159">Renvoyez l’unité défectueuse à Microsoft qui en assurera l’entretien et la manutention.</span><span class="sxs-lookup"><span data-stu-id="17756-159">Return the defective unit to Microsoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="17756-160">Installer un nouveau module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="17756-160">Install a new backup battery module</span></span>
<span data-ttu-id="17756-161">Procédez comme suit pour installer le module de batterie de remplacement dans le PCM du boîtier principal de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="17756-161">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span></span>

#### <a name="to-install-the-battery-module"></a><span data-ttu-id="17756-162">Pour installer le module de batterie</span><span class="sxs-lookup"><span data-stu-id="17756-162">To install the battery module</span></span>
1. <span data-ttu-id="17756-163">Orientez correctement le module de batterie de secours dans le PCM.</span><span class="sxs-lookup"><span data-stu-id="17756-163">Place the backup battery module in the proper orientation in the PCM.</span></span>
2. <span data-ttu-id="17756-164">Appuyez sur la poignée du module de batterie jusqu’en bas pour placer le connecteur.</span><span class="sxs-lookup"><span data-stu-id="17756-164">Press down the battery module handle all the way to seat the connector.</span></span>
3. <span data-ttu-id="17756-165">Remplacez le PCM dans le boîtier principal en procédant de la manière décrite dans [Remplacement d’un module d’alimentation et de refroidissement (PCM) sur votre appareil StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="17756-165">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="17756-166">Une fois le remplacement terminé, accédez à voter appareil, puis accédez à **Surveiller** > **Intégrité matérielle** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="17756-166">After the replacement is complete, go to your device and then go to **Monitor** > **Hardware health** in the Azure portal.</span></span> <span data-ttu-id="17756-167">Vérifiez l'état de la batterie pour vous assurer que l'installation a réussi.</span><span class="sxs-lookup"><span data-stu-id="17756-167">Verify the status of the battery to make sure that the installation was successful.</span></span> <span data-ttu-id="17756-168">Un état vert indique que la batterie est saine.</span><span class="sxs-lookup"><span data-stu-id="17756-168">A green status indicates that the battery is healthy.</span></span>

## <a name="maintain-the-backup-battery-module"></a><span data-ttu-id="17756-169">Entretenir le module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="17756-169">Maintain the backup battery module</span></span>
<span data-ttu-id="17756-170">Dans votre appareil StorSimple, le module de batterie de secours de votre appareil alimente le contrôleur en cas de panne de courant.</span><span class="sxs-lookup"><span data-stu-id="17756-170">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span></span> <span data-ttu-id="17756-171">Il permet à l’appareil StorSimple d’enregistrer des données critiques avant de s’arrêter de façon contrôlée.</span><span class="sxs-lookup"><span data-stu-id="17756-171">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span></span> <span data-ttu-id="17756-172">Ce système, équipé de deux batteries entièrement chargées dans les PCM, peut faire face à deux pannes de courant consécutives.</span><span class="sxs-lookup"><span data-stu-id="17756-172">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span></span>

<span data-ttu-id="17756-173">Dans le portail Azure, **Intégrité matérielle** sous le panneau **Surveiller** indique si la batterie ne fonctionne pas correctement ou si elle approche de la fin de sa durée de vie.</span><span class="sxs-lookup"><span data-stu-id="17756-173">In the Azure portal, the **Hardware health** under the **Monitor** blade indicates whether the battery is malfunctioning or the end-of-life is approaching.</span></span> <span data-ttu-id="17756-174">L’état de la batterie est indiqué par **Batterie dans PCM 0** ou **Batterie dans PCM 1** sous **Composants partagés**.</span><span class="sxs-lookup"><span data-stu-id="17756-174">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="17756-175">Ce panneau indiquera l’état **DÉTÉRIORÉ** si la fin de durée de vie approche et l’état **ÉCHEC** si elle est atteinte.</span><span class="sxs-lookup"><span data-stu-id="17756-175">This blade will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span>

> [!NOTE]
> <span data-ttu-id="17756-176">La batterie peut signaler **ÉCHEC** quand elle a juste besoin d’être chargée.</span><span class="sxs-lookup"><span data-stu-id="17756-176">The battery can report **FAILED** when it simply needs to be charged.</span></span>


<span data-ttu-id="17756-177">Si l’état **DÉTÉRIORÉ** s’affiche, nous vous recommandons de procéder ainsi :</span><span class="sxs-lookup"><span data-stu-id="17756-177">If the **DEGRADED** state appears, we recommend the following course of action:</span></span>

* <span data-ttu-id="17756-178">Le système a peut-être récemment subi une panne ou des opérations de maintenance peuvent être en cours sur les batteries.</span><span class="sxs-lookup"><span data-stu-id="17756-178">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="17756-179">Observez le système pendant 12 heures avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="17756-179">Observe the system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="17756-180">Si l’état est toujours **DÉTÉRIORÉ** après 12 heures de branchement sur secteur alors que les contrôleurs et les PCM sont en cours d’exécution, vous devez changer la batterie.</span><span class="sxs-lookup"><span data-stu-id="17756-180">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span></span> <span data-ttu-id="17756-181">Veuillez [contacter le support Microsoft](storsimple-8000-contact-microsoft-support.md) pour obtenir un module de batterie de secours de remplacement.</span><span class="sxs-lookup"><span data-stu-id="17756-181">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="17756-182">Si l’état redevient opérationnel après 12 heures, cela veut dire que la batterie fonctionne et qu’elle avait juste besoin d’être chargée dans le cadre de la maintenance.</span><span class="sxs-lookup"><span data-stu-id="17756-182">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="17756-183">Si aucune panne n’est survenue et que le PCM est activé et branché sur secteur, la batterie doit être remplacée.</span><span class="sxs-lookup"><span data-stu-id="17756-183">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span></span> <span data-ttu-id="17756-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) pour commander un module de batterie de secours de remplacement.</span><span class="sxs-lookup"><span data-stu-id="17756-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) to order a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17756-185">Jetez la batterie en panne en respectant les réglementations nationales et locales applicables.</span><span class="sxs-lookup"><span data-stu-id="17756-185">Dispose of the failed battery according to national and regional regulations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17756-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="17756-186">Next steps</span></span>
<span data-ttu-id="17756-187">En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="17756-187">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

