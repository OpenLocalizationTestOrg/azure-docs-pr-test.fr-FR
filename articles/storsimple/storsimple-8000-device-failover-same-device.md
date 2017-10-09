---
title: "basculement aaaStorSimple, récupération d’urgence pour les appareils 8000 series | Documents Microsoft"
description: "Découvrez comment toofail sur votre toohello de périphérique StorSimple même appareil."
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
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a><span data-ttu-id="9f57f-103">Basculer votre unité toosame du périphérique physique StorSimple</span><span class="sxs-lookup"><span data-stu-id="9f57f-103">Fail over your StorSimple physical device toosame device</span></span>

## <a name="overview"></a><span data-ttu-id="9f57f-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9f57f-104">Overview</span></span>

<span data-ttu-id="9f57f-105">Ce didacticiel décrit toofail requis de hello étapes sur un tooitself de périphérique physique StorSimple 8000 series s’il existe un reprise après sinistre.</span><span class="sxs-lookup"><span data-stu-id="9f57f-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooitself if there is a disaster.</span></span> <span data-ttu-id="9f57f-106">StorSimple utilise des données hello périphérique basculement fonctionnalité toomigrate à partir d’un périphérique physique source dans l’unité physique du tooanother hello centre de données.</span><span class="sxs-lookup"><span data-stu-id="9f57f-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooanother physical device.</span></span> <span data-ttu-id="9f57f-107">instructions de Hello dans ce didacticiel s’appliquent à des périphériques physiques série tooStorSimple 8000 exécutant des versions de logiciel mise à jour 3 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="9f57f-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="9f57f-108">toolearn en savoir plus sur le basculement de l’appareil et comment il est utilisé toorecover d’urgence, consultez trop[basculement et récupération d’urgence pour les unités StorSimple 8000 series](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="9f57f-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="9f57f-109">toofail sur un périphérique physique tooanother du périphérique physique, allez trop[basculer toohello même appareil physique StorSimple](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="9f57f-109">toofail over a physical device tooanother physical device, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="9f57f-110">toofail sur un tooa de périphérique physique StorSimple StorSimple Appliance du Cloud, passez trop[basculer tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span><span class="sxs-lookup"><span data-stu-id="9f57f-110">toofail over a StorSimple physical device tooa StorSimple Cloud Appliance, go too[Fail over tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9f57f-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9f57f-111">Prerequisites</span></span>

- <span data-ttu-id="9f57f-112">Vérifiez que vous avez consulté les considérations hello pour le basculement de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="9f57f-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="9f57f-113">Pour plus d’informations, consultez trop[considérations courantes pour le basculement de l’appareil](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="9f57f-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-toofail-over-toohello-same-device"></a><span data-ttu-id="9f57f-114">Toofail étapes sur toohello même appareil</span><span class="sxs-lookup"><span data-stu-id="9f57f-114">Steps toofail over toohello same device</span></span>

<span data-ttu-id="9f57f-115">Effectuer hello comme suit si vous avez besoin de toofail sur toohello même appareil.</span><span class="sxs-lookup"><span data-stu-id="9f57f-115">Perform hello following steps if you need toofail over toohello same device.</span></span>

1. <span data-ttu-id="9f57f-116">Prendre des instantanés de cloud de tous les volumes hello dans votre appareil.</span><span class="sxs-lookup"><span data-stu-id="9f57f-116">Take cloud snapshots of all hello volumes in your device.</span></span> <span data-ttu-id="9f57f-117">Pour plus d’informations, consultez trop[sauvegardes toocreate du service Gestionnaire de périphériques StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="9f57f-117">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="9f57f-118">Réinitialiser votre toofactory d’appareil.</span><span class="sxs-lookup"><span data-stu-id="9f57f-118">Reset your device toofactory defaults.</span></span> <span data-ttu-id="9f57f-119">Suivez hello des instructions dans [comment tooreset un toofactory de périphérique StorSimple les paramètres par défaut](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="9f57f-119">Follow hello detailed instructions in [how tooreset a StorSimple device toofactory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="9f57f-120">Atteindre le service du Gestionnaire de périphériques StorSimple toohello, puis sélectionnez **périphériques**.</span><span class="sxs-lookup"><span data-stu-id="9f57f-120">Go toohello StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="9f57f-121">Bonjour **périphériques** panneau, l’ancien périphérique de hello doit apparaître comme étant **hors connexion**.</span><span class="sxs-lookup"><span data-stu-id="9f57f-121">In hello **Devices** blade, hello old device should show as **Offline**.</span></span>

    ![Appareil source hors connexion](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="9f57f-123">Configurez votre appareil et réinscrivez-le auprès de votre service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="9f57f-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="9f57f-124">Hello appareil nouvellement inscrit doit apparaître comme étant **prêt tooset des**.</span><span class="sxs-lookup"><span data-stu-id="9f57f-124">hello newly registered device should show as **Ready tooset up**.</span></span> <span data-ttu-id="9f57f-125">nom du périphérique pour le nouveau périphérique de hello Hello est hello identique à celle de l’ancien périphérique de hello ajouté, mais avec un chiffre tooindicate cet appareil hello était par défaut de réinitialisation toofactory et inscrite à nouveau.</span><span class="sxs-lookup"><span data-stu-id="9f57f-125">hello device name for hello new device is hello same as hello old device but appended with a numeral tooindicate that hello device was reset toofactory default and registered again.</span></span>

    ![APPAREIL nouvellement inscrit de prêt tooset des](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="9f57f-127">Nouvelle unité de hello, terminez l’installation de périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="9f57f-127">For hello new device, complete hello device setup.</span></span> <span data-ttu-id="9f57f-128">Pour plus d’informations, consultez trop[étape 4 : exécuter le programme d’installation minimale de l’appareil](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="9f57f-128">For more information, go too[Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="9f57f-129">Sur hello **périphériques** panneau, hello du périphérique de hello devient trop**Online**.</span><span class="sxs-lookup"><span data-stu-id="9f57f-129">On hello **Devices** blade, hello status of hello device changes too**Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9f57f-130">**Effectuer la configuration minimale hello en premier, ou la récupération d’urgence peut échouer.**</span><span class="sxs-lookup"><span data-stu-id="9f57f-130">**Complete hello minimum configuration first, or your DR may fail.**</span></span>

    ![Appareil nouvellement inscrit en ligne](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="9f57f-132">Sélectionnez périphérique ancien de hello (état hors connexion) et à partir de la barre de commandes hello, cliquez sur **basculer**.</span><span class="sxs-lookup"><span data-stu-id="9f57f-132">Select hello old device (status offline) and from hello command bar, click **Fail over**.</span></span> <span data-ttu-id="9f57f-133">Bonjour **basculer** panneau, sélectionnez l’ancien périphérique en tant que source de hello et spécifiez un appareil cible de hello comme hello les appareil nouvellement inscrit.</span><span class="sxs-lookup"><span data-stu-id="9f57f-133">In hello **Fail over** blade, select old device as hello source and specify hello target device as hello newly registered device.</span></span>

    ![Synthèse du basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="9f57f-135">Pour obtenir des instructions détaillées, voir la rubrique trop[basculer sur un périphérique physique de tooanother](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="9f57f-135">For detailed instructions, refer too[Fail over tooanother physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="9f57f-136">Un travail de restauration du périphérique est créé que vous pouvez surveiller de hello **travaux** panneau.</span><span class="sxs-lookup"><span data-stu-id="9f57f-136">A device restore job is created that you can monitor from hello **Jobs** blade.</span></span>

8. <span data-ttu-id="9f57f-137">Une fois le travail de hello terminé, accéder au nouveau périphérique de hello et accédez toohello **conteneurs de volumes** panneau.</span><span class="sxs-lookup"><span data-stu-id="9f57f-137">After hello job has successfully completed, access hello new device and navigate toohello **Volume containers** blade.</span></span> <span data-ttu-id="9f57f-138">Vérifiez que tous les conteneurs de volumes hello à partir de l’ancien périphérique de hello ont été migrés toohello nouveau périphérique.</span><span class="sxs-lookup"><span data-stu-id="9f57f-138">Verify that all hello volume containers from hello old device have migrated toohello new device.</span></span>

   ![Conteneurs de volumes migrés](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="9f57f-140">Une fois le basculement de hello terminée, vous pouvez désactiver et supprimer l’ancien périphérique de hello à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="9f57f-140">After hello failover is complete, you can deactivate and delete hello old device from hello portal.</span></span> <span data-ttu-id="9f57f-141">Sélectionnez hello ancien périphérique (hors connexion), avec le bouton droit, puis **Deactivate**.</span><span class="sxs-lookup"><span data-stu-id="9f57f-141">Select hello old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="9f57f-142">Une fois que l’appareil de hello est désactivé, état hello du périphérique de hello est mise à jour.</span><span class="sxs-lookup"><span data-stu-id="9f57f-142">After hello device is deactivated, hello status of hello device is updated.</span></span>

     ![Appareil source désactivé](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="9f57f-144">Sélectionnez hello désactivé le périphérique, avec le bouton droit et sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="9f57f-144">Select hello deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="9f57f-145">Cette opération supprime les appareils hello à partir de la liste des appareils hello.</span><span class="sxs-lookup"><span data-stu-id="9f57f-145">This deletes hello device from hello list of devices.</span></span>

    ![Appareil source supprimé](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="9f57f-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9f57f-147">Next steps</span></span>

* <span data-ttu-id="9f57f-148">Une fois que vous avez effectué un basculement, vous devrez peut-être trop[désactiver ou supprimer votre appareil StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="9f57f-148">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="9f57f-149">Pour plus d’informations sur la façon dont toouse hello StorSimple le Gestionnaire de périphériques de service, accédez trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="9f57f-149">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

