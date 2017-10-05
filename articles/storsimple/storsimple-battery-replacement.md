---
title: "Remplacer la batterie d’un appareil Microsoft Azure StorSimple | Microsoft Docs"
description: "Décrit comment retirer, remplacer et entretenir le module de batterie de secours sur votre appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8b89b3f6851ec9ee0570f551b5407419fdba2d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="5c332-103">Remplacer le module de batterie de secours sur votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="5c332-103">Replace the backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="5c332-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5c332-104">Overview</span></span>
<span data-ttu-id="5c332-105">Le module d’alimentation et de refroidissement (PCM) du boîtier principal de votre appareil Microsoft Azure StorSimple dispose d’une batterie supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="5c332-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="5c332-106">Celle-ci fournit l’alimentation pour que l’appareil StorSimple puisse enregistrer des données en cas de perte d’alimentation au niveau du boîtier principal.</span><span class="sxs-lookup"><span data-stu-id="5c332-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span></span> <span data-ttu-id="5c332-107">Cette batterie est appelée *module de batterie de secours*.</span><span class="sxs-lookup"><span data-stu-id="5c332-107">This battery pack is referred to as the *backup battery module*.</span></span> <span data-ttu-id="5c332-108">Le module de batterie de secours existe uniquement pour le boîtier principal de votre appareil StorSimple (le boîtier EBOD ne contient pas de module de batterie de secours).</span><span class="sxs-lookup"><span data-stu-id="5c332-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="5c332-109">Ce didacticiel explique comment :</span><span class="sxs-lookup"><span data-stu-id="5c332-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="5c332-110">Retirer le module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="5c332-110">Remove the backup battery module</span></span> 
* <span data-ttu-id="5c332-111">Installer un nouveau module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="5c332-111">Install a new backup battery module</span></span>
* <span data-ttu-id="5c332-112">Entretenir le module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="5c332-112">Maintain the backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c332-113">Avant le retrait et le remplacement d’un module de batterie de secours, passez en revue les informations de sécurité dans l’ [Introduction au remplacement des composants matériels StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="5c332-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-the-backup-battery-module"></a><span data-ttu-id="5c332-114">Retirer le module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="5c332-114">Remove the backup battery module</span></span>
<span data-ttu-id="5c332-115">Le module de batterie de secours pour votre appareil StorSimple est une unité remplaçable sur site.</span><span class="sxs-lookup"><span data-stu-id="5c332-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="5c332-116">Avant son installation dans le module PCM, le module de batterie doit être conservé dans son emballage d’origine.</span><span class="sxs-lookup"><span data-stu-id="5c332-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span></span> <span data-ttu-id="5c332-117">Procédez comme suit pour supprimer la batterie de secours.</span><span class="sxs-lookup"><span data-stu-id="5c332-117">Perform the following steps to remove the backup battery.</span></span>

#### <a name="to-remove-the-backup-battery-module"></a><span data-ttu-id="5c332-118">Pour retirer le module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="5c332-118">To remove the backup battery module</span></span>
1. <span data-ttu-id="5c332-119">Dans le portail Azure Classic, accédez à **Appareils** > **Maintenance** > **État du matériel**.</span><span class="sxs-lookup"><span data-stu-id="5c332-119">In the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="5c332-120">Sous **Composants partagés**, regardez l’état de la batterie.</span><span class="sxs-lookup"><span data-stu-id="5c332-120">Under **Shared Components**, look at the status of the battery.</span></span>
2. <span data-ttu-id="5c332-121">Identifiez le PCM dans lequel la batterie est défectueuse.</span><span class="sxs-lookup"><span data-stu-id="5c332-121">Identify the PCM in which the battery has failed.</span></span> <span data-ttu-id="5c332-122">La figure 1 illustre l’arrière de l’appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5c332-122">Figure 1 shows the back of the StorSimple device.</span></span>
   
    ![Fond du panier des modules du boîtier principal de l’appareil](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="5c332-124">**Figure 1** Arrière de l’appareil principal avec les modules PCM et de contrôleur</span><span class="sxs-lookup"><span data-stu-id="5c332-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="5c332-125">Étiquette</span><span class="sxs-lookup"><span data-stu-id="5c332-125">Label</span></span> | <span data-ttu-id="5c332-126">Description</span><span class="sxs-lookup"><span data-stu-id="5c332-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="5c332-127">1</span><span class="sxs-lookup"><span data-stu-id="5c332-127">1</span></span> |<span data-ttu-id="5c332-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="5c332-128">PCM 0</span></span> |
   | <span data-ttu-id="5c332-129">2</span><span class="sxs-lookup"><span data-stu-id="5c332-129">2</span></span> |<span data-ttu-id="5c332-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="5c332-130">PCM 1</span></span> |
   | <span data-ttu-id="5c332-131">3</span><span class="sxs-lookup"><span data-stu-id="5c332-131">3</span></span> |<span data-ttu-id="5c332-132">Contrôleur 0</span><span class="sxs-lookup"><span data-stu-id="5c332-132">Controller 0</span></span> |
   | <span data-ttu-id="5c332-133">4</span><span class="sxs-lookup"><span data-stu-id="5c332-133">4</span></span> |<span data-ttu-id="5c332-134">Contrôleur 1</span><span class="sxs-lookup"><span data-stu-id="5c332-134">Controller 1</span></span> |
   
    <span data-ttu-id="5c332-135">Comme l’illustre le numéro 3 dans la figure 2, le voyant LED de surveillance sur PCM 0 qui correspond à **Panne de batterie** doit être allumé.</span><span class="sxs-lookup"><span data-stu-id="5c332-135">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span></span>
   
    ![Fond du panier du module PCM de l’appareil avec voyants LED de surveillance](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="5c332-137">**Figure 2** Arrière du PCM avec les voyants LED de surveillance</span><span class="sxs-lookup"><span data-stu-id="5c332-137">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="5c332-138">Étiquette</span><span class="sxs-lookup"><span data-stu-id="5c332-138">Label</span></span> | <span data-ttu-id="5c332-139">Description</span><span class="sxs-lookup"><span data-stu-id="5c332-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="5c332-140">1</span><span class="sxs-lookup"><span data-stu-id="5c332-140">1</span></span> |<span data-ttu-id="5c332-141">Panne d’alimentation secteur</span><span class="sxs-lookup"><span data-stu-id="5c332-141">AC power failure</span></span> |
   | <span data-ttu-id="5c332-142">2</span><span class="sxs-lookup"><span data-stu-id="5c332-142">2</span></span> |<span data-ttu-id="5c332-143">Panne de ventilateur</span><span class="sxs-lookup"><span data-stu-id="5c332-143">Fan failure</span></span> |
   | <span data-ttu-id="5c332-144">3</span><span class="sxs-lookup"><span data-stu-id="5c332-144">3</span></span> |<span data-ttu-id="5c332-145">Panne de batterie</span><span class="sxs-lookup"><span data-stu-id="5c332-145">Battery fault</span></span> |
   | <span data-ttu-id="5c332-146">4</span><span class="sxs-lookup"><span data-stu-id="5c332-146">4</span></span> |<span data-ttu-id="5c332-147">PCM OK</span><span class="sxs-lookup"><span data-stu-id="5c332-147">PCM OK</span></span> |
   | <span data-ttu-id="5c332-148">5</span><span class="sxs-lookup"><span data-stu-id="5c332-148">5</span></span> |<span data-ttu-id="5c332-149">Panne d’alimentation secteur</span><span class="sxs-lookup"><span data-stu-id="5c332-149">DC power failure</span></span> |
   | <span data-ttu-id="5c332-150">6</span><span class="sxs-lookup"><span data-stu-id="5c332-150">6</span></span> |<span data-ttu-id="5c332-151">Batterie saine</span><span class="sxs-lookup"><span data-stu-id="5c332-151">Battery healthy</span></span> |
3. <span data-ttu-id="5c332-152">Pour retirer le PCM dont la batterie est défectueuse, suivez les étapes de la procédure [Retrait d’un PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="5c332-152">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="5c332-153">Une fois le PCM retiré, soulevez la poignée du module de batterie et faites-la pivoter vers le haut, comme l’illustre la figure ci-après, puis tirez dessus pour extraire la batterie.</span><span class="sxs-lookup"><span data-stu-id="5c332-153">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span></span>
   
    ![Retrait de la batterie du module PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="5c332-155">**Figure 3** Retrait de la batterie du PCM</span><span class="sxs-lookup"><span data-stu-id="5c332-155">**Figure 3** Removing the battery from the PCM</span></span>
5. <span data-ttu-id="5c332-156">Placez le module dans l’emballage de l’unité remplaçable sur site.</span><span class="sxs-lookup"><span data-stu-id="5c332-156">Place the module in the field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="5c332-157">Renvoyez l’unité défectueuse à Microsoft qui en assurera l’entretien et la manutention.</span><span class="sxs-lookup"><span data-stu-id="5c332-157">Return the defective unit to Microsoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="5c332-158">Installer un nouveau module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="5c332-158">Install a new backup battery module</span></span>
<span data-ttu-id="5c332-159">Procédez comme suit pour installer le module de batterie de remplacement dans le PCM du boîtier principal de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5c332-159">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span></span>

#### <a name="to-install-the-battery-module"></a><span data-ttu-id="5c332-160">Pour installer le module de batterie</span><span class="sxs-lookup"><span data-stu-id="5c332-160">To install the battery module</span></span>
1. <span data-ttu-id="5c332-161">Orientez correctement le module de batterie de secours dans le PCM.</span><span class="sxs-lookup"><span data-stu-id="5c332-161">Place the backup battery module in the proper orientation in the PCM.</span></span>
2. <span data-ttu-id="5c332-162">Appuyez sur la poignée du module de batterie jusqu’en bas pour placer le connecteur.</span><span class="sxs-lookup"><span data-stu-id="5c332-162">Press down the battery module handle all the way to seat the connector.</span></span>
3. <span data-ttu-id="5c332-163">Remplacez le PCM dans le boîtier principal en procédant de la manière décrite dans [Remplacement d’un module d’alimentation et de refroidissement (PCM) sur votre appareil StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="5c332-163">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="5c332-164">Une fois le remplacement terminé, accédez à **Appareils** > **Maintenance** > **État du matériel** dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="5c332-164">After the replacement is complete, go to **Devices** > **Maintenance** > **Hardware Status** in the Azure classic portal.</span></span> <span data-ttu-id="5c332-165">Vérifiez l'état de la batterie pour vous assurer que l'installation a réussi.</span><span class="sxs-lookup"><span data-stu-id="5c332-165">Verify the status of the battery to make sure that the installation was successful.</span></span> <span data-ttu-id="5c332-166">Un état vert indique que la batterie est saine.</span><span class="sxs-lookup"><span data-stu-id="5c332-166">A green status indicates that the battery is healthy.</span></span>

## <a name="maintain-the-backup-battery-module"></a><span data-ttu-id="5c332-167">Entretenir le module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="5c332-167">Maintain the backup battery module</span></span>
<span data-ttu-id="5c332-168">Dans votre appareil StorSimple, le module de batterie de secours de votre appareil alimente le contrôleur en cas de panne de courant.</span><span class="sxs-lookup"><span data-stu-id="5c332-168">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span></span> <span data-ttu-id="5c332-169">Il permet à l’appareil StorSimple d’enregistrer des données critiques avant de s’arrêter de façon contrôlée.</span><span class="sxs-lookup"><span data-stu-id="5c332-169">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span></span> <span data-ttu-id="5c332-170">Ce système, équipé de deux batteries entièrement chargées dans les PCM, peut faire face à deux pannes de courant consécutives.</span><span class="sxs-lookup"><span data-stu-id="5c332-170">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span></span>

<span data-ttu-id="5c332-171">Dans le portail Azure Classic, l’option **État du matériel** dans la page **Maintenance** indique si la batterie ne fonctionne pas correctement ou si elle approche de la fin de sa durée de vie.</span><span class="sxs-lookup"><span data-stu-id="5c332-171">In the Azure classic portal, the **Hardware Status** on the **Maintenance** page indicates whether the battery is malfunctioning or the end-of-life is approaching.</span></span> <span data-ttu-id="5c332-172">L’état de la batterie est indiqué par **Batterie dans PCM 0** ou **Batterie dans PCM 1** sous **Composants partagés**.</span><span class="sxs-lookup"><span data-stu-id="5c332-172">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="5c332-173">Cette page indique l’état **DÉTÉRIORÉ** si la fin de durée de vie approche et l’état **ÉCHEC** si elle est atteinte.</span><span class="sxs-lookup"><span data-stu-id="5c332-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="5c332-174">La batterie peut signaler **ÉCHEC** quand elle a juste besoin d’être chargée.</span><span class="sxs-lookup"><span data-stu-id="5c332-174">The battery can report **FAILED** when it simply needs to be charged.</span></span>
> 
> 

<span data-ttu-id="5c332-175">Si l’état **DÉTÉRIORÉ** s’affiche, nous vous recommandons de procéder ainsi :</span><span class="sxs-lookup"><span data-stu-id="5c332-175">If the **DEGRADED** state appears, we recommend the following course of action:</span></span>

* <span data-ttu-id="5c332-176">Le système a peut-être récemment subi une panne ou des opérations de maintenance peuvent être en cours sur les batteries.</span><span class="sxs-lookup"><span data-stu-id="5c332-176">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="5c332-177">Observez le système pendant 12 heures avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="5c332-177">Observe the system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="5c332-178">Si l’état est toujours **DÉTÉRIORÉ** après 12 heures de branchement sur secteur alors que les contrôleurs et les PCM sont en cours d’exécution, vous devez changer la batterie.</span><span class="sxs-lookup"><span data-stu-id="5c332-178">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span></span> <span data-ttu-id="5c332-179">Veuillez [contacter le support Microsoft](storsimple-contact-microsoft-support.md) pour obtenir un module de batterie de secours de remplacement.</span><span class="sxs-lookup"><span data-stu-id="5c332-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="5c332-180">Si l’état redevient opérationnel après 12 heures, cela veut dire que la batterie fonctionne et qu’elle avait juste besoin d’être chargée dans le cadre de la maintenance.</span><span class="sxs-lookup"><span data-stu-id="5c332-180">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="5c332-181">Si aucune panne n’est survenue et que le PCM est activé et branché sur secteur, la batterie doit être remplacée.</span><span class="sxs-lookup"><span data-stu-id="5c332-181">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span></span> <span data-ttu-id="5c332-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) pour commander un module de batterie de secours de remplacement.</span><span class="sxs-lookup"><span data-stu-id="5c332-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) to order a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c332-183">Jetez la batterie en panne en respectant les réglementations nationales et locales applicables.</span><span class="sxs-lookup"><span data-stu-id="5c332-183">Dispose of the failed battery according to national and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5c332-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5c332-184">Next steps</span></span>
<span data-ttu-id="5c332-185">En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="5c332-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

