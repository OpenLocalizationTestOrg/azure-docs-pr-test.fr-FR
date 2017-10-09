---
title: aaaReplace un PCM sur votre appareil StorSimple | Documents Microsoft
description: Explique comment tooremove et remplacer hello Module de refroidissement (PCM) sur votre appareil StorSimple
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: cc19ccb29884557720f7538b90dfb05268330b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="075da-103">Remplacer un module d’alimentation et de refroidissement (PCM, Power and Cooling Module) sur votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="075da-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="075da-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="075da-104">Overview</span></span>
<span data-ttu-id="075da-105">Hello d’alimentation et Module de refroidissement (PCM) dans votre appareil Microsoft Azure StorSimple se compose d’un bloc d’alimentation et des ventilateurs contrôlés par l’intermédiaire de type hello principal et les boîtiers.</span><span class="sxs-lookup"><span data-stu-id="075da-105">hello Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through hello primary and EBOD enclosures.</span></span> <span data-ttu-id="075da-106">Il n’existe qu’un seul modèle de PCM certifié pour chaque boîtier.</span><span class="sxs-lookup"><span data-stu-id="075da-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="075da-107">boîtier principal de Hello est certifié pour un PCM de 764 W et boîtiers hello est certifié pour un PCM de 580 W.</span><span class="sxs-lookup"><span data-stu-id="075da-107">hello primary enclosure is certified for a 764 W PCM and hello EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="075da-108">Bien que hello PCM pour le boîtier principal de hello et boîtiers hello sont différentes, la procédure de remplacement hello est identique.</span><span class="sxs-lookup"><span data-stu-id="075da-108">Although hello PCMs for hello primary enclosure and hello EBOD enclosure are different, hello replacement procedure is identical.</span></span>

<span data-ttu-id="075da-109">Ce didacticiel explique comment :</span><span class="sxs-lookup"><span data-stu-id="075da-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="075da-110">Retirer un PCM</span><span class="sxs-lookup"><span data-stu-id="075da-110">Remove a PCM</span></span>
* <span data-ttu-id="075da-111">Installer un PCM de remplacement</span><span class="sxs-lookup"><span data-stu-id="075da-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="075da-112">Avant de supprimer et remplacer un PCM, passez en revue les informations de sécurité hello dans [remplacement de composant matériel StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="075da-112">Before removing and replacing a PCM, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="075da-113">Avant de remplacer un PCM</span><span class="sxs-lookup"><span data-stu-id="075da-113">Before you replace a PCM</span></span>
<span data-ttu-id="075da-114">Tenez compte des hello suivant des problèmes importants avant de remplacer votre PCM :</span><span class="sxs-lookup"><span data-stu-id="075da-114">Be aware of hello following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="075da-115">Si hello d’alimentation de hello PCM tombe en panne, laissez hello module défectueux installé mais Retirez le cordon d’alimentation hello.</span><span class="sxs-lookup"><span data-stu-id="075da-115">If hello power supply of hello PCM fails, leave hello faulty module installed, but remove hello power cord.</span></span> <span data-ttu-id="075da-116">ventilateur de Hello sera power tooreceive de boîtier de hello et poursuivre tooprovide un refroidissement adéquat.</span><span class="sxs-lookup"><span data-stu-id="075da-116">hello fan will continue tooreceive power from hello enclosure and continue tooprovide proper cooling.</span></span> <span data-ttu-id="075da-117">Si le ventilateur de hello échoue, hello PCM doit toobe immédiatement remplacé.</span><span class="sxs-lookup"><span data-stu-id="075da-117">If hello fan fails, hello PCM needs toobe replaced immediately.</span></span>
* <span data-ttu-id="075da-118">Avant de supprimer hello PCM, débranchez hello alimentation hello PCM en désactivant le commutateur principal de hello (le cas échéant) ou en retirant physiquement le cordon d’alimentation hello.</span><span class="sxs-lookup"><span data-stu-id="075da-118">Before removing hello PCM, disconnect hello power from hello PCM by turning off hello main switch (where present) or by physically removing hello power cord.</span></span> <span data-ttu-id="075da-119">Cela fournit un système d’avertissement tooyour qu’un arrêt de l’alimentation est imminent.</span><span class="sxs-lookup"><span data-stu-id="075da-119">This provides a warning tooyour system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="075da-120">Vérifiez que hello pour qu'autre PCM est opérationnel la poursuite de système avant remplacement hello PCM défectueux.</span><span class="sxs-lookup"><span data-stu-id="075da-120">Make sure that hello other PCM is functional for continued system operation before replacing hello faulty PCM.</span></span> <span data-ttu-id="075da-121">Un PCM défectueux doit être remplacé dès que possible par un PCM totalement opérationnel.</span><span class="sxs-lookup"><span data-stu-id="075da-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="075da-122">Remplacement d’un module PCM prend uniquement de quelques minutes toocomplete, mais il doit être effectuée dans 10 minutes de la suppression de hello échoué PCM tooprevent surchauffe.</span><span class="sxs-lookup"><span data-stu-id="075da-122">PCM module replacement takes only few minutes toocomplete, but it must be completed within 10 minutes of removing hello failed PCM tooprevent overheating.</span></span>
* <span data-ttu-id="075da-123">Notez que hello remplacement 764 W modules PCM à la sortie d’usine de hello ne contiennent pas de module de batterie de secours hello.</span><span class="sxs-lookup"><span data-stu-id="075da-123">Note that hello replacement 764 W PCM modules shipped from hello factory do not contain hello backup battery module.</span></span> <span data-ttu-id="075da-124">Vous avez besoin de batterie de hello tooremove à partir de votre PCM défectueux et puis insérez-le dans le remplacement de hello hello remplacement module tooperforming préalable.</span><span class="sxs-lookup"><span data-stu-id="075da-124">You will need tooremove hello battery from your faulty PCM and then insert it into hello replacement module prior tooperforming hello replacement.</span></span> <span data-ttu-id="075da-125">Pour plus d’informations, consultez Comment trop[supprimer et insérer un module de batterie de secours](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="075da-125">For more information, see how too[remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="075da-126">Retirer un PCM</span><span class="sxs-lookup"><span data-stu-id="075da-126">Remove a PCM</span></span>
<span data-ttu-id="075da-127">Suivez ces instructions lorsque vous êtes prêt tooremove une puissance et Module de refroidissement (PCM) à partir de votre appareil Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="075da-127">Follow these instructions when you are ready tooremove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="075da-128">Avant de retirer le PCM, vérifiez que vous disposez d’un remplacement approprié (764 W pour le boîtier principal de hello) ou 580 W pour hello boîtiers.</span><span class="sxs-lookup"><span data-stu-id="075da-128">Before you remove your PCM, verify that you have a correct replacement (764 W for hello primary enclosure or 580 W for hello EBOD enclosure).</span></span>
> 
> 

#### <a name="tooremove-a-pcm"></a><span data-ttu-id="075da-129">tooremove un PCM</span><span class="sxs-lookup"><span data-stu-id="075da-129">tooremove a PCM</span></span>
1. <span data-ttu-id="075da-130">Bonjour portail Azure classic, cliquez sur **périphériques** > **Maintenance** > **état du matériel**.</span><span class="sxs-lookup"><span data-stu-id="075da-130">In hello Azure classic portal, click **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="075da-131">Vérifier l’état de hello des composants PCM hello sous **composants partagés** tooidentify le PCM défectueux :</span><span class="sxs-lookup"><span data-stu-id="075da-131">Check hello status of hello PCM components under **Shared Components** tooidentify which PCM has failed:</span></span>
   
   * <span data-ttu-id="075da-132">Si un bloc d’alimentation dans PCM 0 a échoué, hello état de **d’alimentation dans PCM 0** apparaîtra en rouge.</span><span class="sxs-lookup"><span data-stu-id="075da-132">If a power supply in PCM 0 has failed, hello status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="075da-133">Si un bloc d’alimentation dans PCM 1 a échoué, hello état de **alimentation dans PCM 1** apparaîtra en rouge.</span><span class="sxs-lookup"><span data-stu-id="075da-133">If a power supply in PCM 1 has failed, hello status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="075da-134">Si le ventilateur hello dans PCM 1 a échoué, hello statut de **de refroidissement 0 pour PCM 0** ou **refroidissement 1 pour PCM 0** apparaîtra en rouge.</span><span class="sxs-lookup"><span data-stu-id="075da-134">If hello fan in PCM 1 has failed, hello status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="075da-135">Recherchez hello PCM défectueux à hello arrière du boîtier principal de hello.</span><span class="sxs-lookup"><span data-stu-id="075da-135">Locate hello failed PCM on hello back of hello primary enclosure.</span></span> <span data-ttu-id="075da-136">Si vous exécutez un modèle 8600, identifier le boîtier principal de hello en examinant hello numéro d’Identification système unité affiché en hello DEL du panneau avant.</span><span class="sxs-lookup"><span data-stu-id="075da-136">If you are running an 8600 model, identify hello primary enclosure by looking at hello System Unit Identification Number shown on hello front panel LED display.</span></span> <span data-ttu-id="075da-137">Hello par défaut affiché sur le boîtier principal de hello est **00**, alors que la valeur par défaut hello ID d’unité est affiché sur hello boîtiers est **01**.</span><span class="sxs-lookup"><span data-stu-id="075da-137">hello default Unit ID displayed on hello primary enclosure is **00**, whereas hello default Unit ID displayed on hello EBOD enclosure is **01**.</span></span> <span data-ttu-id="075da-138">Hello diagramme et le tableau suivants expliquent façade de hello d’affichage de hello DEL.</span><span class="sxs-lookup"><span data-stu-id="075da-138">hello following diagram and table explain hello front panel of hello LED display.</span></span>
   
    ![ID du système sur le panneau avant des opérations](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="075da-140">**Figure 1** panneau avant de l’appareil de hello</span><span class="sxs-lookup"><span data-stu-id="075da-140">**Figure 1** Front panel of hello device</span></span>  
   
   | <span data-ttu-id="075da-141">Étiquette</span><span class="sxs-lookup"><span data-stu-id="075da-141">Label</span></span> | <span data-ttu-id="075da-142">Description</span><span class="sxs-lookup"><span data-stu-id="075da-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="075da-143">1</span><span class="sxs-lookup"><span data-stu-id="075da-143">1</span></span> |<span data-ttu-id="075da-144">Bouton Muet</span><span class="sxs-lookup"><span data-stu-id="075da-144">Mute button</span></span> |
   | <span data-ttu-id="075da-145">2</span><span class="sxs-lookup"><span data-stu-id="075da-145">2</span></span> |<span data-ttu-id="075da-146">Alimentation du système</span><span class="sxs-lookup"><span data-stu-id="075da-146">System power</span></span> |
   | <span data-ttu-id="075da-147">3</span><span class="sxs-lookup"><span data-stu-id="075da-147">3</span></span> |<span data-ttu-id="075da-148">Panne de module</span><span class="sxs-lookup"><span data-stu-id="075da-148">Module fault</span></span> |
   | <span data-ttu-id="075da-149">4</span><span class="sxs-lookup"><span data-stu-id="075da-149">4</span></span> |<span data-ttu-id="075da-150">Erreur logique</span><span class="sxs-lookup"><span data-stu-id="075da-150">Logical fault</span></span> |
   | <span data-ttu-id="075da-151">5</span><span class="sxs-lookup"><span data-stu-id="075da-151">5</span></span> |<span data-ttu-id="075da-152">Affichage de l’ID de l’unité</span><span class="sxs-lookup"><span data-stu-id="075da-152">Unit ID display</span></span> |
3. <span data-ttu-id="075da-153">Hello des témoins DEL Bonjour à l’arrière du boîtier principal de hello peut également être utilisé tooidentify hello PCM défectueux.</span><span class="sxs-lookup"><span data-stu-id="075da-153">hello monitoring indicator LEDs in hello back of hello primary enclosure can also be used tooidentify hello faulty PCM.</span></span> <span data-ttu-id="075da-154">Voir hello diagramme et tableau toounderstand comment toouse hello DEL toolocate hello PCM défectueux.</span><span class="sxs-lookup"><span data-stu-id="075da-154">See hello following diagram and table toounderstand how toouse hello LEDs toolocate hello faulty PCM.</span></span> <span data-ttu-id="075da-155">Par exemple, si hello conduit correspondant toohello **panne du ventilateur** est allumée, hello panne de ventilateur.</span><span class="sxs-lookup"><span data-stu-id="075da-155">For example, if hello LED corresponding toohello **Fan Fail** is lit, hello fan has failed.</span></span> <span data-ttu-id="075da-156">De même, si hello conduit correspondant trop**panne** est allumée, alimentation hello a échoué.</span><span class="sxs-lookup"><span data-stu-id="075da-156">Likewise, if hello LED corresponding too**AC Fail** is lit, hello power supply has failed.</span></span> 
   
    ![Fond de panier des voyants LED de surveillance du PCM de l’appareil](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="075da-158">**Figure 2** : Arrière du PCM avec les voyants LED</span><span class="sxs-lookup"><span data-stu-id="075da-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="075da-159">Étiquette</span><span class="sxs-lookup"><span data-stu-id="075da-159">Label</span></span> | <span data-ttu-id="075da-160">Description</span><span class="sxs-lookup"><span data-stu-id="075da-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="075da-161">1</span><span class="sxs-lookup"><span data-stu-id="075da-161">1</span></span> |<span data-ttu-id="075da-162">Panne d’alimentation secteur</span><span class="sxs-lookup"><span data-stu-id="075da-162">AC power failure</span></span> |
   | <span data-ttu-id="075da-163">2</span><span class="sxs-lookup"><span data-stu-id="075da-163">2</span></span> |<span data-ttu-id="075da-164">Panne de ventilateur</span><span class="sxs-lookup"><span data-stu-id="075da-164">Fan failure</span></span> |
   | <span data-ttu-id="075da-165">3</span><span class="sxs-lookup"><span data-stu-id="075da-165">3</span></span> |<span data-ttu-id="075da-166">Panne de batterie</span><span class="sxs-lookup"><span data-stu-id="075da-166">Battery fault</span></span> |
   | <span data-ttu-id="075da-167">4</span><span class="sxs-lookup"><span data-stu-id="075da-167">4</span></span> |<span data-ttu-id="075da-168">PCM OK</span><span class="sxs-lookup"><span data-stu-id="075da-168">PCM OK</span></span> |
   | <span data-ttu-id="075da-169">5</span><span class="sxs-lookup"><span data-stu-id="075da-169">5</span></span> |<span data-ttu-id="075da-170">Panne d’alimentation secteur</span><span class="sxs-lookup"><span data-stu-id="075da-170">DC power failure</span></span> |
   | <span data-ttu-id="075da-171">6</span><span class="sxs-lookup"><span data-stu-id="075da-171">6</span></span> |<span data-ttu-id="075da-172">Batterie saine</span><span class="sxs-lookup"><span data-stu-id="075da-172">Battery healthy</span></span> |
4. <span data-ttu-id="075da-173">Consultez toohello suivant schéma Hello arrière module PCM de hello StorSimple périphérique toolocate hello a échoué.</span><span class="sxs-lookup"><span data-stu-id="075da-173">Refer toohello following diagram of hello back of hello StorSimple device toolocate hello failed PCM module.</span></span> <span data-ttu-id="075da-174">PCM 0 est sur hello gauche et PCM 1 est à droite de hello.</span><span class="sxs-lookup"><span data-stu-id="075da-174">PCM 0 is on hello left and PCM 1 is on hello right.</span></span> <span data-ttu-id="075da-175">table Hello qui suit décrit les modules hello.</span><span class="sxs-lookup"><span data-stu-id="075da-175">hello table that follows explains hello modules.</span></span>
   
     ![Fond du panier des modules du boîtier principal de l’appareil](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="075da-177">**Figure 3** : Arrière de l’appareil avec des modules enfichables</span><span class="sxs-lookup"><span data-stu-id="075da-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="075da-178">Étiquette</span><span class="sxs-lookup"><span data-stu-id="075da-178">Label</span></span> | <span data-ttu-id="075da-179">Description</span><span class="sxs-lookup"><span data-stu-id="075da-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="075da-180">1</span><span class="sxs-lookup"><span data-stu-id="075da-180">1</span></span> |<span data-ttu-id="075da-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="075da-181">PCM 0</span></span> |
   | <span data-ttu-id="075da-182">2</span><span class="sxs-lookup"><span data-stu-id="075da-182">2</span></span> |<span data-ttu-id="075da-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="075da-183">PCM 1</span></span> |
   | <span data-ttu-id="075da-184">3</span><span class="sxs-lookup"><span data-stu-id="075da-184">3</span></span> |<span data-ttu-id="075da-185">Contrôleur 0</span><span class="sxs-lookup"><span data-stu-id="075da-185">Controller 0</span></span> |
   | <span data-ttu-id="075da-186">4</span><span class="sxs-lookup"><span data-stu-id="075da-186">4</span></span> |<span data-ttu-id="075da-187">Contrôleur 1</span><span class="sxs-lookup"><span data-stu-id="075da-187">Controller 1</span></span> |
5. <span data-ttu-id="075da-188">Activer off hello PCM défectueux et débranchez d’alimentation hello.</span><span class="sxs-lookup"><span data-stu-id="075da-188">Turn off hello faulty PCM and disconnect hello power supply cord.</span></span> <span data-ttu-id="075da-189">Vous pouvez supprimer hello PCM.</span><span class="sxs-lookup"><span data-stu-id="075da-189">You can now remove hello PCM.</span></span>
6. <span data-ttu-id="075da-190">Saisissez le loquet de hello et côté hello Hello PCM gérer entre votre pouce et et serrez vos doigts handle de hello tooopen ensemble.</span><span class="sxs-lookup"><span data-stu-id="075da-190">Grasp hello latch and hello side of hello PCM handle between your thumb and forefinger, and squeeze them together tooopen hello handle.</span></span>
   
    ![Ouverture de la poignée du PCM](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="075da-192">**Figure 4** hello d’ouverture PCM gérer</span><span class="sxs-lookup"><span data-stu-id="075da-192">**Figure 4** Opening hello PCM handle</span></span>
7. <span data-ttu-id="075da-193">Saisissez la poignée de hello et supprimer hello PCM.</span><span class="sxs-lookup"><span data-stu-id="075da-193">Grip hello handle and remove hello PCM.</span></span>
   
    ![Retrait du PCM de l’appareil](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="075da-195">**Figure 5** suppression hello PCM</span><span class="sxs-lookup"><span data-stu-id="075da-195">**Figure 5** Removing hello PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="075da-196">Installer un PCM de remplacement</span><span class="sxs-lookup"><span data-stu-id="075da-196">Install a replacement PCM</span></span>
<span data-ttu-id="075da-197">Suivez ces instructions de tooinstall un PCM de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="075da-197">Follow these instructions tooinstall a PCM in your StorSimple device.</span></span> <span data-ttu-id="075da-198">Assurez-vous que vous avez inséré le remplacement de hello tooinstalling préalable hello batterie de secours module PCM (s’applique uniquement les PCM W too764).</span><span class="sxs-lookup"><span data-stu-id="075da-198">Ensure that you have inserted hello backup battery module prior tooinstalling hello replacement PCM (applies too764 W PCMs only).</span></span> <span data-ttu-id="075da-199">Pour plus d’informations, consultez Comment trop[supprimer et insérer un module de batterie de secours](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="075da-199">For more information, see how too[remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

#### <a name="tooinstall-a-pcm"></a><span data-ttu-id="075da-200">tooinstall un PCM</span><span class="sxs-lookup"><span data-stu-id="075da-200">tooinstall a PCM</span></span>
1. <span data-ttu-id="075da-201">Vérifiez que vous avez hello PCM de rechange correct pour ce boîtier.</span><span class="sxs-lookup"><span data-stu-id="075da-201">Verify that you have hello correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="075da-202">boîtier principal de Hello a besoin d’un PCM de 764 W et hello boîtiers doit être un PCM de 580 W.</span><span class="sxs-lookup"><span data-stu-id="075da-202">hello primary enclosure needs a 764 W PCM and hello EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="075da-203">Vous ne devez pas essayer toouse hello PCM de 580 W dans le boîtier principal de hello ou hello de 764 W Bonjour boîtiers.</span><span class="sxs-lookup"><span data-stu-id="075da-203">You should not attempt toouse hello 580 W PCM in hello Primary enclosure, or hello 764 W PCM in hello EBOD enclosure.</span></span> <span data-ttu-id="075da-204">Hello suivant montre l’illustration où tooidentify ces informations sur hello d’étiquette qui est apposée toohello PCM.</span><span class="sxs-lookup"><span data-stu-id="075da-204">hello following image shows where tooidentify this information on hello label that is affixed toohello PCM.</span></span>
   
    ![Étiquette du PCM de l’appareil](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="075da-206">**Figure 6** : Étiquette du PCM</span><span class="sxs-lookup"><span data-stu-id="075da-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="075da-207">Recherchez le boîtier toohello de dommages, en faisant particulièrement attention toohello connecteurs.</span><span class="sxs-lookup"><span data-stu-id="075da-207">Check for damage toohello enclosure, paying particular attention toohello connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="075da-208">**N’installez pas de module de hello si les broches sont tordues.**</span><span class="sxs-lookup"><span data-stu-id="075da-208">**Do not install hello module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="075da-209">Ouvrez hello PCM gérer Bonjour position, module de hello diapositive dans boîtier de hello.</span><span class="sxs-lookup"><span data-stu-id="075da-209">With hello PCM handle in hello open position, slide hello module into hello enclosure.</span></span>
   
    ![Installation du PCM de l’appareil](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="075da-211">**Figure 7** installation hello PCM</span><span class="sxs-lookup"><span data-stu-id="075da-211">**Figure 7** Installing hello PCM</span></span>
4. <span data-ttu-id="075da-212">Fermez manuellement la poignée PCM hello.</span><span class="sxs-lookup"><span data-stu-id="075da-212">Manually close hello PCM handle.</span></span> <span data-ttu-id="075da-213">Vous devez entendre un clic comme hello loquet de la poignée se met en place.</span><span class="sxs-lookup"><span data-stu-id="075da-213">You should hear a click as hello handle latch engages.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="075da-214">tooensure qui hello connecteur broches, vous pouvez doucement CIL sur hello handle sans libérer le verrou de hello.</span><span class="sxs-lookup"><span data-stu-id="075da-214">tooensure that hello connector pins have engaged, you can gently tug on hello handle without releasing hello latch.</span></span> <span data-ttu-id="075da-215">Si hello PCM sort, cela implique ce verrou hello a été fermé avant des connecteurs hello.</span><span class="sxs-lookup"><span data-stu-id="075da-215">If hello PCM slides out, it implies that hello latch was closed before hello connectors engaged.</span></span>
   > 
   > 
5. <span data-ttu-id="075da-216">Se connecter hello câbles toohello power d’alimentation et toohello PCM.</span><span class="sxs-lookup"><span data-stu-id="075da-216">Connect hello power cables toohello power source and toohello PCM.</span></span>
6. <span data-ttu-id="075da-217">Sécuriser les déformation hello dispositif anti-traction de relief.</span><span class="sxs-lookup"><span data-stu-id="075da-217">Secure hello strain relief bales.</span></span> 
7. <span data-ttu-id="075da-218">Activez hello PCM.</span><span class="sxs-lookup"><span data-stu-id="075da-218">Turn on hello PCM.</span></span>
8. <span data-ttu-id="075da-219">Vérifiez que le remplacement de hello a réussi : Bonjour portail classique Azure de votre service StorSimple Manager, accédez trop**périphériques** > **Maintenance**  >  **État du matériel**.</span><span class="sxs-lookup"><span data-stu-id="075da-219">Verify that hello replacement was successful: in hello Azure classic portal of your StorSimple Manager service, navigate too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="075da-220">Sous **composants partagés**, état hello Hello PCM doit être verte.</span><span class="sxs-lookup"><span data-stu-id="075da-220">Under **Shared Components**, hello status of hello PCM should be green.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="075da-221">Il peut prendre quelques minutes pour initialiser la toocompletely hello remplacement PCM.</span><span class="sxs-lookup"><span data-stu-id="075da-221">It may take a few minutes for hello replacement PCM toocompletely initialize.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="075da-222">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="075da-222">Next steps</span></span>
<span data-ttu-id="075da-223">En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="075da-223">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

