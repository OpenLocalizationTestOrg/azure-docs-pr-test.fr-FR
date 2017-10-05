---
title: "Affichage et gestion des tâches StorSimple | Microsoft Docs"
description: "Décrit la page Tâches du service StorSimple Manager et explique comment l’utiliser pour effectuer le suivi des tâches de sauvegarde planifiées, actuelles et récentes."
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
ms.openlocfilehash: 6df1b27ce76de7a781ecc40af8430114d80b20d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-view-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="0488a-103">Utilisez le service StorSimple Manager pour afficher et gérer les tâches StorSimple (Mise à jour 2)</span><span class="sxs-lookup"><span data-stu-id="0488a-103">Use the StorSimple Manager service to view and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="0488a-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0488a-104">Overview</span></span>
<span data-ttu-id="0488a-105">La page **Tâches** est un portail centralisé unique qui permet de consulter et de gérer les tâches qui ont été lancées sur les appareils connectés à votre service StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="0488a-105">The **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Manager service.</span></span> <span data-ttu-id="0488a-106">Vous pouvez consulter les tâches planifiées, en cours d'exécution, terminées, annulées et en échec pour plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="0488a-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="0488a-107">Les résultats sont présentés sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="0488a-107">Results are presented in a tabular format.</span></span> 

![Page Tâches](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="0488a-109">Vous pouvez rechercher rapidement les tâches qui vous intéressent en filtrant sur les champs, à savoir :</span><span class="sxs-lookup"><span data-stu-id="0488a-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="0488a-110">**État** : les tâches peuvent être en cours d'exécution, terminées, annulées, en échec, en cours d'annulation ou terminées avec des erreurs.</span><span class="sxs-lookup"><span data-stu-id="0488a-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="0488a-111">**De et À** : les tâches peuvent être filtrées selon la date et l'heure.</span><span class="sxs-lookup"><span data-stu-id="0488a-111">**From and To** – Jobs can be filtered based on the date and time range.</span></span>
* <span data-ttu-id="0488a-112">**Type** : le type de tâche peut être sauvegarde, sauvegarde manuelle, restauration, clonage, basculement d'appareil, créer un volume épinglé localement, modifier le volume, mettre à jour, prendre en charge le package ou approvisionnement de l'appareil virtuel.</span><span class="sxs-lookup"><span data-stu-id="0488a-112">**Type** – The job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="0488a-113">**Appareils** : les tâches sont initiées sur un certain appareil connecté à votre service.</span><span class="sxs-lookup"><span data-stu-id="0488a-113">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
  <span data-ttu-id="0488a-114">Les tâches filtrées sont ensuite affichées sous forme de tableau sur la base des attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="0488a-114">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>
  
  * <span data-ttu-id="0488a-115">**Type** : sauvegarde, sauvegarde manuelle, restauration, clonage, basculement d'appareil, créer un volume épinglé localement, modifier le volume, mettre à jour, prendre en charge le package ou approvisionnement de l'appareil virtuel.</span><span class="sxs-lookup"><span data-stu-id="0488a-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="0488a-116">**État** : en cours d'exécution, terminées, annulées, en échec, en cours d'annulation ou terminées avec des erreurs.</span><span class="sxs-lookup"><span data-stu-id="0488a-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="0488a-117">**Entité** : les tâches peuvent être associées à un volume, une stratégie de sauvegarde ou un appareil.</span><span class="sxs-lookup"><span data-stu-id="0488a-117">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="0488a-118">Par exemple, une tâche de clonage est associée à un volume, tandis qu'une tâche de sauvegarde planifiée est associée à une stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="0488a-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="0488a-119">Une tâche d’appareil est créée à la suite d’une récupération d'urgence ou d’une opération de restauration.</span><span class="sxs-lookup"><span data-stu-id="0488a-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="0488a-120">**Appareil** : nom de l'appareil sur lequel la tâche a été lancée.</span><span class="sxs-lookup"><span data-stu-id="0488a-120">**Device** – The name of the device on which the job was started.</span></span>
  * <span data-ttu-id="0488a-121">**Démarré le** : heure à laquelle la tâche a été lancée.</span><span class="sxs-lookup"><span data-stu-id="0488a-121">**Started on** – The time when the job was started.</span></span>
  * <span data-ttu-id="0488a-122">**Progression** : pourcentage d'achèvement d'une tâche en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="0488a-122">**Progress** – The percentage completion of a running job.</span></span> <span data-ttu-id="0488a-123">Pour une tâche terminée, le pourcentage doit toujours être de 100 %.</span><span class="sxs-lookup"><span data-stu-id="0488a-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="0488a-124">La liste des tâches est actualisée toutes les 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="0488a-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="0488a-125">Cette page vous permet d’effectuer diverses actions liées aux tâches, à savoir :</span><span class="sxs-lookup"><span data-stu-id="0488a-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="0488a-126">Affichage des détails d’une tâche</span><span class="sxs-lookup"><span data-stu-id="0488a-126">View job details</span></span>
* <span data-ttu-id="0488a-127">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="0488a-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="0488a-128">Affichage des détails d’une tâche</span><span class="sxs-lookup"><span data-stu-id="0488a-128">View job details</span></span>
<span data-ttu-id="0488a-129">Pour afficher les détails d’une tâche, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="0488a-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="0488a-130">Pour afficher les détails d’une tâche</span><span class="sxs-lookup"><span data-stu-id="0488a-130">To view job details</span></span>
1. <span data-ttu-id="0488a-131">Dans la page **Tâches** , affichez la ou les tâches qui vous intéressent en exécutant une requête avec les filtres appropriés.</span><span class="sxs-lookup"><span data-stu-id="0488a-131">On the **Jobs** page, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="0488a-132">Vous pouvez rechercher des tâches terminées, en cours d'exécution ou annulées.</span><span class="sxs-lookup"><span data-stu-id="0488a-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="0488a-133">Sélectionnez une tâche.</span><span class="sxs-lookup"><span data-stu-id="0488a-133">Select a job.</span></span>
3. <span data-ttu-id="0488a-134">En bas de la page, cliquez sur **Détails**.</span><span class="sxs-lookup"><span data-stu-id="0488a-134">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="0488a-135">Dans la boîte de dialogue **Détails de la tâche de sauvegarde** , vous pouvez consulter l'état, les détails, les statistiques temporelles et les statistiques de données.</span><span class="sxs-lookup"><span data-stu-id="0488a-135">In the **Backup Job Details** dialog box, you can view the status, details, time statistics, and data statistics.</span></span>
   
    ![Page Détails de la tâche](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="0488a-137">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="0488a-137">Cancel a job</span></span>
<span data-ttu-id="0488a-138">Pour annuler une tâche en cours d’exécution, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="0488a-138">Perform the following steps to cancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="0488a-139">Certaines tâches, telles que la modification d'un volume pour modifier le type de volume ou l'extension d'un volume, ne peuvent pas être annulées.</span><span class="sxs-lookup"><span data-stu-id="0488a-139">Some jobs, such as modifying a volume to change the volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="to-cancel-a-job"></a><span data-ttu-id="0488a-140">Pour annuler une tâche</span><span class="sxs-lookup"><span data-stu-id="0488a-140">To cancel a job</span></span>
1. <span data-ttu-id="0488a-141">Dans la page **Tâches** , affichez les tâches en cours d’exécution que vous voulez annuler en exécutant une requête avec les filtres appropriés.</span><span class="sxs-lookup"><span data-stu-id="0488a-141">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="0488a-142">Sélectionnez la tâche.</span><span class="sxs-lookup"><span data-stu-id="0488a-142">Select the job.</span></span>
3. <span data-ttu-id="0488a-143">En bas de la page, cliquez sur **Annuler**.</span><span class="sxs-lookup"><span data-stu-id="0488a-143">At the bottom of the page, click **Cancel**.</span></span>
4. <span data-ttu-id="0488a-144">Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="0488a-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="0488a-145">Cette tâche est à présent annulée.</span><span class="sxs-lookup"><span data-stu-id="0488a-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0488a-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0488a-146">Next steps</span></span>
* <span data-ttu-id="0488a-147">En savoir plus sur la [gestion de vos stratégies de sauvegarde StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="0488a-147">Learn how to [manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="0488a-148">Découvrez comment [utiliser le service StorSimple Manager pour gérer votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="0488a-148">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

