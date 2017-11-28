---
title: "basculement aaaStorSimple, tooa de récupération d’urgence StorSimple Cloud Appliance | Documents Microsoft"
description: "Découvrez le matériel de cloud toofail sur votre tooa de périphérique physique StorSimple 8000 series."
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
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a><span data-ttu-id="4fe6e-103">Basculer tooyour StorSimple Appliance de Cloud</span><span class="sxs-lookup"><span data-stu-id="4fe6e-103">Fail over tooyour StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="4fe6e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4fe6e-104">Overview</span></span>

<span data-ttu-id="4fe6e-105">Ce didacticiel décrit toofail requis de hello étapes sur un tooa de périphérique physique StorSimple 8000 series StorSimple Appliance de Cloud s’il existe un reprise après sinistre.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooa StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="4fe6e-106">StorSimple utilise des données hello périphérique basculement fonctionnalité toomigrate à partir d’un périphérique physique source dans le dispositif de cloud hello datacenter tooa s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooa cloud appliance running in Azure.</span></span> <span data-ttu-id="4fe6e-107">conseils Hello dans ce didacticiel s’applique des périphériques physiques tooStorSimple 8000 series et appareils de cloud qui exécutent des versions de logiciel mise à jour 3 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="4fe6e-108">toolearn en savoir plus sur le basculement de l’appareil et comment il est utilisé toorecover d’urgence, consultez trop[basculement et récupération d’urgence pour les unités StorSimple 8000 series](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="4fe6e-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="4fe6e-109">toofail sur un appareil StorSimple appareil physique tooanother physique, allez trop[basculer sur un appareil physique StorSimple de tooa](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="4fe6e-109">toofail over a StorSimple physical device tooanother physical device, go too[Fail over tooa StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="4fe6e-110">toofail sur un appareil tooitself, accédez trop[basculer toohello même appareil physique StorSimple](storsimple-8000-device-failover-same-device.md).</span><span class="sxs-lookup"><span data-stu-id="4fe6e-110">toofail over a device tooitself, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fe6e-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4fe6e-111">Prerequisites</span></span>

- <span data-ttu-id="4fe6e-112">Vérifiez que vous avez consulté les considérations hello pour le basculement de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="4fe6e-113">Pour plus d’informations, consultez trop[considérations courantes pour le basculement de l’appareil](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="4fe6e-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="4fe6e-114">Vous devez avoir créé et configuré une StorSimple Cloud Appliance avant d’exécuter cette procédure.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="4fe6e-115">Si en cours d’exécution mettre à jour la version du logiciel 3 ou version ultérieure, envisagez d’utiliser un dispositif 8020 cloud pour hello récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for hello DR.</span></span> <span data-ttu-id="4fe6e-116">modèle 8020 de Hello a 64 To et utilise le stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-116">hello 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="4fe6e-117">Pour plus d’informations, consultez trop[déployer et gérer une application de Cloud StorSimple](storsimple-8000-cloud-appliance-u2.md).</span><span class="sxs-lookup"><span data-stu-id="4fe6e-117">For more information, go too[Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-toofail-over-tooa-cloud-appliance"></a><span data-ttu-id="4fe6e-118">Toofail étapes cloud via tooa</span><span class="sxs-lookup"><span data-stu-id="4fe6e-118">Steps toofail over tooa cloud appliance</span></span>

<span data-ttu-id="4fe6e-119">Effectuer hello suivant les étapes toorestore hello appareil tooa cible StorSimple Appliance de Cloud.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-119">Perform hello following steps toorestore hello device tooa target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="4fe6e-120">Vérifiez que hello conteneur de volume toofail sur a associé à des instantanés cloud.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-120">Verify that hello volume container you want toofail over has associated cloud snapshots.</span></span> <span data-ttu-id="4fe6e-121">Pour plus d’informations, consultez trop[sauvegardes toocreate du service Gestionnaire de périphériques StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="4fe6e-121">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="4fe6e-122">Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **périphériques**.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-122">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="4fe6e-123">Bonjour **périphériques** panneau, accédez toohello la liste des périphériques connectés à votre service.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-123">In hello **Devices** blade, go toohello list of devices connected with your service.</span></span>
    <span data-ttu-id="4fe6e-124">![Sélectionner l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="4fe6e-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="4fe6e-125">Sélectionnez votre appareil source et cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-125">Select and click your source device.</span></span> <span data-ttu-id="4fe6e-126">Appareil de source de Hello dispose des conteneurs de volumes hello que vous souhaitez toofail par.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-126">hello source device has hello volume containers that you want toofail over.</span></span> <span data-ttu-id="4fe6e-127">Accédez trop**Paramètres > conteneurs de volumes**.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-127">Go too**Settings > Volume Containers**.</span></span>

    ![Sélectionnez l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="4fe6e-129">Sélectionnez un conteneur de volumes que vous aimeriez toofail sur tooanother appareil.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-129">Select a volume container that you would like toofail over tooanother device.</span></span> <span data-ttu-id="4fe6e-130">Cliquez sur hello volume conteneur toodisplay hello liste des volumes de ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-130">Click hello volume container toodisplay hello list of volumes within this container.</span></span> <span data-ttu-id="4fe6e-131">Sélectionnez un volume, avec le bouton droit, puis cliquez sur **mettre hors connexion** tootake le volume hello hors connexion.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-131">Select a volume, right-click, and click **Take Offline** tootake hello volume offline.</span></span>

    ![Sélectionnez l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="4fe6e-133">Répétez ce processus pour tous les volumes hello dans le conteneur de volume hello.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-133">Repeat this process for all hello volumes in hello volume container.</span></span>

     ![Sélectionnez l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="4fe6e-135">Étape précédente de hello Répétez ces étapes pour tous les hello conteneurs de volumes vous aimeriez toofail sur tooanother appareil.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-135">Repeat hello previous step for all hello volume containers you would like toofail over tooanother device.</span></span>

7. <span data-ttu-id="4fe6e-136">Revenir en arrière toohello **périphériques** panneau.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-136">Go back toohello **Devices** blade.</span></span> <span data-ttu-id="4fe6e-137">Dans la barre de commandes hello, cliquez sur **basculer**.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-137">From hello command bar, click **Fail over**.</span></span>

    ![Cliquer sur Effectuer un basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="4fe6e-139">Bonjour **basculer** panneau, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4fe6e-139">In hello **Fail over** blade, perform hello following steps:</span></span>
   
    1. <span data-ttu-id="4fe6e-140">Cliquez sur **Source**.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-140">Click **Source**.</span></span> <span data-ttu-id="4fe6e-141">Sélectionnez toofail de conteneurs de volume hello sur.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-141">Select hello volume containers toofail over.</span></span> <span data-ttu-id="4fe6e-142">**Hello uniquement les conteneurs de volumes avec des instantanés cloud associés et les volumes hors connexion sont affichés.**</span><span class="sxs-lookup"><span data-stu-id="4fe6e-142">**Only hello volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="4fe6e-143">![Sélectionner une source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="4fe6e-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="4fe6e-144">Cliquez sur **Cible**.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-144">Click **Target**.</span></span> <span data-ttu-id="4fe6e-145">Sélectionnez une cible cloud à partir de la liste déroulante de hello de périphériques disponibles.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-145">Select a target cloud appliance from hello dropdown list of available devices.</span></span> <span data-ttu-id="4fe6e-146">**Uniquement hello pour les appareils qui ont des conteneurs de volumes source suffisamment capacité tooaccommodate sont affichent dans la liste de hello.**</span><span class="sxs-lookup"><span data-stu-id="4fe6e-146">**Only hello devices that have sufficient capacity tooaccommodate source volume containers are displayed in hello list.**</span></span>

        ![Sélectionner la cible](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="4fe6e-148">Passez en revue les paramètres de basculement hello sous **Résumé** et sélectionnez la case à cocher de hello indiquant que les volumes hello dans les conteneurs de volumes sélectionnés sont hors connexion.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-148">Review hello failover settings under **Summary** and select hello checkbox indicating that hello volumes in selected volume containers are offline.</span></span> 

        ![Passer en revue les paramètres de basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="4fe6e-150">Un travail de basculement est créé.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-150">A failover job is created.</span></span> <span data-ttu-id="4fe6e-151">basculement de hello toomonitor des tâches, cliquez sur la notification de travail hello.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-151">toomonitor hello failover job, click hello job notification.</span></span>

    ![Surveiller le travail de basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="4fe6e-153">Une fois que hello basculement terminé, revenez toohello **périphériques** panneau.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-153">After hello failover is completed, go back toohello **Devices** blade.</span></span>

    1. <span data-ttu-id="4fe6e-154">Sélectionnez le périphérique hello qui a été utilisé en tant que cible de hello pour le basculement de hello.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-154">Select hello device that was used as hello target for hello failover.</span></span>

       ![Sélectionnez l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="4fe6e-156">Cliquez sur **Conteneurs de volumes**.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-156">Click **Volume Containers**.</span></span> <span data-ttu-id="4fe6e-157">Tous les conteneurs de volume hello, ainsi que les volumes hello à partir de l’ancien périphérique de hello, doivent être répertoriés.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-157">All hello volume containers, along with hello volumes from hello old device, should be listed.</span></span>

       <span data-ttu-id="4fe6e-158">Si le conteneur de volume hello ayant basculé a attaché localement les volumes, les volumes sont basculés en tant que volumes hiérarchisés.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-158">If hello volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="4fe6e-159">Les volumes épinglés localement ne sont pas pris en charge sur une StorSimple Cloud Appliance.</span><span class="sxs-lookup"><span data-stu-id="4fe6e-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![Afficher les conteneurs de volumes cibles](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="4fe6e-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4fe6e-161">Next steps</span></span>

* <span data-ttu-id="4fe6e-162">Une fois que vous avez effectué un basculement, vous devrez peut-être trop[désactiver ou supprimer votre appareil StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="4fe6e-162">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="4fe6e-163">Pour plus d’informations sur la façon dont toouse hello StorSimple le Gestionnaire de périphériques de service, accédez trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="4fe6e-163">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

