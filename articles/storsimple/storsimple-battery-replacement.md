---
title: "batterie aaaReplace sur l’appareil Microsoft Azure StorSimple | Documents Microsoft"
description: "Décrit comment remplacer les tooremove et mettre à jour le module de batterie de secours hello sur votre appareil StorSimple."
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
ms.openlocfilehash: 542774a5f451ec7ad2bd442f88598df318d8b285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="d9745-103">Remplacez le module de batterie de secours hello sur votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="d9745-103">Replace hello backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="d9745-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d9745-104">Overview</span></span>
<span data-ttu-id="d9745-105">boîtier principal de Hello d’alimentation et de Module de refroidissement (PCM) sur votre appareil Microsoft Azure StorSimple a un pack batterie supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="d9745-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="d9745-106">Ce pack fournit power afin que hello appareil StorSimple peut enregistrer les données si la perte de boîtier principal du toohello d’alimentation secteur.</span><span class="sxs-lookup"><span data-stu-id="d9745-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="d9745-107">Ce pack batterie est référencé tooas hello *module de batterie de secours*.</span><span class="sxs-lookup"><span data-stu-id="d9745-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="d9745-108">module de batterie de secours Hello existe uniquement pour le boîtier principal de hello dans votre appareil StorSimple (hello boîtiers ne contient pas un module de batterie de secours).</span><span class="sxs-lookup"><span data-stu-id="d9745-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="d9745-109">Ce didacticiel explique comment :</span><span class="sxs-lookup"><span data-stu-id="d9745-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="d9745-110">Supprimer le module de batterie de secours hello</span><span class="sxs-lookup"><span data-stu-id="d9745-110">Remove hello backup battery module</span></span> 
* <span data-ttu-id="d9745-111">Installer un nouveau module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="d9745-111">Install a new backup battery module</span></span>
* <span data-ttu-id="d9745-112">Mettre à jour le module de batterie de secours hello</span><span class="sxs-lookup"><span data-stu-id="d9745-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9745-113">Avant la suppression et le remplacement d’un module de batterie de secours, passez en revue les informations de sécurité hello Bonjour [remplacement de composant matériel Introduction tooStorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="d9745-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="d9745-114">Supprimer le module de batterie de secours hello</span><span class="sxs-lookup"><span data-stu-id="d9745-114">Remove hello backup battery module</span></span>
<span data-ttu-id="d9745-115">module de batterie de secours Hello pour votre appareil StorSimple est une unité remplaçable.</span><span class="sxs-lookup"><span data-stu-id="d9745-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="d9745-116">Avant son installation Bonjour PCM, module de batterie hello doit être stockée dans son emballage d’origine.</span><span class="sxs-lookup"><span data-stu-id="d9745-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="d9745-117">Effectuer hello suivant la batterie de secours étapes tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="d9745-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="d9745-118">module de batterie de secours hello tooremove</span><span class="sxs-lookup"><span data-stu-id="d9745-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="d9745-119">Dans hello portail Azure classic, accédez trop**périphériques** > **Maintenance** > **état du matériel**.</span><span class="sxs-lookup"><span data-stu-id="d9745-119">In hello Azure classic portal, go too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="d9745-120">Sous **composants partagés**, regardez statut hello de batterie de hello.</span><span class="sxs-lookup"><span data-stu-id="d9745-120">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="d9745-121">Identifier le PCM hello dans le hello batterie a échoué.</span><span class="sxs-lookup"><span data-stu-id="d9745-121">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="d9745-122">La figure 1 montre hello arrière de l’appareil StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="d9745-122">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![Fond du panier des modules du boîtier principal de l’appareil](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="d9745-124">**Figure 1** Arrière de l’appareil principal avec les modules PCM et de contrôleur</span><span class="sxs-lookup"><span data-stu-id="d9745-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="d9745-125">Étiquette</span><span class="sxs-lookup"><span data-stu-id="d9745-125">Label</span></span> | <span data-ttu-id="d9745-126">Description</span><span class="sxs-lookup"><span data-stu-id="d9745-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="d9745-127">1</span><span class="sxs-lookup"><span data-stu-id="d9745-127">1</span></span> |<span data-ttu-id="d9745-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="d9745-128">PCM 0</span></span> |
   | <span data-ttu-id="d9745-129">2</span><span class="sxs-lookup"><span data-stu-id="d9745-129">2</span></span> |<span data-ttu-id="d9745-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="d9745-130">PCM 1</span></span> |
   | <span data-ttu-id="d9745-131">3</span><span class="sxs-lookup"><span data-stu-id="d9745-131">3</span></span> |<span data-ttu-id="d9745-132">Contrôleur 0</span><span class="sxs-lookup"><span data-stu-id="d9745-132">Controller 0</span></span> |
   | <span data-ttu-id="d9745-133">4</span><span class="sxs-lookup"><span data-stu-id="d9745-133">4</span></span> |<span data-ttu-id="d9745-134">Contrôleur 1</span><span class="sxs-lookup"><span data-stu-id="d9745-134">Controller 1</span></span> |
   
    <span data-ttu-id="d9745-135">Comme indiqué par le numéro 3 Bonjour Figure 2, hello analyse indicateur LED sur PCM 0 qui correspond trop**panne** doit être allumée.</span><span class="sxs-lookup"><span data-stu-id="d9745-135">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![Fond du panier du module PCM de l’appareil avec voyants LED de surveillance](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="d9745-137">**Figure 2** hello d’affichage arrière du PCM des témoins DEL</span><span class="sxs-lookup"><span data-stu-id="d9745-137">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="d9745-138">Étiquette</span><span class="sxs-lookup"><span data-stu-id="d9745-138">Label</span></span> | <span data-ttu-id="d9745-139">Description</span><span class="sxs-lookup"><span data-stu-id="d9745-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="d9745-140">1</span><span class="sxs-lookup"><span data-stu-id="d9745-140">1</span></span> |<span data-ttu-id="d9745-141">Panne d’alimentation secteur</span><span class="sxs-lookup"><span data-stu-id="d9745-141">AC power failure</span></span> |
   | <span data-ttu-id="d9745-142">2</span><span class="sxs-lookup"><span data-stu-id="d9745-142">2</span></span> |<span data-ttu-id="d9745-143">Panne de ventilateur</span><span class="sxs-lookup"><span data-stu-id="d9745-143">Fan failure</span></span> |
   | <span data-ttu-id="d9745-144">3</span><span class="sxs-lookup"><span data-stu-id="d9745-144">3</span></span> |<span data-ttu-id="d9745-145">Panne de batterie</span><span class="sxs-lookup"><span data-stu-id="d9745-145">Battery fault</span></span> |
   | <span data-ttu-id="d9745-146">4</span><span class="sxs-lookup"><span data-stu-id="d9745-146">4</span></span> |<span data-ttu-id="d9745-147">PCM OK</span><span class="sxs-lookup"><span data-stu-id="d9745-147">PCM OK</span></span> |
   | <span data-ttu-id="d9745-148">5</span><span class="sxs-lookup"><span data-stu-id="d9745-148">5</span></span> |<span data-ttu-id="d9745-149">Panne d’alimentation secteur</span><span class="sxs-lookup"><span data-stu-id="d9745-149">DC power failure</span></span> |
   | <span data-ttu-id="d9745-150">6</span><span class="sxs-lookup"><span data-stu-id="d9745-150">6</span></span> |<span data-ttu-id="d9745-151">Batterie saine</span><span class="sxs-lookup"><span data-stu-id="d9745-151">Battery healthy</span></span> |
3. <span data-ttu-id="d9745-152">tooremove hello PCM avec la batterie est défectueuse, suivez les étapes de hello dans [retirer un PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="d9745-152">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="d9745-153">Hello PCM supprimé, courbes d’élévation et une batterie de rotation hello module gérer vers le haut, comme indiqué dans la figure suivante de hello et tirez dessus pour les batteries de hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="d9745-153">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![Retrait de la batterie du module PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="d9745-155">**Figure 3** supprime les batterie hello hello PCM</span><span class="sxs-lookup"><span data-stu-id="d9745-155">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="d9745-156">Placez le module de hello dans hello remplaçable emballage de l’unité.</span><span class="sxs-lookup"><span data-stu-id="d9745-156">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="d9745-157">Retourner tooMicrosoft d’unité défectueuse hello de maintenance et de gestion appropriée.</span><span class="sxs-lookup"><span data-stu-id="d9745-157">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="d9745-158">Installer un nouveau module de batterie de secours</span><span class="sxs-lookup"><span data-stu-id="d9745-158">Install a new backup battery module</span></span>
<span data-ttu-id="d9745-159">Effectuer hello suivant du module de batterie de rechange étapes tooinstall hello Bonjour PCM dans le boîtier principal de hello de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d9745-159">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="d9745-160">module de batterie hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="d9745-160">tooinstall hello battery module</span></span>
1. <span data-ttu-id="d9745-161">Placez le module de batterie de secours hello dans l’orientation appropriée de hello Bonjour PCM.</span><span class="sxs-lookup"><span data-stu-id="d9745-161">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="d9745-162">Module de batterie hello appuyez gérer connecteur hello de tous les hello moyen tooseat.</span><span class="sxs-lookup"><span data-stu-id="d9745-162">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="d9745-163">Remplacez hello PCM dans le boîtier principal de hello en suivant les instructions de hello dans [remplacer un Module de refroidissement et de puissance de votre appareil StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="d9745-163">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="d9745-164">Une fois le remplacement de hello terminée, accédez trop**périphériques** > **Maintenance** > **état du matériel** Bonjour portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="d9745-164">After hello replacement is complete, go too**Devices** > **Maintenance** > **Hardware Status** in hello Azure classic portal.</span></span> <span data-ttu-id="d9745-165">Vérifiez l’état hello de hello toomake de batterie que que hello installation a réussi.</span><span class="sxs-lookup"><span data-stu-id="d9745-165">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="d9745-166">Un état vert indique que la batterie de hello est sain.</span><span class="sxs-lookup"><span data-stu-id="d9745-166">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="d9745-167">Mettre à jour le module de batterie de secours hello</span><span class="sxs-lookup"><span data-stu-id="d9745-167">Maintain hello backup battery module</span></span>
<span data-ttu-id="d9745-168">Dans votre appareil StorSimple, module de batterie de secours hello fournit contrôleur toohello de l’alimentation pendant un événement de perte d’alimentation.</span><span class="sxs-lookup"><span data-stu-id="d9745-168">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="d9745-169">Il permet de hello StorSimple périphérique toosave données critiques de tooshutting de préalable vers le bas de manière contrôlée.</span><span class="sxs-lookup"><span data-stu-id="d9745-169">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="d9745-170">Avec deux batteries entièrement chargées Bonjour PCM, système de hello peut gérer deux d’affilée.</span><span class="sxs-lookup"><span data-stu-id="d9745-170">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="d9745-171">Bonjour portail Azure classic, hello **état du matériel** sur hello **Maintenance** page indique si la batterie de hello est défectueux ou hello en fin de vie est proche.</span><span class="sxs-lookup"><span data-stu-id="d9745-171">In hello Azure classic portal, hello **Hardware Status** on hello **Maintenance** page indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="d9745-172">état de la batterie Hello est indiqué par **batterie dans PCM 0** ou **batterie dans PCM 1** sous **composants partagés**.</span><span class="sxs-lookup"><span data-stu-id="d9745-172">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="d9745-173">Cette page indique l’état **DÉTÉRIORÉ** si la fin de durée de vie approche et l’état **ÉCHEC** si elle est atteinte.</span><span class="sxs-lookup"><span data-stu-id="d9745-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="d9745-174">batterie de Hello peut signaler **n’a pas pu** lorsqu’elle doit simplement toobe facturé.</span><span class="sxs-lookup"><span data-stu-id="d9745-174">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>
> 
> 

<span data-ttu-id="d9745-175">Si hello **détérioré** état s’affiche, nous vous recommandons de hello suivant la marche à suivre :</span><span class="sxs-lookup"><span data-stu-id="d9745-175">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="d9745-176">système de Hello a peut-être rencontré une panne de courant récentes ou les piles hello peuvent être en cours de maintenance périodique.</span><span class="sxs-lookup"><span data-stu-id="d9745-176">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="d9745-177">Observez le système de hello pendant 12 heures avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="d9745-177">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="d9745-178">Si l’état de hello est toujours **détérioré** après 12 heures d’alimentation de tooAC connexion permanente avec hello contrôleurs et les PCM sont en cours d’exécution, puis hello batterie doit toobe remplacé.</span><span class="sxs-lookup"><span data-stu-id="d9745-178">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="d9745-179">Veuillez [contacter le support Microsoft](storsimple-contact-microsoft-support.md) pour obtenir un module de batterie de secours de remplacement.</span><span class="sxs-lookup"><span data-stu-id="d9745-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="d9745-180">Si l’état de hello devient OK après 12 heures, hello batterie est opérationnelle, et il nécessaire uniquement les frais de maintenance.</span><span class="sxs-lookup"><span data-stu-id="d9745-180">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="d9745-181">S’il n’a pas été une entraîne une perte d’alimentation secteur et hello PCM est allumée et connecté tooAC power, batterie de hello doit toobe remplacé.</span><span class="sxs-lookup"><span data-stu-id="d9745-181">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="d9745-182">[Contactez le Support Microsoft](storsimple-contact-microsoft-support.md) tooorder un module de batterie de secours.</span><span class="sxs-lookup"><span data-stu-id="d9745-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9745-183">Dispose de hello Échec de la batterie en fonction de toonational et réglementations régionales.</span><span class="sxs-lookup"><span data-stu-id="d9745-183">Dispose of hello failed battery according toonational and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d9745-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9745-184">Next steps</span></span>
<span data-ttu-id="d9745-185">En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="d9745-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

