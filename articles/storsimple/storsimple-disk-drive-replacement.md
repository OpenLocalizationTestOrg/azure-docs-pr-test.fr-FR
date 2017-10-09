---
title: aaaReplace un lecteur de disque sur un appareil StorSimple | Documents Microsoft
description: "Explique comment tooreplace un disque du lecteur sur un boîtier principal StorSimple ou d’un boîtier EBOD."
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
ms.openlocfilehash: d2c78a6d951b0f00ac42e74a34cf1bc83952a3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a><span data-ttu-id="dc37a-103">Remplacer un lecteur de disque sur votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="dc37a-103">Replace a disk drive on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="dc37a-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="dc37a-104">Overview</span></span>
<span data-ttu-id="dc37a-105">Ce didacticiel explique comment vous pouvez retirer et remplacer un lecteur de disque dur défectueux ou défaillant sur un appareil Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dc37a-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="dc37a-106">tooreplace un lecteur de disque, vous devez :</span><span class="sxs-lookup"><span data-stu-id="dc37a-106">tooreplace a disk drive, you need to:</span></span>

* <span data-ttu-id="dc37a-107">Désactiver le dispositif de sécurisation hello</span><span class="sxs-lookup"><span data-stu-id="dc37a-107">Disengage hello antitamper lock</span></span>
* <span data-ttu-id="dc37a-108">Supprimer le lecteur de disque hello</span><span class="sxs-lookup"><span data-stu-id="dc37a-108">Remove hello disk drive</span></span>
* <span data-ttu-id="dc37a-109">Installer le lecteur de disque de remplacement hello</span><span class="sxs-lookup"><span data-stu-id="dc37a-109">Install hello replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc37a-110">Avant de retrait et le remplacement d’un disque dur, passez en revue les informations de sécurité hello dans [remplacement de composant matériel StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="dc37a-110">Before removing and replacing a disk drive, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="disengage-hello-antitamper-lock"></a><span data-ttu-id="dc37a-111">Désactiver le dispositif de sécurisation hello</span><span class="sxs-lookup"><span data-stu-id="dc37a-111">Disengage hello antitamper lock</span></span>
<span data-ttu-id="dc37a-112">Cette procédure explique comment dispositifs de hello sur votre appareil StorSimple peuvent verrouiller ou déverrouiller lorsque vous remplacez les lecteurs de disque hello.</span><span class="sxs-lookup"><span data-stu-id="dc37a-112">This procedure explains how hello antitamper locks on your StorSimple device can be engaged or disengaged when you replace hello disk drives.</span></span> <span data-ttu-id="dc37a-113">dispositifs de Hello sont montés dans des poignées de transport de lecteur hello et ils sont accessibles via une petite ouverture dans hello loquet de handle de hello.</span><span class="sxs-lookup"><span data-stu-id="dc37a-113">hello antitamper locks are fitted in hello drive carrier handles, and they are accessed through a small aperture in hello latch section of hello handle.</span></span> <span data-ttu-id="dc37a-114">Les lecteurs sont fournis avec les verrous hello définir la position toohello verrouillé.</span><span class="sxs-lookup"><span data-stu-id="dc37a-114">Drives are supplied with hello locks set toohello locked position.</span></span>

#### <a name="toounlock-hello-antitamper-lock"></a><span data-ttu-id="dc37a-115">Dispositif de sécurisation de toounlock hello</span><span class="sxs-lookup"><span data-stu-id="dc37a-115">toounlock hello antitamper lock</span></span>
1. <span data-ttu-id="dc37a-116">Insérez soigneusement la clé de verrouillage de hello (tournevis « infalsifiables « T10 fourni par Microsoft) en ouverture hello du handle hello et le socket.</span><span class="sxs-lookup"><span data-stu-id="dc37a-116">Carefully insert hello lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into hello aperture in hello handle and into its socket.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="dc37a-117">Si le dispositif de sécurisation hello est activé, indicateur de hello rouge est visible dans l’ouverture de hello.</span><span class="sxs-lookup"><span data-stu-id="dc37a-117">If hello antitamper lock is activated, hello red indicator is visible in hello aperture.</span></span>
   > 
   > 
   
    ![Lecteur de disque verrouillé](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="dc37a-119">**Figure 1** : Verrou anti-effraction engagé</span><span class="sxs-lookup"><span data-stu-id="dc37a-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="dc37a-120">Étiquette</span><span class="sxs-lookup"><span data-stu-id="dc37a-120">Label</span></span> | <span data-ttu-id="dc37a-121">Description</span><span class="sxs-lookup"><span data-stu-id="dc37a-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="dc37a-122">1</span><span class="sxs-lookup"><span data-stu-id="dc37a-122">1</span></span> |<span data-ttu-id="dc37a-123">Ouverture de l’indicateur</span><span class="sxs-lookup"><span data-stu-id="dc37a-123">Indicator aperture</span></span> |
   | <span data-ttu-id="dc37a-124">2</span><span class="sxs-lookup"><span data-stu-id="dc37a-124">2</span></span> |<span data-ttu-id="dc37a-125">Verrou anti-effraction</span><span class="sxs-lookup"><span data-stu-id="dc37a-125">Antitamper lock</span></span> |
2. <span data-ttu-id="dc37a-126">Clé de rotation hello dans un sens inverse des aiguilles jusqu'à ce que l’indicateur de hello rouge n’est pas visible dans l’ouverture de hello au-dessus de la clé de hello.</span><span class="sxs-lookup"><span data-stu-id="dc37a-126">Rotate hello key in an anticlockwise direction until hello red indicator is not visible in hello aperture above hello key.</span></span>
3. <span data-ttu-id="dc37a-127">Supprimez la clé de hello.</span><span class="sxs-lookup"><span data-stu-id="dc37a-127">Remove hello key.</span></span>
   
    ![ : Lecteur de disque déverrouillé](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="dc37a-129">**Figure 2** : Lecteur de disque déverrouillé</span><span class="sxs-lookup"><span data-stu-id="dc37a-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="dc37a-130">lecteur de disque Hello peut maintenant être supprimée.</span><span class="sxs-lookup"><span data-stu-id="dc37a-130">hello disk drive can now be removed.</span></span>

<span data-ttu-id="dc37a-131">Suivez les étapes de hello de verrou de hello tooengage inverse.</span><span class="sxs-lookup"><span data-stu-id="dc37a-131">Follow hello steps in reverse tooengage hello lock.</span></span>

## <a name="remove-hello-disk-drive"></a><span data-ttu-id="dc37a-132">Supprimer le lecteur de disque hello</span><span class="sxs-lookup"><span data-stu-id="dc37a-132">Remove hello disk drive</span></span>
<span data-ttu-id="dc37a-133">Votre appareil StorSimple prend en charge une configuration des espaces de stockage en RAID 10.</span><span class="sxs-lookup"><span data-stu-id="dc37a-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="dc37a-134">Ceci implique qu’il peut fonctionner normalement avec un disque défectueux, qui peut être un disque SSD ou un disque dur.</span><span class="sxs-lookup"><span data-stu-id="dc37a-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="dc37a-135">Si votre système a plus d’un disque en panne, ne supprimez pas plus d’un disque SSD ou HDD système hello à n’importe quel point dans le temps.</span><span class="sxs-lookup"><span data-stu-id="dc37a-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from hello system at any point in time.</span></span> <span data-ttu-id="dc37a-136">Ceci peut entraîner la perte de données.</span><span class="sxs-lookup"><span data-stu-id="dc37a-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="dc37a-137">Veillez à placer un disque SSD de remplacement à un emplacement qui contenait auparavant un disque SSD.</span><span class="sxs-lookup"><span data-stu-id="dc37a-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="dc37a-138">De même, veillez à placer un disque dur de remplacement à un emplacement qui contenait auparavant un disque dur.</span><span class="sxs-lookup"><span data-stu-id="dc37a-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="dc37a-139">Bonjour portail Azure classic, les emplacements sont numérotés de 0 à 11.</span><span class="sxs-lookup"><span data-stu-id="dc37a-139">In hello Azure classic portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="dc37a-140">Par conséquent, si le portail de hello montre qu’un disque dans l’emplacement 2 a échoué sur l’appareil de hello, recherchez hello disque en panne dans l’emplacement de tiers hello hello en haut à gauche.</span><span class="sxs-lookup"><span data-stu-id="dc37a-140">Therefore, if hello portal shows that a disk in slot 2 has failed, on hello device, look for hello failed disk in hello third slot from hello top left.</span></span>
> 
> 

<span data-ttu-id="dc37a-141">Lecteurs peuvent être supprimés et remplacés pendant le fonctionnement du système de hello.</span><span class="sxs-lookup"><span data-stu-id="dc37a-141">Drives can be removed and replaced while hello system is operating.</span></span>

#### <a name="tooremove-a-drive"></a><span data-ttu-id="dc37a-142">tooremove un lecteur</span><span class="sxs-lookup"><span data-stu-id="dc37a-142">tooremove a drive</span></span>
1. <span data-ttu-id="dc37a-143">tooidentify hello disque défaillant hello portail Azure classic, dans accédez trop**périphériques** > **Maintenance** > **état du matériel**.</span><span class="sxs-lookup"><span data-stu-id="dc37a-143">tooidentify hello failed disk, in hello Azure classic portal, go too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="dc37a-144">Car un disque peut échouer dans le boîtier principal de hello et/ou un boîtier EBOD (si vous utilisez un modèle 8600), examinez état hello de disques hello sous **composants partagés** et sous **EBOD composants partagés du boîtier**.</span><span class="sxs-lookup"><span data-stu-id="dc37a-144">Because a disk can fail in hello primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at hello status of hello disks under **Shared Components** and under **EBOD enclosure Shared Components**.</span></span> <span data-ttu-id="dc37a-145">Un disque défectueux dans un des boîtiers est affiché avec un état rouge.</span><span class="sxs-lookup"><span data-stu-id="dc37a-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="dc37a-146">Recherchez hello lecteurs à l’avant du boîtier principal de hello ou boîtiers hello hello.</span><span class="sxs-lookup"><span data-stu-id="dc37a-146">Locate hello drives in hello front of hello primary enclosure or hello EBOD enclosure.</span></span> 
3. <span data-ttu-id="dc37a-147">Si le disque de hello est déverrouillé, passez toohello prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="dc37a-147">If hello disk is unlocked, proceed toohello next step.</span></span> <span data-ttu-id="dc37a-148">Si le disque de hello est verrouillé, déverrouillez-le en suivant la procédure hello dans [désactiver le dispositif de sécurisation hello](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="dc37a-148">If hello disk is locked, unlock it by following hello procedure in [Disengage hello antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="dc37a-149">Appuyez sur hello noir de verrous internes sur le module de transport hello et extraient retirer poignée hello avant de hello du châssis de hello.</span><span class="sxs-lookup"><span data-stu-id="dc37a-149">Press hello black latch on hello drive carrier module and pull hello drive carrier handle out and away from hello front of hello chassis.</span></span> 
   
    ![Libération de la poignée du lecteur de disque](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="dc37a-151">**Figure 3** poignée hello libération</span><span class="sxs-lookup"><span data-stu-id="dc37a-151">**Figure 3** Releasing hello drive handle</span></span>
5. <span data-ttu-id="dc37a-152">Lors de la poignée du lecteur hello est entièrement développée, faites glisser hello lecteur hors du châssis de hello.</span><span class="sxs-lookup"><span data-stu-id="dc37a-152">When hello drive carrier handle is fully extended, slide hello drive carrier out of hello chassis.</span></span> 
   
    ![Retrait du disque hors du lecteur de disque](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="dc37a-154">**Figure 4** glissante disque hello en dehors de l’opérateur de hello</span><span class="sxs-lookup"><span data-stu-id="dc37a-154">**Figure 4** Sliding hello disk drive out of hello carrier</span></span>

## <a name="install-hello-replacement-disk-drive"></a><span data-ttu-id="dc37a-155">Installer le lecteur de disque de remplacement hello</span><span class="sxs-lookup"><span data-stu-id="dc37a-155">Install hello replacement disk drive</span></span>
<span data-ttu-id="dc37a-156">Après un lecteur de disque défectueux dans votre appareil StorSimple et vous l’avez supprimé, suivez cette procédure tooreplace avec un nouveau lecteur.</span><span class="sxs-lookup"><span data-stu-id="dc37a-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure tooreplace it with a new drive.</span></span>

#### <a name="tooinsert-a-drive"></a><span data-ttu-id="dc37a-157">tooinsert un lecteur</span><span class="sxs-lookup"><span data-stu-id="dc37a-157">tooinsert a drive</span></span>
1. <span data-ttu-id="dc37a-158">Vérifiez la poignée hello est entièrement développée, comme indiqué dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="dc37a-158">Ensure hello drive carrier handle is fully extended, as shown in hello following image.</span></span>
   
    ![Lecteur de disque avec la poignée en extension](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="dc37a-160">**Figure 5** : Lecteur avec la poignée en extension</span><span class="sxs-lookup"><span data-stu-id="dc37a-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="dc37a-161">Faites glisser hello lecteur moyen de tous les hello dans le châssis de hello.</span><span class="sxs-lookup"><span data-stu-id="dc37a-161">Slide hello drive carrier all hello way into hello chassis.</span></span> 
   
    ![Insertion du disque dans le support de lecteur disque](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="dc37a-163">**Figure 6** support hello décalé dans le châssis de hello</span><span class="sxs-lookup"><span data-stu-id="dc37a-163">**Figure 6**  Sliding hello drive carrier into hello chassis</span></span>
3. <span data-ttu-id="dc37a-164">Avec hello lecteur transporteur hello inséré, fermez sa poignée lors de la poursuite de l’opération toopush hello support dans le châssis hello, jusqu'à ce que la poignée du lecteur hello s’aligne en position verrouillée.</span><span class="sxs-lookup"><span data-stu-id="dc37a-164">With hello drive carrier inserted, close hello drive carrier handle while continuing toopush hello drive carrier into hello chassis, until hello drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="dc37a-165">Utilisez hello clé de verrouillage a été fournie par la poignée du support Microsoft (tournevis de Torx inviolable) toosecure hello en place en activant le hello verrou vis un quart de tour dans le sens horaire.</span><span class="sxs-lookup"><span data-stu-id="dc37a-165">Use hello lock key that was provided by Microsoft (tamperproof Torx screwdriver) toosecure hello carrier handle into place by turning hello lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="dc37a-166">Vérifiez que hello remplacement a fonctionné et que lecteur de hello est opérationnel en accédant, via hello portail Azure classic, trop**Maintenance** > **état du matériel**.</span><span class="sxs-lookup"><span data-stu-id="dc37a-166">Verify that hello replacement was successful and hello drive is operational by accessing hello Azure classic portal and navigating too**Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="dc37a-167">Sous **composants partagés** ou **composants partagés du boîtier EBOD**, état du lecteur hello doit être vert, indiquant qu’il est sain.</span><span class="sxs-lookup"><span data-stu-id="dc37a-167">Under **Shared Components** or **EBOD enclosure Shared Components**, hello drive status should be green, indicating that it is healthy.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dc37a-168">Il peut prendre plusieurs heures hello disque état tooturn vert après le remplacement de hello.</span><span class="sxs-lookup"><span data-stu-id="dc37a-168">It may take several hours for hello disk status tooturn green after hello replacement.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="dc37a-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dc37a-169">Next steps</span></span>
<span data-ttu-id="dc37a-170">En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="dc37a-170">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

