---
title: "Afficher et gérer des travaux pour la gamme StorSimple 8000 | Microsoft Docs"
description: "Décrit le panneau Travaux (jobs) du service StorSimple Device Manager et explique comment l’utiliser pour effectuer le suivi des travaux de sauvegarde planifiée, actuelle et récente."
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
ms.openlocfilehash: bf8038b7171053b75eeb9aed88bff4246e65a8a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="687ac-103">Utiliser le service StorSimple Device Manager pour afficher et gérer des travaux (Update 3 et versions ultérieures)</span><span class="sxs-lookup"><span data-stu-id="687ac-103">Use the StorSimple Device Manager service to view and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="687ac-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="687ac-104">Overview</span></span>
<span data-ttu-id="687ac-105">Le panneau **Travaux (jobs)** est un portail centralisé unique qui permet de consulter et de gérer les travaux qui ont été lancés sur les appareils connectés à votre service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="687ac-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="687ac-106">Vous pouvez consulter les tâches planifiées, en cours d'exécution, terminées, annulées et en échec pour plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="687ac-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="687ac-107">Les résultats sont présentés sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="687ac-107">Results are presented in a tabular format.</span></span>

![Panneau Tâches](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="687ac-109">Vous pouvez rechercher rapidement les tâches qui vous intéressent en filtrant sur les champs, à savoir :</span><span class="sxs-lookup"><span data-stu-id="687ac-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="687ac-110">**État** : les travaux peuvent être en cours, s’être bien déroulés, avoir échoué, avoir été annulés ou s’être bien déroulés mais avec des erreurs.</span><span class="sxs-lookup"><span data-stu-id="687ac-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="687ac-111">**Période** : les tâches peuvent être filtrées selon la date et l’heure.</span><span class="sxs-lookup"><span data-stu-id="687ac-111">**Time range** – Jobs can be filtered based on the date and time range.</span></span> <span data-ttu-id="687ac-112">Les plages sont : dernière heure, dernières 24 heures, derniers 7 jours, 30 derniers jours, année dernière ou une date personnalisée.</span><span class="sxs-lookup"><span data-stu-id="687ac-112">The ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="687ac-113">**Type** : le type de travail peut être une sauvegarde planifiée, une sauvegarde manuelle, une restauration de sauvegarde, un clonage de volume, un basculement de conteneurs de volumes, une création de volume épinglé localement, une modification de volume, une installation de mises à jour, une collecte de journaux de support et une création d’appliance cloud.</span><span class="sxs-lookup"><span data-stu-id="687ac-113">**Type** – The job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="687ac-114">**Appareils** : les tâches sont initiées sur un certain appareil connecté à votre service.</span><span class="sxs-lookup"><span data-stu-id="687ac-114">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
  
<span data-ttu-id="687ac-115">Les tâches filtrées sont ensuite affichées sous forme de tableau sur la base des attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="687ac-115">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>
  
* <span data-ttu-id="687ac-116">**Nom** : une sauvegarde planifiée, une sauvegarde manuelle, une restauration de sauvegarde, un clonage de volume, un basculement de conteneurs de volumes, une création de volume épinglé localement, une modification de volume, une installation de mises à jour, une collecte de journaux de support ou une création d’appliance cloud.</span><span class="sxs-lookup"><span data-stu-id="687ac-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="687ac-117">**État** : en cours d'exécution, terminées, annulées, en échec, en cours d'annulation ou terminées avec des erreurs.</span><span class="sxs-lookup"><span data-stu-id="687ac-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="687ac-118">**Entité** : les tâches peuvent être associées à un volume, une stratégie de sauvegarde ou un appareil.</span><span class="sxs-lookup"><span data-stu-id="687ac-118">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="687ac-119">Par exemple, une tâche de clonage est associée à un volume, tandis qu'une tâche de sauvegarde planifiée est associée à une stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="687ac-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="687ac-120">Une tâche d’appareil est créée à la suite d’une récupération d'urgence ou d’une opération de restauration.</span><span class="sxs-lookup"><span data-stu-id="687ac-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="687ac-121">**Appareil** : nom de l'appareil sur lequel la tâche a été lancée.</span><span class="sxs-lookup"><span data-stu-id="687ac-121">**Device** – The name of the device on which the job was started.</span></span>
* <span data-ttu-id="687ac-122">**Démarré le** : heure à laquelle la tâche a été lancée.</span><span class="sxs-lookup"><span data-stu-id="687ac-122">**Started on** – The time when the job was started.</span></span>
* <span data-ttu-id="687ac-123">**Durée** : le temps nécessaire pour terminer le travail.</span><span class="sxs-lookup"><span data-stu-id="687ac-123">**Duration** – The time required to complete the job.</span></span>

<span data-ttu-id="687ac-124">La liste des tâches est actualisée toutes les 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="687ac-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="687ac-125">Cette page vous permet d’effectuer diverses actions liées aux tâches, à savoir :</span><span class="sxs-lookup"><span data-stu-id="687ac-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="687ac-126">Affichage des détails d’une tâche</span><span class="sxs-lookup"><span data-stu-id="687ac-126">View job details</span></span>
* <span data-ttu-id="687ac-127">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="687ac-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="687ac-128">Affichage des détails d’une tâche</span><span class="sxs-lookup"><span data-stu-id="687ac-128">View job details</span></span>
<span data-ttu-id="687ac-129">Pour afficher les détails d’une tâche, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="687ac-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="687ac-130">Pour afficher les détails d’une tâche</span><span class="sxs-lookup"><span data-stu-id="687ac-130">To view job details</span></span>
1. <span data-ttu-id="687ac-131">Accédez à votre service StorSimple Device Manager et cliquez sur **Travaux (jobs)**.</span><span class="sxs-lookup"><span data-stu-id="687ac-131">Go to your StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="687ac-132">Dans le panneau **Travaux (jobs)**, affichez les travaux qui vous intéressent en exécutant une requête avec les filtres appropriés.</span><span class="sxs-lookup"><span data-stu-id="687ac-132">In the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="687ac-133">Vous pouvez rechercher des tâches terminées, en cours d'exécution ou annulées.</span><span class="sxs-lookup"><span data-stu-id="687ac-133">You can search for completed, running, or canceled jobs.</span></span>

    ![Panneau Tâches](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="687ac-135">Sélectionnez un travail et cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="687ac-135">Select and click a job.</span></span>

    ![Panneau Tâches](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="687ac-137">Dans le panneau des détails du travail, vous pouvez consulter l’état, les détails, les statistiques temporelles et les statistiques de données.</span><span class="sxs-lookup"><span data-stu-id="687ac-137">In the job details blade, you can view the status, details, time statistics, and data statistics.</span></span>
   
    ![Détails du travail](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="687ac-139">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="687ac-139">Cancel a job</span></span>
<span data-ttu-id="687ac-140">Pour annuler une tâche en cours d’exécution, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="687ac-140">Perform the following steps to cancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="687ac-141">Certaines tâches, telles que la modification d'un volume pour modifier le type de volume ou l'extension d'un volume, ne peuvent pas être annulées.</span><span class="sxs-lookup"><span data-stu-id="687ac-141">Some jobs, such as modifying a volume to change the volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="to-cancel-a-job"></a><span data-ttu-id="687ac-142">Pour annuler une tâche</span><span class="sxs-lookup"><span data-stu-id="687ac-142">To cancel a job</span></span>
1. <span data-ttu-id="687ac-143">Dans la page **Tâches** , affichez les tâches en cours d’exécution que vous voulez annuler en exécutant une requête avec les filtres appropriés.</span><span class="sxs-lookup"><span data-stu-id="687ac-143">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span> <span data-ttu-id="687ac-144">Sélectionnez la tâche.</span><span class="sxs-lookup"><span data-stu-id="687ac-144">Select the job.</span></span>

2. <span data-ttu-id="687ac-145">Cliquez avec le bouton droit sur le travail sélectionné pour appeler le menu contextuel, puis cliquez sur **Annuler**.</span><span class="sxs-lookup"><span data-stu-id="687ac-145">Right-click on the selected job to invoke the context menu and click **Cancel**.</span></span>

    ![Détails du travail](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="687ac-147">Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="687ac-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="687ac-148">Cette tâche est à présent annulée.</span><span class="sxs-lookup"><span data-stu-id="687ac-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="687ac-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="687ac-149">Next steps</span></span>
* <span data-ttu-id="687ac-150">En savoir plus sur la [gestion de vos stratégies de sauvegarde StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="687ac-150">Learn how to [manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="687ac-151">Découvrez comment [utiliser le service StorSimple Device Manager pour gérer votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="687ac-151">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

