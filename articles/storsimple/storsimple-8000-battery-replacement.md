---
title: "batterie aaaReplace sur l’appareil de série Microsoft Azure StorSimple 8000 | Documents Microsoft"
description: "Décrit comment remplacer les tooremove et mettre à jour le module de batterie de secours hello sur votre appareil StorSimple."
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
ms.openlocfilehash: 5ac767807e6c3fd817d8d522629db2aceaac9bdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="52241-103">Remplacez le module de batterie de secours hello sur votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="52241-103">Replace hello backup battery module on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="52241-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="52241-104">Overview</span></span>
<span data-ttu-id="52241-105">boîtier principal de Hello d’alimentation et de Module de refroidissement (PCM) sur votre appareil Microsoft Azure StorSimple a un pack batterie supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="52241-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="52241-106">Ce pack fournit power afin que hello appareil StorSimple peut enregistrer les données si la perte de boîtier principal du toohello d’alimentation secteur.</span><span class="sxs-lookup"><span data-stu-id="52241-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="52241-107">Ce pack batterie est référencé tooas hello *module de batterie de secours*.</span><span class="sxs-lookup"><span data-stu-id="52241-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="52241-108">module de batterie de secours Hello existe uniquement pour le boîtier principal de hello dans votre appareil StorSimple (hello boîtiers ne contient pas un module de batterie de secours).</span><span class="sxs-lookup"><span data-stu-id="52241-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span>

<span data-ttu-id="52241-109">Ce didacticiel explique comment :</span><span class="sxs-lookup"><span data-stu-id="52241-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="52241-110">Supprimer le module de batterie de secours hello</span><span class="sxs-lookup"><span data-stu-id="52241-110">Remove hello backup battery module</span></span>
* <span data-ttu-id="52241-111">Installer un nouveau module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="52241-111">Install a new backup battery module</span></span>
* <span data-ttu-id="52241-112">Mettre à jour le module de batterie de secours hello</span><span class="sxs-lookup"><span data-stu-id="52241-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52241-113">Avant la suppression et le remplacement d’un module de batterie de secours, passez en revue les informations de sécurité hello Bonjour [remplacement de composant matériel Introduction tooStorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="52241-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="52241-114">Supprimer le module de batterie de secours hello</span><span class="sxs-lookup"><span data-stu-id="52241-114">Remove hello backup battery module</span></span>
<span data-ttu-id="52241-115">module de batterie de secours Hello pour votre appareil StorSimple est une unité remplaçable.</span><span class="sxs-lookup"><span data-stu-id="52241-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="52241-116">Avant son installation Bonjour PCM, module de batterie hello doit être stockée dans son emballage d’origine.</span><span class="sxs-lookup"><span data-stu-id="52241-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="52241-117">Effectuer hello suivant la batterie de secours étapes tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="52241-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="52241-118">module de batterie de secours hello tooremove</span><span class="sxs-lookup"><span data-stu-id="52241-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="52241-119">Bonjour portail Azure, accédez à panneau de service de gestionnaire de périphériques StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="52241-119">In hello Azure portal, go tooyour StorSimple Device Manager service blade.</span></span> <span data-ttu-id="52241-120">Accédez trop**périphériques** , puis sélectionnez votre appareil dans la liste des appareils hello.</span><span class="sxs-lookup"><span data-stu-id="52241-120">Go too**Devices** and then select your device from hello list of devices.</span></span> <span data-ttu-id="52241-121">Accédez trop**moniteur** > **l’intégrité du matériel**.</span><span class="sxs-lookup"><span data-stu-id="52241-121">Navigate too**Monitor** > **Hardware health**.</span></span> <span data-ttu-id="52241-122">Sous **composants partagés**, regardez statut hello de batterie de hello.</span><span class="sxs-lookup"><span data-stu-id="52241-122">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="52241-123">Identifier le PCM hello dans le hello batterie a échoué.</span><span class="sxs-lookup"><span data-stu-id="52241-123">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="52241-124">La figure 1 montre hello arrière de l’appareil StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="52241-124">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![Fond du panier des modules du boîtier principal de l’appareil](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="52241-126">**Figure 1** Arrière de l’appareil principal avec les modules PCM et de contrôleur</span><span class="sxs-lookup"><span data-stu-id="52241-126">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="52241-127">Étiquette</span><span class="sxs-lookup"><span data-stu-id="52241-127">Label</span></span> | <span data-ttu-id="52241-128">Description</span><span class="sxs-lookup"><span data-stu-id="52241-128">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="52241-129">1</span><span class="sxs-lookup"><span data-stu-id="52241-129">1</span></span> |<span data-ttu-id="52241-130">PCM 0</span><span class="sxs-lookup"><span data-stu-id="52241-130">PCM 0</span></span> |
   | <span data-ttu-id="52241-131">2</span><span class="sxs-lookup"><span data-stu-id="52241-131">2</span></span> |<span data-ttu-id="52241-132">PCM 1</span><span class="sxs-lookup"><span data-stu-id="52241-132">PCM 1</span></span> |
   | <span data-ttu-id="52241-133">3</span><span class="sxs-lookup"><span data-stu-id="52241-133">3</span></span> |<span data-ttu-id="52241-134">Contrôleur 0</span><span class="sxs-lookup"><span data-stu-id="52241-134">Controller 0</span></span> |
   | <span data-ttu-id="52241-135">4</span><span class="sxs-lookup"><span data-stu-id="52241-135">4</span></span> |<span data-ttu-id="52241-136">Contrôleur 1</span><span class="sxs-lookup"><span data-stu-id="52241-136">Controller 1</span></span> |
   
    <span data-ttu-id="52241-137">Comme indiqué par le numéro 3 Bonjour Figure 2, hello analyse indicateur LED sur PCM 0 qui correspond trop**panne** doit être allumée.</span><span class="sxs-lookup"><span data-stu-id="52241-137">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![Fond du panier du module PCM de l’appareil avec voyants LED de surveillance](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="52241-139">**Figure 2** hello d’affichage arrière du PCM des témoins DEL</span><span class="sxs-lookup"><span data-stu-id="52241-139">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="52241-140">Étiquette</span><span class="sxs-lookup"><span data-stu-id="52241-140">Label</span></span> | <span data-ttu-id="52241-141">Description</span><span class="sxs-lookup"><span data-stu-id="52241-141">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="52241-142">1</span><span class="sxs-lookup"><span data-stu-id="52241-142">1</span></span> |<span data-ttu-id="52241-143">Panne d’alimentation secteur</span><span class="sxs-lookup"><span data-stu-id="52241-143">AC power failure</span></span> |
   | <span data-ttu-id="52241-144">2</span><span class="sxs-lookup"><span data-stu-id="52241-144">2</span></span> |<span data-ttu-id="52241-145">Panne de ventilateur</span><span class="sxs-lookup"><span data-stu-id="52241-145">Fan failure</span></span> |
   | <span data-ttu-id="52241-146">3</span><span class="sxs-lookup"><span data-stu-id="52241-146">3</span></span> |<span data-ttu-id="52241-147">Panne de batterie</span><span class="sxs-lookup"><span data-stu-id="52241-147">Battery fault</span></span> |
   | <span data-ttu-id="52241-148">4</span><span class="sxs-lookup"><span data-stu-id="52241-148">4</span></span> |<span data-ttu-id="52241-149">PCM OK</span><span class="sxs-lookup"><span data-stu-id="52241-149">PCM OK</span></span> |
   | <span data-ttu-id="52241-150">5</span><span class="sxs-lookup"><span data-stu-id="52241-150">5</span></span> |<span data-ttu-id="52241-151">Panne d’alimentation secteur</span><span class="sxs-lookup"><span data-stu-id="52241-151">DC power failure</span></span> |
   | <span data-ttu-id="52241-152">6</span><span class="sxs-lookup"><span data-stu-id="52241-152">6</span></span> |<span data-ttu-id="52241-153">Batterie saine</span><span class="sxs-lookup"><span data-stu-id="52241-153">Battery healthy</span></span> |
3. <span data-ttu-id="52241-154">tooremove hello PCM avec la batterie est défectueuse, suivez les étapes de hello dans [retirer un PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="52241-154">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="52241-155">Hello PCM supprimé, courbes d’élévation et une batterie de rotation hello module gérer vers le haut, comme indiqué dans la figure suivante de hello et tirez dessus pour les batteries de hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="52241-155">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![Retrait de la batterie du module PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="52241-157">**Figure 3** supprime les batterie hello hello PCM</span><span class="sxs-lookup"><span data-stu-id="52241-157">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="52241-158">Placez le module de hello dans hello remplaçable emballage de l’unité.</span><span class="sxs-lookup"><span data-stu-id="52241-158">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="52241-159">Retourner tooMicrosoft d’unité défectueuse hello de maintenance et de gestion appropriée.</span><span class="sxs-lookup"><span data-stu-id="52241-159">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="52241-160">Installer un nouveau module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="52241-160">Install a new backup battery module</span></span>
<span data-ttu-id="52241-161">Effectuer hello suivant du module de batterie de rechange étapes tooinstall hello Bonjour PCM dans le boîtier principal de hello de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="52241-161">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="52241-162">module de batterie hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="52241-162">tooinstall hello battery module</span></span>
1. <span data-ttu-id="52241-163">Placez le module de batterie de secours hello dans l’orientation appropriée de hello Bonjour PCM.</span><span class="sxs-lookup"><span data-stu-id="52241-163">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="52241-164">Module de batterie hello appuyez gérer connecteur hello de tous les hello moyen tooseat.</span><span class="sxs-lookup"><span data-stu-id="52241-164">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="52241-165">Remplacez hello PCM dans le boîtier principal de hello en suivant les instructions de hello dans [remplacer un Module de refroidissement et de puissance de votre appareil StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="52241-165">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="52241-166">Une fois terminée, remplacement de hello tooyour appareil et puis trop**moniteur** > **l’intégrité du matériel** Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="52241-166">After hello replacement is complete, go tooyour device and then go too**Monitor** > **Hardware health** in hello Azure portal.</span></span> <span data-ttu-id="52241-167">Vérifiez l’état hello de hello toomake de batterie que que hello installation a réussi.</span><span class="sxs-lookup"><span data-stu-id="52241-167">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="52241-168">Un état vert indique que la batterie de hello est sain.</span><span class="sxs-lookup"><span data-stu-id="52241-168">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="52241-169">Mettre à jour le module de batterie de secours hello</span><span class="sxs-lookup"><span data-stu-id="52241-169">Maintain hello backup battery module</span></span>
<span data-ttu-id="52241-170">Dans votre appareil StorSimple, module de batterie de secours hello fournit contrôleur toohello de l’alimentation pendant un événement de perte d’alimentation.</span><span class="sxs-lookup"><span data-stu-id="52241-170">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="52241-171">Il permet de hello StorSimple périphérique toosave données critiques de tooshutting de préalable vers le bas de manière contrôlée.</span><span class="sxs-lookup"><span data-stu-id="52241-171">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="52241-172">Avec deux batteries entièrement chargées Bonjour PCM, système de hello peut gérer deux d’affilée.</span><span class="sxs-lookup"><span data-stu-id="52241-172">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="52241-173">Bonjour portail Azure, hello **l’intégrité du matériel** sous hello **moniteur** panneau indique si la batterie de hello est défectueux ou hello en fin de vie est proche.</span><span class="sxs-lookup"><span data-stu-id="52241-173">In hello Azure portal, hello **Hardware health** under hello **Monitor** blade indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="52241-174">état de la batterie Hello est indiqué par **batterie dans PCM 0** ou **batterie dans PCM 1** sous **composants partagés**.</span><span class="sxs-lookup"><span data-stu-id="52241-174">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="52241-175">Ce panneau indiquera l’état **DÉTÉRIORÉ** si la fin de durée de vie approche et l’état **ÉCHEC** si elle est atteinte.</span><span class="sxs-lookup"><span data-stu-id="52241-175">This blade will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span>

> [!NOTE]
> <span data-ttu-id="52241-176">batterie de Hello peut signaler **n’a pas pu** lorsqu’elle doit simplement toobe facturé.</span><span class="sxs-lookup"><span data-stu-id="52241-176">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>


<span data-ttu-id="52241-177">Si hello **détérioré** état s’affiche, nous vous recommandons de hello suivant la marche à suivre :</span><span class="sxs-lookup"><span data-stu-id="52241-177">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="52241-178">système de Hello a peut-être rencontré une panne de courant récentes ou les piles hello peuvent être en cours de maintenance périodique.</span><span class="sxs-lookup"><span data-stu-id="52241-178">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="52241-179">Observez le système de hello pendant 12 heures avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="52241-179">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="52241-180">Si l’état de hello est toujours **détérioré** après 12 heures d’alimentation de tooAC connexion permanente avec hello contrôleurs et les PCM sont en cours d’exécution, puis hello batterie doit toobe remplacé.</span><span class="sxs-lookup"><span data-stu-id="52241-180">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="52241-181">Veuillez [contacter le support Microsoft](storsimple-8000-contact-microsoft-support.md) pour obtenir un module de batterie de secours de remplacement.</span><span class="sxs-lookup"><span data-stu-id="52241-181">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="52241-182">Si l’état de hello devient OK après 12 heures, hello batterie est opérationnelle, et il nécessaire uniquement les frais de maintenance.</span><span class="sxs-lookup"><span data-stu-id="52241-182">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="52241-183">S’il n’a pas été une entraîne une perte d’alimentation secteur et hello PCM est allumée et connecté tooAC power, batterie de hello doit toobe remplacé.</span><span class="sxs-lookup"><span data-stu-id="52241-183">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="52241-184">[Contactez le Support Microsoft](storsimple-8000-contact-microsoft-support.md) tooorder un module de batterie de secours.</span><span class="sxs-lookup"><span data-stu-id="52241-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52241-185">Dispose de hello Échec de la batterie en fonction de toonational et réglementations régionales.</span><span class="sxs-lookup"><span data-stu-id="52241-185">Dispose of hello failed battery according toonational and regional regulations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52241-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="52241-186">Next steps</span></span>
<span data-ttu-id="52241-187">En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="52241-187">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

