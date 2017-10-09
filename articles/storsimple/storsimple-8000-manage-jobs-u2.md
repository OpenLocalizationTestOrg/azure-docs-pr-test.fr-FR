---
title: "aaaView et gérer des tâches pour la série StorSimple 8000 | Documents Microsoft"
description: "Décrit le panneau de travaux de service de gestionnaire de périphériques StorSimple hello et comment toouse il tootrack récente, en cours et planifiées travaux de sauvegarde."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="20b1a-103">Utilisez tooview de service de gestionnaire de périphériques StorSimple hello et gérer des tâches (Update 3 et versions ultérieur)</span><span class="sxs-lookup"><span data-stu-id="20b1a-103">Use hello StorSimple Device Manager service tooview and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="20b1a-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="20b1a-104">Overview</span></span>
<span data-ttu-id="20b1a-105">Hello **travaux** panneau fournit un portail centralisé unique pour l’affichage et la gestion des travaux qui ont été démarrées sur les périphériques connectés tooyour le Gestionnaire de périphériques StorSimple service.</span><span class="sxs-lookup"><span data-stu-id="20b1a-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="20b1a-106">Vous pouvez consulter les tâches planifiées, en cours d'exécution, terminées, annulées et en échec pour plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="20b1a-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="20b1a-107">Les résultats sont présentés sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="20b1a-107">Results are presented in a tabular format.</span></span>

![Panneau Tâches](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="20b1a-109">Vous pouvez rechercher rapidement les travaux qui hello que vous intéressent en filtrant sur des champs tels que :</span><span class="sxs-lookup"><span data-stu-id="20b1a-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="20b1a-110">**État** : les travaux peuvent être en cours, s’être bien déroulés, avoir échoué, avoir été annulés ou s’être bien déroulés mais avec des erreurs.</span><span class="sxs-lookup"><span data-stu-id="20b1a-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="20b1a-111">**Intervalle de temps** – travaux peuvent être filtrées hello en fonction de date et la plage horaire.</span><span class="sxs-lookup"><span data-stu-id="20b1a-111">**Time range** – Jobs can be filtered based on hello date and time range.</span></span> <span data-ttu-id="20b1a-112">les plages de Hello sont après 1 heure, dernières 24 heures, 7 derniers jours, 30 derniers jours, année ou dates personnalisée.</span><span class="sxs-lookup"><span data-stu-id="20b1a-112">hello ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="20b1a-113">**Type** – type de tâche hello peut être sauvegarde planifiée, de sauvegarde manuelle, de restauration de sauvegarde, cloner le volume, basculer les conteneurs de volumes, créer le volume attaché localement, modifier le volume, installer les mises à jour, collecter des journaux de prise en charge et créer le dispositif de cloud.</span><span class="sxs-lookup"><span data-stu-id="20b1a-113">**Type** – hello job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="20b1a-114">**Appareils** – travaux sont initiés sur un certain service tooyour de périphérique connecté.</span><span class="sxs-lookup"><span data-stu-id="20b1a-114">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  
<span data-ttu-id="20b1a-115">Hello travaux filtrés est ensuite sous forme de tableau sur la base de hello de hello suivant d’attributs :</span><span class="sxs-lookup"><span data-stu-id="20b1a-115">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
* <span data-ttu-id="20b1a-116">**Nom** : une sauvegarde planifiée, une sauvegarde manuelle, une restauration de sauvegarde, un clonage de volume, un basculement de conteneurs de volumes, une création de volume épinglé localement, une modification de volume, une installation de mises à jour, une collecte de journaux de support ou une création d’appliance cloud.</span><span class="sxs-lookup"><span data-stu-id="20b1a-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="20b1a-117">**État** : en cours d'exécution, terminées, annulées, en échec, en cours d'annulation ou terminées avec des erreurs.</span><span class="sxs-lookup"><span data-stu-id="20b1a-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="20b1a-118">**Entité** – les travaux hello peuvent être associés à un volume, une stratégie de sauvegarde ou un périphérique.</span><span class="sxs-lookup"><span data-stu-id="20b1a-118">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="20b1a-119">Par exemple, une tâche de clonage est associée à un volume, tandis qu'une tâche de sauvegarde planifiée est associée à une stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="20b1a-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="20b1a-120">Une tâche d’appareil est créée à la suite d’une récupération d'urgence ou d’une opération de restauration.</span><span class="sxs-lookup"><span data-stu-id="20b1a-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="20b1a-121">**APPAREIL** hello – nom de l’appareil hello sur quel hello travail a été démarré.</span><span class="sxs-lookup"><span data-stu-id="20b1a-121">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="20b1a-122">**Démarré sur** – heure hello auxquelles hello travail a démarré.</span><span class="sxs-lookup"><span data-stu-id="20b1a-122">**Started on** – hello time when hello job was started.</span></span>
* <span data-ttu-id="20b1a-123">**Durée** – hello temps requis toocomplete hello tâche.</span><span class="sxs-lookup"><span data-stu-id="20b1a-123">**Duration** – hello time required toocomplete hello job.</span></span>

<span data-ttu-id="20b1a-124">Hello de la liste des travaux est actualisée toutes les 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="20b1a-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="20b1a-125">Vous pouvez effectuer hello suivant d’actions relatives à la tâche sur cette page :</span><span class="sxs-lookup"><span data-stu-id="20b1a-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="20b1a-126">Affichage des détails d’une tâche</span><span class="sxs-lookup"><span data-stu-id="20b1a-126">View job details</span></span>
* <span data-ttu-id="20b1a-127">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="20b1a-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="20b1a-128">Affichage des détails d’une tâche</span><span class="sxs-lookup"><span data-stu-id="20b1a-128">View job details</span></span>
<span data-ttu-id="20b1a-129">Effectuer hello suivant détaille de hello tooview étapes d’un travail.</span><span class="sxs-lookup"><span data-stu-id="20b1a-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="20b1a-130">Détails de la tâche tooview</span><span class="sxs-lookup"><span data-stu-id="20b1a-130">tooview job details</span></span>
1. <span data-ttu-id="20b1a-131">Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, puis cliquez sur **travaux**.</span><span class="sxs-lookup"><span data-stu-id="20b1a-131">Go tooyour StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="20b1a-132">Bonjour **travaux** panneau, une ou plusieurs tâches hello affichage vous intéressent en exécutant une requête avec les filtres appropriés.</span><span class="sxs-lookup"><span data-stu-id="20b1a-132">In hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="20b1a-133">Vous pouvez rechercher des tâches terminées, en cours d'exécution ou annulées.</span><span class="sxs-lookup"><span data-stu-id="20b1a-133">You can search for completed, running, or canceled jobs.</span></span>

    ![Panneau Tâches](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="20b1a-135">Sélectionnez un travail et cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="20b1a-135">Select and click a job.</span></span>

    ![Panneau Tâches](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="20b1a-137">Dans le panneau de détails du travail hello, vous pouvez afficher hello état, détails, les statistiques de temps et les données statistiques.</span><span class="sxs-lookup"><span data-stu-id="20b1a-137">In hello job details blade, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![Détails du travail](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="20b1a-139">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="20b1a-139">Cancel a job</span></span>
<span data-ttu-id="20b1a-140">Effectuer hello suivant les étapes toocancel un travail en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="20b1a-140">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="20b1a-141">Certaines tâches, telles que la modification d’un type de volume volume toochange hello ou étendre un volume, ne peut pas être annulées.</span><span class="sxs-lookup"><span data-stu-id="20b1a-141">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="toocancel-a-job"></a><span data-ttu-id="20b1a-142">toocancel un travail</span><span class="sxs-lookup"><span data-stu-id="20b1a-142">toocancel a job</span></span>
1. <span data-ttu-id="20b1a-143">Sur hello **travaux** page, affichez ou les travaux en cours d’exécution hello que vous souhaitez toocancel en exécutant une requête avec les filtres appropriés.</span><span class="sxs-lookup"><span data-stu-id="20b1a-143">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span> <span data-ttu-id="20b1a-144">Sélectionnez le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="20b1a-144">Select hello job.</span></span>

2. <span data-ttu-id="20b1a-145">Avec le bouton droit dans le menu contextuel hello hello travail sélectionné tooinvoke et cliquez sur **Annuler**.</span><span class="sxs-lookup"><span data-stu-id="20b1a-145">Right-click on hello selected job tooinvoke hello context menu and click **Cancel**.</span></span>

    ![Détails du travail](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="20b1a-147">Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="20b1a-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="20b1a-148">Cette tâche est à présent annulée.</span><span class="sxs-lookup"><span data-stu-id="20b1a-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20b1a-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="20b1a-149">Next steps</span></span>
* <span data-ttu-id="20b1a-150">Découvrez comment trop[gérer vos stratégies de sauvegarde StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="20b1a-150">Learn how too[manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="20b1a-151">Découvrez comment trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="20b1a-151">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

