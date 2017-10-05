---
title: "Basculement, récupération d’urgence StorSimple vers une StorSimple Cloud Appliance| Microsoft Docs"
description: "Découvrez comment basculer votre appareil physique de la gamme StorSimple 8000 vers une appliance cloud."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: ec8bebf2854e84a37e84b45564e80fc20b63d8d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-to-your-storsimple-cloud-appliance"></a><span data-ttu-id="549f2-103">Basculer vers votre StorSimple Cloud Appliance</span><span class="sxs-lookup"><span data-stu-id="549f2-103">Fail over to your StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="549f2-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="549f2-104">Overview</span></span>

<span data-ttu-id="549f2-105">Ce didacticiel décrit les étapes requises pour basculer un appareil physique de la gamme StorSimple 8000 vers une StorSimple Cloud Appliance en cas de sinistre.</span><span class="sxs-lookup"><span data-stu-id="549f2-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to a StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="549f2-106">StorSimple utilise l’option de basculement d’appareil pour migrer des données d’un appareil physique source dans le centre de données vers une appliance cloud exécutée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="549f2-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to a cloud appliance running in Azure.</span></span> <span data-ttu-id="549f2-107">Les instructions de ce didacticiel s’appliquent aux appareils physiques de gamme StorSimple 8000 et aux appliances cloud exécutant des versions logicielles Update 3 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="549f2-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="549f2-108">Pour en savoir plus sur le basculement d’appareil et comment il est utilisé après un sinistre, accédez à [Basculement et récupération d’urgence pour les appareils StorSimple de la gamme 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="549f2-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="549f2-109">Pour basculer un appareil physique StorSimple vers un autre appareil physique, accédez à [Basculer vers un appareil physique StorSimple](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="549f2-109">To fail over a StorSimple physical device to another physical device, go to [Fail over to a StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="549f2-110">Pour basculer un appareil vers lui-même, accédez à [Basculer vers le même appareil physique StorSimple](storsimple-8000-device-failover-same-device.md).</span><span class="sxs-lookup"><span data-stu-id="549f2-110">To fail over a device to itself, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="549f2-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="549f2-111">Prerequisites</span></span>

- <span data-ttu-id="549f2-112">Assurez-vous d’avoir passé en revue les considérations relatives au basculement d’appareil.</span><span class="sxs-lookup"><span data-stu-id="549f2-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="549f2-113">Pour plus d’informations, accédez à [Considérations courantes relatives au basculement d’appareil](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="549f2-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="549f2-114">Vous devez avoir créé et configuré une StorSimple Cloud Appliance avant d’exécuter cette procédure.</span><span class="sxs-lookup"><span data-stu-id="549f2-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="549f2-115">Si vous exécutez la version logicielle Update 3 ou une version ultérieure, envisagez d’utiliser une appliance cloud 8020 pour la récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="549f2-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for the DR.</span></span> <span data-ttu-id="549f2-116">Le modèle 8020 a 64 To et utilise le stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="549f2-116">The 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="549f2-117">Pour plus d’informations, accédez à [Déployer et gérer une StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span><span class="sxs-lookup"><span data-stu-id="549f2-117">For more information, go to [Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-to-fail-over-to-a-cloud-appliance"></a><span data-ttu-id="549f2-118">Étapes de basculement vers une appliance cloud</span><span class="sxs-lookup"><span data-stu-id="549f2-118">Steps to fail over to a cloud appliance</span></span>

<span data-ttu-id="549f2-119">Procédez comme suit pour restaurer l’appareil vers une StorSimple Cloud Appliance cible.</span><span class="sxs-lookup"><span data-stu-id="549f2-119">Perform the following steps to restore the device to a target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="549f2-120">Vérifiez que le conteneur de volumes que vous souhaitez basculer est associé à des instantanés cloud.</span><span class="sxs-lookup"><span data-stu-id="549f2-120">Verify that the volume container you want to fail over has associated cloud snapshots.</span></span> <span data-ttu-id="549f2-121">Pour plus d’informations, accédez à [Utiliser le service StorSimple Device Manager pour créer des sauvegardes](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="549f2-121">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="549f2-122">Accédez à votre service StorSimple Device Manager et cliquez sur **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="549f2-122">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="549f2-123">Dans le panneau **Appareils**, accédez à la liste des appareils connectés à votre service.</span><span class="sxs-lookup"><span data-stu-id="549f2-123">In the **Devices** blade, go to the list of devices connected with your service.</span></span>
    <span data-ttu-id="549f2-124">![Sélectionner l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="549f2-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="549f2-125">Sélectionnez votre appareil source et cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="549f2-125">Select and click your source device.</span></span> <span data-ttu-id="549f2-126">L’appareil source comprend les conteneurs de volumes que vous souhaitez basculer.</span><span class="sxs-lookup"><span data-stu-id="549f2-126">The source device has the volume containers that you want to fail over.</span></span> <span data-ttu-id="549f2-127">Accédez à **Paramètres > Conteneurs de volumes**.</span><span class="sxs-lookup"><span data-stu-id="549f2-127">Go to **Settings > Volume Containers**.</span></span>

    ![Sélectionnez l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="549f2-129">Sélectionnez un conteneur de volume que vous souhaitez basculer vers un autre appareil.</span><span class="sxs-lookup"><span data-stu-id="549f2-129">Select a volume container that you would like to fail over to another device.</span></span> <span data-ttu-id="549f2-130">Cliquez sur le conteneur de volume pour afficher la liste des volumes dans ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="549f2-130">Click the volume container to display the list of volumes within this container.</span></span> <span data-ttu-id="549f2-131">Sélectionnez un volume, cliquez avec le bouton droit, puis cliquez sur **Mettre hors connexion** afin de mettre le volume hors connexion.</span><span class="sxs-lookup"><span data-stu-id="549f2-131">Select a volume, right-click, and click **Take Offline** to take the volume offline.</span></span>

    ![Sélectionnez l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="549f2-133">Répétez ce processus pour tous les volumes dans le conteneur de volume.</span><span class="sxs-lookup"><span data-stu-id="549f2-133">Repeat this process for all the volumes in the volume container.</span></span>

     ![Sélectionnez l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="549f2-135">Répétez l’étape précédente pour tous les conteneurs de volume que vous souhaitez basculer vers un autre appareil.</span><span class="sxs-lookup"><span data-stu-id="549f2-135">Repeat the previous step for all the volume containers you would like to fail over to another device.</span></span>

7. <span data-ttu-id="549f2-136">Revenez au panneau **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="549f2-136">Go back to the **Devices** blade.</span></span> <span data-ttu-id="549f2-137">Dans la barre de commandes, cliquez sur **Effectuer un basculement**.</span><span class="sxs-lookup"><span data-stu-id="549f2-137">From the command bar, click **Fail over**.</span></span>

    ![Cliquer sur Effectuer un basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="549f2-139">Dans le panneau **Effectuer un basculement**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="549f2-139">In the **Fail over** blade, perform the following steps:</span></span>
   
    1. <span data-ttu-id="549f2-140">Cliquez sur **Source**.</span><span class="sxs-lookup"><span data-stu-id="549f2-140">Click **Source**.</span></span> <span data-ttu-id="549f2-141">Sélectionnez les conteneurs de volumes à basculer.</span><span class="sxs-lookup"><span data-stu-id="549f2-141">Select the volume containers to fail over.</span></span> <span data-ttu-id="549f2-142">**Seuls les conteneurs de volumes associés à des instantanés cloud et des volumes hors connexion sont affichés.**</span><span class="sxs-lookup"><span data-stu-id="549f2-142">**Only the volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="549f2-143">![Sélectionner une source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="549f2-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="549f2-144">Cliquez sur **Cible**.</span><span class="sxs-lookup"><span data-stu-id="549f2-144">Click **Target**.</span></span> <span data-ttu-id="549f2-145">Sélectionnez une appliance cloud cible dans la liste déroulante des appareils disponibles.</span><span class="sxs-lookup"><span data-stu-id="549f2-145">Select a target cloud appliance from the dropdown list of available devices.</span></span> <span data-ttu-id="549f2-146">**Seuls les appareils disposant d’une capacité suffisante pour accueillir les conteneurs de volumes source sont affichés dans la liste.**</span><span class="sxs-lookup"><span data-stu-id="549f2-146">**Only the devices that have sufficient capacity to accommodate source volume containers are displayed in the list.**</span></span>

        ![Sélectionner la cible](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="549f2-148">Passez en revue les paramètres de basculement sous **Résumé** et activez la case à cocher indiquant que les volumes dans les conteneurs de volumes sélectionnés sont hors connexion.</span><span class="sxs-lookup"><span data-stu-id="549f2-148">Review the failover settings under **Summary** and select the checkbox indicating that the volumes in selected volume containers are offline.</span></span> 

        ![Passer en revue les paramètres de basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="549f2-150">Un travail de basculement est créé.</span><span class="sxs-lookup"><span data-stu-id="549f2-150">A failover job is created.</span></span> <span data-ttu-id="549f2-151">Pour surveiller le travail de basculement, cliquez sur la notification de travail.</span><span class="sxs-lookup"><span data-stu-id="549f2-151">To monitor the failover job, click the job notification.</span></span>

    ![Surveiller le travail de basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="549f2-153">Une fois le basculement terminé, revenez au panneau **Appareils** .</span><span class="sxs-lookup"><span data-stu-id="549f2-153">After the failover is completed, go back to the **Devices** blade.</span></span>

    1. <span data-ttu-id="549f2-154">Sélectionnez l’appareil qui a été utilisé en tant que cible pour le basculement.</span><span class="sxs-lookup"><span data-stu-id="549f2-154">Select the device that was used as the target for the failover.</span></span>

       ![Sélectionnez l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="549f2-156">Cliquez sur **Conteneurs de volumes**.</span><span class="sxs-lookup"><span data-stu-id="549f2-156">Click **Volume Containers**.</span></span> <span data-ttu-id="549f2-157">Tous les conteneurs de volume, ainsi que les volumes de l’ancien appareil, doivent être répertoriés.</span><span class="sxs-lookup"><span data-stu-id="549f2-157">All the volume containers, along with the volumes from the old device, should be listed.</span></span>

       <span data-ttu-id="549f2-158">Si le conteneur de volumes que vous avez basculé contient des volumes épinglés localement, ces volumes sont basculés en tant que volumes à plusieurs niveaux.</span><span class="sxs-lookup"><span data-stu-id="549f2-158">If the volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="549f2-159">Les volumes épinglés localement ne sont pas pris en charge sur une StorSimple Cloud Appliance.</span><span class="sxs-lookup"><span data-stu-id="549f2-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![Afficher les conteneurs de volumes cibles](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="549f2-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="549f2-161">Next steps</span></span>

* <span data-ttu-id="549f2-162">Après avoir effectué un basculement, vous devrez peut-être [désactiver ou supprimer votre appareil StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="549f2-162">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="549f2-163">Pour plus d’informations sur l’utilisation du service StorSimple Device Manager, accédez à [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md) (Utiliser le service StorSimple Device Manager pour gérer votre appareil StorSimple).</span><span class="sxs-lookup"><span data-stu-id="549f2-163">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

