---
title: "Basculement et récupération d’urgence pour les appareils de la gamme StorSimple 8000 | Microsoft Docs"
description: "Découvrez comment basculer votre appareil StorSimple vers le même appareil."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: acc8929dc3476e9590e8e4d9526b38b7c0719570
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-your-storsimple-physical-device-to-same-device"></a><span data-ttu-id="1f2c6-103">Basculer votre appareil physique StorSimple vers le même appareil</span><span class="sxs-lookup"><span data-stu-id="1f2c6-103">Fail over your StorSimple physical device to same device</span></span>

## <a name="overview"></a><span data-ttu-id="1f2c6-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1f2c6-104">Overview</span></span>

<span data-ttu-id="1f2c6-105">Ce didacticiel décrit les étapes requises pour basculer un appareil physique de la gamme StorSimple 8000 vers un autre appareil physique StorSimple en cas d’incident.Ce didacticiel décrit les étapes requises pour basculer un appareil physique de la gamme StorSimple 8000 vers lui-même en cas d’incident.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to itself if there is a disaster.</span></span> <span data-ttu-id="1f2c6-106">StorSimple utilise l’option de basculement d’appareil pour migrer les données d’un appareil physique source dans le centre de données vers un autre appareil physique.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to another physical device.</span></span> <span data-ttu-id="1f2c6-107">Les instructions de ce didacticiel s’appliquent aux appareils physiques de la gamme StorSimple 8000 exécutant le logiciel Update 3 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="1f2c6-108">Pour plus d’informations sur le basculement d’appareil et son utilisation à des fins de récupération après un incident, accédez à [Failover and disaster recovery for your StorSimple 8000 series device](storsimple-8000-device-failover-disaster-recovery.md) (Basculement et récupération d’urgence pour vos appareils StorSimple de la gamme 8000).</span><span class="sxs-lookup"><span data-stu-id="1f2c6-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="1f2c6-109">Pour basculer un appareil physique StorSimple vers un autre appareil physique, accédez à [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-physical-device.md) (Basculer votre appareil physique StorSimple vers lui-même).</span><span class="sxs-lookup"><span data-stu-id="1f2c6-109">To fail over a physical device to another physical device, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="1f2c6-110">Pour basculer un appareil physique StorSimple vers une instance StorSimple Cloud Appliance, accédez à [Fail over to your StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md) (Basculement vers votre StorSimple Cloud Appliance).</span><span class="sxs-lookup"><span data-stu-id="1f2c6-110">To fail over a StorSimple physical device to a StorSimple Cloud Appliance, go to [Fail over to a StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="1f2c6-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1f2c6-111">Prerequisites</span></span>

- <span data-ttu-id="1f2c6-112">Assurez-vous d’avoir passé en revue les considérations relatives au basculement d’appareil.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="1f2c6-113">Pour plus d’informations, accédez à [Considérations courantes relatives au basculement d’appareil](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="1f2c6-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-to-fail-over-to-the-same-device"></a><span data-ttu-id="1f2c6-114">Procédure de basculement vers le même appareil</span><span class="sxs-lookup"><span data-stu-id="1f2c6-114">Steps to fail over to the same device</span></span>

<span data-ttu-id="1f2c6-115">Si vous avez besoin d’effectuer un basculement vers le même appareil, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-115">Perform the following steps if you need to fail over to the same device.</span></span>

1. <span data-ttu-id="1f2c6-116">Prenez des instantanés de cloud de tous les volumes de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-116">Take cloud snapshots of all the volumes in your device.</span></span> <span data-ttu-id="1f2c6-117">Pour plus d’informations, accédez à [Utiliser le service StorSimple Device Manager dans le portail Azure pour gérer les stratégies de sauvegarde](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="1f2c6-117">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="1f2c6-118">Réinitialisez votre appareil aux valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-118">Reset your device to factory defaults.</span></span> <span data-ttu-id="1f2c6-119">Suivez les instructions détaillées dans la section [Rétablissement des paramètres par défaut de l’appareil](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="1f2c6-119">Follow the detailed instructions in [how to reset a StorSimple device to factory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="1f2c6-120">Accédez au service StorSimple Device Manager, puis sélectionnez **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-120">Go to the StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="1f2c6-121">Dans le panneau **Appareils**, l’ancien appareil doit présenter l’état **Hors connexion**.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-121">In the **Devices** blade, the old device should show as **Offline**.</span></span>

    ![Appareil source hors connexion](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="1f2c6-123">Configurez votre appareil et réinscrivez-le auprès de votre service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="1f2c6-124">L’appareil nouvellement inscrit doit présenter l’état **Prêt pour la configuration**.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-124">The newly registered device should show as **Ready to set up**.</span></span> <span data-ttu-id="1f2c6-125">Le nom du nouvel appareil est le même que celui de l’ancien, mais il est suivi d’un chiffre pour indiquer que ses paramètres d’usine ont été rétablis et qu’il a été inscrit à nouveau.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-125">The device name for the new device is the same as the old device but appended with a numeral to indicate that the device was reset to factory default and registered again.</span></span>

    ![Appareil nouvellement inscrit prêt pour la configuration](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="1f2c6-127">Terminez l’installation du nouvel appareil.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-127">For the new device, complete the device setup.</span></span> <span data-ttu-id="1f2c6-128">Pour plus d’informations, accédez à [Étape 4 : Fin de l’installation minimale de l’appareil](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="1f2c6-128">For more information, go to [Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="1f2c6-129">Dans le panneau **Appareils**, l’appareil présente maintenant l’état **En ligne**.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-129">On the **Devices** blade, the status of the device changes to **Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1f2c6-130">**Effectuez tout d’abord la configuration minimale. Sinon, la récupération d’urgence risque d’échouer.**</span><span class="sxs-lookup"><span data-stu-id="1f2c6-130">**Complete the minimum configuration first, or your DR may fail.**</span></span>

    ![Appareil nouvellement inscrit en ligne](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="1f2c6-132">Sélectionnez l’ancien appareil (état Hors connexion) et dans la barre de commandes, cliquez sur **Basculement**.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-132">Select the old device (status offline) and from the command bar, click **Fail over**.</span></span> <span data-ttu-id="1f2c6-133">Dans le panneau **Basculement**, sélectionnez l’ancien appareil en tant que source et spécifiez l’appareil nouvellement inscrit en tant qu’appareil cible.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-133">In the **Fail over** blade, select old device as the source and specify the target device as the newly registered device.</span></span>

    ![Synthèse du basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="1f2c6-135">Pour obtenir des instructions détaillées, reportez-vous à la section [Basculer vers un autre appareil physique](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="1f2c6-135">For detailed instructions, refer to [Fail over to another physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="1f2c6-136">Un travail de restauration de l’appareil est créé. Vous pouvez suivre sa progression à partir du panneau **Travaux** .</span><span class="sxs-lookup"><span data-stu-id="1f2c6-136">A device restore job is created that you can monitor from the **Jobs** blade.</span></span>

8. <span data-ttu-id="1f2c6-137">Une fois ce travail terminé, accédez au nouvel appareil, puis au panneau **Conteneurs de volumes** .</span><span class="sxs-lookup"><span data-stu-id="1f2c6-137">After the job has successfully completed, access the new device and navigate to the **Volume containers** blade.</span></span> <span data-ttu-id="1f2c6-138">Vérifiez que tous les conteneurs de volumes de l’ancien appareil ont été migrés vers le nouvel appareil.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-138">Verify that all the volume containers from the old device have migrated to the new device.</span></span>

   ![Conteneurs de volumes migrés](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="1f2c6-140">Une fois le basculement terminé, vous pouvez désactiver et supprimer l’ancien appareil à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-140">After the failover is complete, you can deactivate and delete the old device from the portal.</span></span> <span data-ttu-id="1f2c6-141">Sélectionnez l’ancien appareil, cliquez avec le bouton droit, puis sélectionnez **Désactiver**.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-141">Select the old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="1f2c6-142">Une fois l’appareil désactivé, son état est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-142">After the device is deactivated, the status of the device is updated.</span></span>

     ![Appareil source désactivé](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="1f2c6-144">Sélectionnez l’appareil désactivé, cliquez avec le bouton droit, puis sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-144">Select the deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="1f2c6-145">Votre appareil est supprimé de la liste d’appareils.</span><span class="sxs-lookup"><span data-stu-id="1f2c6-145">This deletes the device from the list of devices.</span></span>

    ![Appareil source supprimé](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="1f2c6-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1f2c6-147">Next steps</span></span>

* <span data-ttu-id="1f2c6-148">Après avoir effectué un basculement, vous devrez peut-être [désactiver ou supprimer votre appareil StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="1f2c6-148">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="1f2c6-149">Pour plus d’informations sur l’utilisation du service StorSimple Device Manager, accédez à [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md) (Utiliser le service StorSimple Device Manager pour gérer votre appareil StorSimple).</span><span class="sxs-lookup"><span data-stu-id="1f2c6-149">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

