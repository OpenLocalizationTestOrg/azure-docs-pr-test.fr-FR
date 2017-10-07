---
title: "aaaView et gérer des tâches de StorSimple | Documents Microsoft"
description: "Décrit la page de travaux du service Gestionnaire StorSimple hello et comment toouse il tootrack récente, en cours et planifiées travaux de sauvegarde."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="46a0d-103">Utilisez hello StorSimple Manager service tooview et gérer des travaux de StorSimple (Update 2)</span><span class="sxs-lookup"><span data-stu-id="46a0d-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="46a0d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="46a0d-104">Overview</span></span>
<span data-ttu-id="46a0d-105">Hello **travaux** page fournit un portail centralisé unique pour l’affichage et la gestion des travaux qui ont été démarrées sur les périphériques connectés tooyour le service StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="46a0d-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="46a0d-106">Vous pouvez consulter les tâches planifiées, en cours d'exécution, terminées, annulées et en échec pour plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="46a0d-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="46a0d-107">Les résultats sont présentés sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="46a0d-107">Results are presented in a tabular format.</span></span> 

![Page Tâches](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="46a0d-109">Vous pouvez rechercher rapidement les travaux qui hello que vous intéressent en filtrant sur des champs tels que :</span><span class="sxs-lookup"><span data-stu-id="46a0d-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="46a0d-110">**État** : les tâches peuvent être en cours d'exécution, terminées, annulées, en échec, en cours d'annulation ou terminées avec des erreurs.</span><span class="sxs-lookup"><span data-stu-id="46a0d-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="46a0d-111">**Depuis et vers** – travaux peuvent être filtrées hello en fonction de date et la plage horaire.</span><span class="sxs-lookup"><span data-stu-id="46a0d-111">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="46a0d-112">**Type** – type de tâche hello peut être une sauvegarde, une sauvegarde manuelle, restauration, clone, basculement de l’appareil, créer un volume attaché localement, modifier le volume, mettez à jour, prennent en charge le package ou la configuration de périphérique virtuel.</span><span class="sxs-lookup"><span data-stu-id="46a0d-112">**Type** – hello job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="46a0d-113">**Appareils** – travaux sont initiés sur un certain service tooyour de périphérique connecté.</span><span class="sxs-lookup"><span data-stu-id="46a0d-113">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  <span data-ttu-id="46a0d-114">Hello travaux filtrés est ensuite sous forme de tableau sur la base de hello de hello suivant d’attributs :</span><span class="sxs-lookup"><span data-stu-id="46a0d-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
  * <span data-ttu-id="46a0d-115">**Type** : sauvegarde, sauvegarde manuelle, restauration, clonage, basculement d'appareil, créer un volume épinglé localement, modifier le volume, mettre à jour, prendre en charge le package ou approvisionnement de l'appareil virtuel.</span><span class="sxs-lookup"><span data-stu-id="46a0d-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="46a0d-116">**État** : en cours d'exécution, terminées, annulées, en échec, en cours d'annulation ou terminées avec des erreurs.</span><span class="sxs-lookup"><span data-stu-id="46a0d-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="46a0d-117">**Entité** – les travaux hello peuvent être associés à un volume, une stratégie de sauvegarde ou un périphérique.</span><span class="sxs-lookup"><span data-stu-id="46a0d-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="46a0d-118">Par exemple, une tâche de clonage est associée à un volume, tandis qu'une tâche de sauvegarde planifiée est associée à une stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="46a0d-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="46a0d-119">Une tâche d’appareil est créée à la suite d’une récupération d'urgence ou d’une opération de restauration.</span><span class="sxs-lookup"><span data-stu-id="46a0d-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="46a0d-120">**APPAREIL** hello – nom de l’appareil hello sur quel hello travail a été démarré.</span><span class="sxs-lookup"><span data-stu-id="46a0d-120">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="46a0d-121">**Démarré sur** – heure hello auxquelles hello travail a démarré.</span><span class="sxs-lookup"><span data-stu-id="46a0d-121">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="46a0d-122">**Progression** – hello pourcentage de réalisation d’une tâche en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="46a0d-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="46a0d-123">Pour une tâche terminée, le pourcentage doit toujours être de 100 %.</span><span class="sxs-lookup"><span data-stu-id="46a0d-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="46a0d-124">Hello de la liste des travaux est actualisée toutes les 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="46a0d-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="46a0d-125">Vous pouvez effectuer hello suivant d’actions relatives à la tâche sur cette page :</span><span class="sxs-lookup"><span data-stu-id="46a0d-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="46a0d-126">Affichage des détails d’une tâche</span><span class="sxs-lookup"><span data-stu-id="46a0d-126">View job details</span></span>
* <span data-ttu-id="46a0d-127">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="46a0d-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="46a0d-128">Affichage des détails d’une tâche</span><span class="sxs-lookup"><span data-stu-id="46a0d-128">View job details</span></span>
<span data-ttu-id="46a0d-129">Effectuer hello suivant détaille de hello tooview étapes d’un travail.</span><span class="sxs-lookup"><span data-stu-id="46a0d-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="46a0d-130">Détails de la tâche tooview</span><span class="sxs-lookup"><span data-stu-id="46a0d-130">tooview job details</span></span>
1. <span data-ttu-id="46a0d-131">Sur hello **travaux** page, affichez ou les travaux hello vous intéressent en exécutant une requête avec les filtres appropriés.</span><span class="sxs-lookup"><span data-stu-id="46a0d-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="46a0d-132">Vous pouvez rechercher des tâches terminées, en cours d'exécution ou annulées.</span><span class="sxs-lookup"><span data-stu-id="46a0d-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="46a0d-133">Sélectionnez une tâche.</span><span class="sxs-lookup"><span data-stu-id="46a0d-133">Select a job.</span></span>
3. <span data-ttu-id="46a0d-134">Au bas de hello de page de hello, cliquez sur **détails**.</span><span class="sxs-lookup"><span data-stu-id="46a0d-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="46a0d-135">Bonjour **détails de la tâche sauvegarde** boîte de dialogue, vous pouvez afficher le statut de hello, détails, les statistiques de temps et les statistiques de données.</span><span class="sxs-lookup"><span data-stu-id="46a0d-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![Page Détails de la tâche](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="46a0d-137">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="46a0d-137">Cancel a job</span></span>
<span data-ttu-id="46a0d-138">Effectuer hello suivant les étapes toocancel un travail en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="46a0d-138">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="46a0d-139">Certaines tâches, telles que la modification d’un type de volume volume toochange hello ou étendre un volume, ne peut pas être annulées.</span><span class="sxs-lookup"><span data-stu-id="46a0d-139">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="toocancel-a-job"></a><span data-ttu-id="46a0d-140">toocancel un travail</span><span class="sxs-lookup"><span data-stu-id="46a0d-140">toocancel a job</span></span>
1. <span data-ttu-id="46a0d-141">Sur hello **travaux** page, affichez ou les travaux en cours d’exécution hello que vous souhaitez toocancel en exécutant une requête avec les filtres appropriés.</span><span class="sxs-lookup"><span data-stu-id="46a0d-141">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="46a0d-142">Sélectionnez le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="46a0d-142">Select hello job.</span></span>
3. <span data-ttu-id="46a0d-143">Au bas de hello de page de hello, cliquez sur **Annuler**.</span><span class="sxs-lookup"><span data-stu-id="46a0d-143">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="46a0d-144">Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="46a0d-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="46a0d-145">Cette tâche est à présent annulée.</span><span class="sxs-lookup"><span data-stu-id="46a0d-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46a0d-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="46a0d-146">Next steps</span></span>
* <span data-ttu-id="46a0d-147">Découvrez comment trop[gérer vos stratégies de sauvegarde StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="46a0d-147">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="46a0d-148">Découvrez comment trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="46a0d-148">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

