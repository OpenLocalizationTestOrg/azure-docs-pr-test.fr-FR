---
title: Remplacer un lecteur de disque sur un appareil StorSimple | Microsoft Docs
description: "Explique comment remplacer un lecteur de disque sur un boîtier principal ou EBOD StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 0659ab9d304dbfcce72e8c3c79edad68e70b9630
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a><span data-ttu-id="17a7d-103">Remplacer un lecteur de disque sur votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="17a7d-103">Replace a disk drive on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="17a7d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="17a7d-104">Overview</span></span>
<span data-ttu-id="17a7d-105">Ce didacticiel explique comment vous pouvez retirer et remplacer un lecteur de disque dur défectueux ou défaillant sur un appareil Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="17a7d-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="17a7d-106">Pour remplacer un lecteur de disque, vous devez :</span><span class="sxs-lookup"><span data-stu-id="17a7d-106">To replace a disk drive, you need to:</span></span>

* <span data-ttu-id="17a7d-107">Désengager le verrou anti-effraction</span><span class="sxs-lookup"><span data-stu-id="17a7d-107">Disengage the antitamper lock</span></span>
* <span data-ttu-id="17a7d-108">Retirer le lecteur de disque</span><span class="sxs-lookup"><span data-stu-id="17a7d-108">Remove the disk drive</span></span>
* <span data-ttu-id="17a7d-109">    Installez le lecteur de disque de remplacement</span><span class="sxs-lookup"><span data-stu-id="17a7d-109">Install the replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17a7d-110">Avant de retirer et de remplacer un lecteur de disque, passez en revue les informations de sécurité dans [Remplacement de composants matériels StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="17a7d-110">Before removing and replacing a disk drive, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="disengage-the-antitamper-lock"></a><span data-ttu-id="17a7d-111">Désengager le verrou anti-effraction</span><span class="sxs-lookup"><span data-stu-id="17a7d-111">Disengage the antitamper lock</span></span>
<span data-ttu-id="17a7d-112">Cette procédure explique comment les verrous anti-effraction sur votre appareil StorSimple peuvent être engagés ou désengagés quand vous remplacez les lecteurs de disque.</span><span class="sxs-lookup"><span data-stu-id="17a7d-112">This procedure explains how the antitamper locks on your StorSimple device can be engaged or disengaged when you replace the disk drives.</span></span> <span data-ttu-id="17a7d-113">Les verrous anti-effraction sont montés dans les poignées du support de lecteur et ils sont accessibles via une petite ouverture dans la partie verrou de la poignée.</span><span class="sxs-lookup"><span data-stu-id="17a7d-113">The antitamper locks are fitted in the drive carrier handles, and they are accessed through a small aperture in the latch section of the handle.</span></span> <span data-ttu-id="17a7d-114">Les lecteurs sont fournis avec les verrous en position verrouillée.</span><span class="sxs-lookup"><span data-stu-id="17a7d-114">Drives are supplied with the locks set to the locked position.</span></span>

#### <a name="to-unlock-the-antitamper-lock"></a><span data-ttu-id="17a7d-115">Pour déverrouiller le verrou anti-effraction</span><span class="sxs-lookup"><span data-stu-id="17a7d-115">To unlock the antitamper lock</span></span>
1. <span data-ttu-id="17a7d-116">Insérez soigneusement la clé de verrouillage (un tournevis « anti-effraction » T10 fourni par Microsoft) dans l’ouverture de la poignée et dans son emplacement.</span><span class="sxs-lookup"><span data-stu-id="17a7d-116">Carefully insert the lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into the aperture in the handle and into its socket.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="17a7d-117">Si le verrou anti-effraction est activé, l’indicateur rouge est visible dans l’ouverture.</span><span class="sxs-lookup"><span data-stu-id="17a7d-117">If the antitamper lock is activated, the red indicator is visible in the aperture.</span></span>
   > 
   > 
   
    ![Lecteur de disque verrouillé](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="17a7d-119">**Figure 1** : Verrou anti-effraction engagé</span><span class="sxs-lookup"><span data-stu-id="17a7d-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="17a7d-120">Étiquette</span><span class="sxs-lookup"><span data-stu-id="17a7d-120">Label</span></span> | <span data-ttu-id="17a7d-121">Description</span><span class="sxs-lookup"><span data-stu-id="17a7d-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="17a7d-122">1</span><span class="sxs-lookup"><span data-stu-id="17a7d-122">1</span></span> |<span data-ttu-id="17a7d-123">Ouverture de l’indicateur</span><span class="sxs-lookup"><span data-stu-id="17a7d-123">Indicator aperture</span></span> |
   | <span data-ttu-id="17a7d-124">2</span><span class="sxs-lookup"><span data-stu-id="17a7d-124">2</span></span> |<span data-ttu-id="17a7d-125">Verrou anti-effraction</span><span class="sxs-lookup"><span data-stu-id="17a7d-125">Antitamper lock</span></span> |
2. <span data-ttu-id="17a7d-126">Faites tourner la clé dans le sens inverse des aiguilles d’une montre jusqu’à ce que l’indicateur rouge ne soit plus visible dans l’ouverture au-dessus de la clé.</span><span class="sxs-lookup"><span data-stu-id="17a7d-126">Rotate the key in an anticlockwise direction until the red indicator is not visible in the aperture above the key.</span></span>
3. <span data-ttu-id="17a7d-127">Retirez la clé.</span><span class="sxs-lookup"><span data-stu-id="17a7d-127">Remove the key.</span></span>
   
    ![ : Lecteur de disque déverrouillé](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="17a7d-129">**Figure 2** : Lecteur de disque déverrouillé</span><span class="sxs-lookup"><span data-stu-id="17a7d-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="17a7d-130">Le lecteur de disque peut maintenant être retiré.</span><span class="sxs-lookup"><span data-stu-id="17a7d-130">The disk drive can now be removed.</span></span>

<span data-ttu-id="17a7d-131">Suivez les étapes en sens inverse pour engager le verrou.</span><span class="sxs-lookup"><span data-stu-id="17a7d-131">Follow the steps in reverse to engage the lock.</span></span>

## <a name="remove-the-disk-drive"></a><span data-ttu-id="17a7d-132">Retirer le lecteur de disque</span><span class="sxs-lookup"><span data-stu-id="17a7d-132">Remove the disk drive</span></span>
<span data-ttu-id="17a7d-133">Votre appareil StorSimple prend en charge une configuration des espaces de stockage en RAID 10.</span><span class="sxs-lookup"><span data-stu-id="17a7d-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="17a7d-134">Ceci implique qu’il peut fonctionner normalement avec un disque défectueux, qui peut être un disque SSD ou un disque dur.</span><span class="sxs-lookup"><span data-stu-id="17a7d-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="17a7d-135">Si votre système a plusieurs disques défectueux, ne retirez jamais en même temps plusieurs disques SSD ou disques durs du système.</span><span class="sxs-lookup"><span data-stu-id="17a7d-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from the system at any point in time.</span></span> <span data-ttu-id="17a7d-136">Ceci peut entraîner la perte de données.</span><span class="sxs-lookup"><span data-stu-id="17a7d-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="17a7d-137">Veillez à placer un disque SSD de remplacement à un emplacement qui contenait auparavant un disque SSD.</span><span class="sxs-lookup"><span data-stu-id="17a7d-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="17a7d-138">De même, veillez à placer un disque dur de remplacement à un emplacement qui contenait auparavant un disque dur.</span><span class="sxs-lookup"><span data-stu-id="17a7d-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="17a7d-139">Dans le portail Azure Classic, les emplacements sont numérotés de 0 à 11.</span><span class="sxs-lookup"><span data-stu-id="17a7d-139">In the Azure classic portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="17a7d-140">Par conséquent, si le portail indique qu’un disque à l’emplacement 2 est défectueux, sur l’appareil, vous trouvez le disque défectueux au troisième emplacement à partir du coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="17a7d-140">Therefore, if the portal shows that a disk in slot 2 has failed, on the device, look for the failed disk in the third slot from the top left.</span></span>
> 
> 

<span data-ttu-id="17a7d-141">Les lecteurs peuvent être retirés et remplacés pendant que le système fonctionne.</span><span class="sxs-lookup"><span data-stu-id="17a7d-141">Drives can be removed and replaced while the system is operating.</span></span>

#### <a name="to-remove-a-drive"></a><span data-ttu-id="17a7d-142">Pour retirer un lecteur</span><span class="sxs-lookup"><span data-stu-id="17a7d-142">To remove a drive</span></span>
1. <span data-ttu-id="17a7d-143">Pour identifier le disque défectueux, accédez dans le Portail Azure Classic à **Appareils** > **Maintenance** > **Statut du matériel**.</span><span class="sxs-lookup"><span data-stu-id="17a7d-143">To identify the failed disk, in the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="17a7d-144">Comme un disque défectueux peut se trouver dans le boîtier principal et/ou dans un boîtier EBOD (si vous utilisez un modèle 8600), vérifiez l’état des disques sous **Composants partagés** et sous **Composants partagés du boîtier EBOD**.</span><span class="sxs-lookup"><span data-stu-id="17a7d-144">Because a disk can fail in the primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at the status of the disks under **Shared Components** and under **EBOD enclosure Shared Components**.</span></span> <span data-ttu-id="17a7d-145">Un disque défectueux dans un des boîtiers est affiché avec un état rouge.</span><span class="sxs-lookup"><span data-stu-id="17a7d-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="17a7d-146">Recherchez les lecteurs à l’avant du boîtier principal ou du boîtier EBOD.</span><span class="sxs-lookup"><span data-stu-id="17a7d-146">Locate the drives in the front of the primary enclosure or the EBOD enclosure.</span></span> 
3. <span data-ttu-id="17a7d-147">Si le disque est déverrouillé, passez à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="17a7d-147">If the disk is unlocked, proceed to the next step.</span></span> <span data-ttu-id="17a7d-148">Si le disque est verrouillé, déverrouillez-le en suivant la procédure décrite dans [Désengager le verrou anti-effraction](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="17a7d-148">If the disk is locked, unlock it by following the procedure in [Disengage the antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="17a7d-149">Appuyez sur le verrou noir du module de support de lecteur et tirez sur la poignée du support de lecteur vers l’avant du châssis.</span><span class="sxs-lookup"><span data-stu-id="17a7d-149">Press the black latch on the drive carrier module and pull the drive carrier handle out and away from the front of the chassis.</span></span> 
   
    ![Libération de la poignée du lecteur de disque](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="17a7d-151">**Figure 3** : Libération de la poignée du lecteur</span><span class="sxs-lookup"><span data-stu-id="17a7d-151">**Figure 3** Releasing the drive handle</span></span>
5. <span data-ttu-id="17a7d-152">Quand la poignée du support de lecteur est entièrement en extension, faites glisser le support de lecteur hors du châssis.</span><span class="sxs-lookup"><span data-stu-id="17a7d-152">When the drive carrier handle is fully extended, slide the drive carrier out of the chassis.</span></span> 
   
    ![Retrait du disque hors du lecteur de disque](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="17a7d-154">**Figure 4** : Retrait du lecteur de disque hors du châssis</span><span class="sxs-lookup"><span data-stu-id="17a7d-154">**Figure 4** Sliding the disk drive out of the carrier</span></span>

## <a name="install-the-replacement-disk-drive"></a><span data-ttu-id="17a7d-155">    Installez le lecteur de disque de remplacement</span><span class="sxs-lookup"><span data-stu-id="17a7d-155">Install the replacement disk drive</span></span>
<span data-ttu-id="17a7d-156">Quand un lecteur est défectueux dans votre appareil StorSimple et que vous l’avez retiré, suivez cette procédure pour le remplacer par un nouveau lecteur.</span><span class="sxs-lookup"><span data-stu-id="17a7d-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure to replace it with a new drive.</span></span>

#### <a name="to-insert-a-drive"></a><span data-ttu-id="17a7d-157">Pour insérer un lecteur</span><span class="sxs-lookup"><span data-stu-id="17a7d-157">To insert a drive</span></span>
1. <span data-ttu-id="17a7d-158">Assurez-vous que la poignée du support de lecteur est entièrement en extension, comme illustré dans l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="17a7d-158">Ensure the drive carrier handle is fully extended, as shown in the following image.</span></span>
   
    ![Lecteur de disque avec la poignée en extension](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="17a7d-160">**Figure 5** : Lecteur avec la poignée en extension</span><span class="sxs-lookup"><span data-stu-id="17a7d-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="17a7d-161">Faites glisser le support de lecteur jusqu’au bout dans le châssis.</span><span class="sxs-lookup"><span data-stu-id="17a7d-161">Slide the drive carrier all the way into the chassis.</span></span> 
   
    ![Insertion du disque dans le support de lecteur disque](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="17a7d-163">**Figure 6** : Insertion du support de lecteur dans le châssis</span><span class="sxs-lookup"><span data-stu-id="17a7d-163">**Figure 6**  Sliding the drive carrier into the chassis</span></span>
3. <span data-ttu-id="17a7d-164">Le support de lecteur étant inséré, fermez la poignée du support de lecteur tout en continuant à pousser le support de lecteur dans le châssis, jusqu’à ce que la poignée du support de lecteur s’enclenche en position verrouillée.</span><span class="sxs-lookup"><span data-stu-id="17a7d-164">With the drive carrier inserted, close the drive carrier handle while continuing to push the drive carrier into the chassis, until the drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="17a7d-165">Utilisez la clé de verrouillage qui a été fournie par Microsoft (tournevis Torx anti-effraction) pour sécuriser la poignée du support à son emplacement en tournant la vis de verrouillage d’un quart de tour dans le sens des aiguilles d’une montre.</span><span class="sxs-lookup"><span data-stu-id="17a7d-165">Use the lock key that was provided by Microsoft (tamperproof Torx screwdriver) to secure the carrier handle into place by turning the lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="17a7d-166">Vérifiez que le remplacement a réussi et que le lecteur est opérationnel en accédant au portail Azure Classic, puis à **Maintenance** > **Statut du matériel**.</span><span class="sxs-lookup"><span data-stu-id="17a7d-166">Verify that the replacement was successful and the drive is operational by accessing the Azure classic portal and navigating to **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="17a7d-167">Sous **Composants partagés** ou **Composants partagés du boîtier EBOD**, l’état du disque doit être en vert, indiquant qu’il est intègre.</span><span class="sxs-lookup"><span data-stu-id="17a7d-167">Under **Shared Components** or **EBOD enclosure Shared Components**, the drive status should be green, indicating that it is healthy.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="17a7d-168">Plusieurs heures peuvent être nécessaires pour que l’état du disque passe en vert après le remplacement.</span><span class="sxs-lookup"><span data-stu-id="17a7d-168">It may take several hours for the disk status to turn green after the replacement.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="17a7d-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="17a7d-169">Next steps</span></span>
<span data-ttu-id="17a7d-170">En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="17a7d-170">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

