---
title: "les travaux de sauvegarde de gestionnaire d’instantanés aaaStorSimple | Documents Microsoft"
description: "Décrit comment toouse hello StorSimple Snapshot Manager MMC enfichable tooview et gérer des travaux de sauvegarde planifiées, en cours d’exécution et terminées."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a><span data-ttu-id="ce61e-103">Utilisez le Gestionnaire d’instantanés StorSimple tooview et gérer des travaux de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="ce61e-103">Use StorSimple Snapshot Manager tooview and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="ce61e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ce61e-104">Overview</span></span>
<span data-ttu-id="ce61e-105">Hello **travaux** nœud Bonjour **étendue** volet affiche hello **planifiée**, **dernières 24 heures**, et **en cours d’exécution**les tâches que vous avez lancées de façon interactive ou par une stratégie configurée de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="ce61e-105">hello **Jobs** node in hello **Scope** pane shows hello **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="ce61e-106">Ce didacticiel explique comment vous pouvez utiliser hello **travaux** informations sur les nœuds toodisplay sur les travaux de sauvegarde planifiées, récentes et en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ce61e-106">This tutorial explains how you can use hello **Jobs** node toodisplay information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="ce61e-107">(hello la liste des tâches et les informations correspondantes s’affiche dans hello **résultats** volet.) Vous pouvez également cliquer avec le bouton droit sur une tâche répertoriée et afficher un menu contextuel présentant les actions disponibles.</span><span class="sxs-lookup"><span data-stu-id="ce61e-107">(hello list of jobs and corresponding information appears in hello **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="ce61e-108">Afficher les tâches planifiées</span><span class="sxs-lookup"><span data-stu-id="ce61e-108">View scheduled jobs</span></span>
<span data-ttu-id="ce61e-109">Hello utilisation suivant la procédure tooview des travaux de sauvegarde planifiés.</span><span class="sxs-lookup"><span data-stu-id="ce61e-109">Use hello following procedure tooview scheduled backup jobs.</span></span>

#### <a name="tooview-scheduled-jobs"></a><span data-ttu-id="ce61e-110">travaux de tooview planifié</span><span class="sxs-lookup"><span data-stu-id="ce61e-110">tooview scheduled jobs</span></span>
1. <span data-ttu-id="ce61e-111">Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ce61e-111">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="ce61e-112">Bonjour **étendue** volet, développez hello **travaux** nœud, puis cliquez sur **planifiée**.</span><span class="sxs-lookup"><span data-stu-id="ce61e-112">In hello **Scope** pane, expand hello **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="ce61e-113">Hello informations suivantes s’affichent dans hello **résultats** volet :</span><span class="sxs-lookup"><span data-stu-id="ce61e-113">hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="ce61e-114">**Nom** hello – nom de l’instantané programmé de hello</span><span class="sxs-lookup"><span data-stu-id="ce61e-114">**Name** – hello name of hello scheduled snapshot</span></span>
   * <span data-ttu-id="ce61e-115">**Prochaine exécution** : hello date et heure de capture instantanée planifiée suivante, hello</span><span class="sxs-lookup"><span data-stu-id="ce61e-115">**Next Run** – hello date and time of hello next scheduled snapshot</span></span>
   * <span data-ttu-id="ce61e-116">**La dernière exécution** : hello date et heure d’instantané hello planifiée le plus récent</span><span class="sxs-lookup"><span data-stu-id="ce61e-116">**Last Run** – hello date and time of hello most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="ce61e-117">Pour les instantanés uniquement à usage unique, hello **prochaine exécution** et **dernière exécution** sera même hello.</span><span class="sxs-lookup"><span data-stu-id="ce61e-117">For one-time only snapshots, hello **Next Run** and **Last Run** will be hello same.</span></span>
     
     ![Tâches de sauvegarde planifiées](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="ce61e-119">tooperform des actions supplémentaires sur une tâche spécifique, cliquez sur le nom de travail de hello Bonjour **résultats** volet et sélectionnez des options de menu hello.</span><span class="sxs-lookup"><span data-stu-id="ce61e-119">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="ce61e-120">Afficher les tâches récentes</span><span class="sxs-lookup"><span data-stu-id="ce61e-120">View recent jobs</span></span>
<span data-ttu-id="ce61e-121">Utilisez hello après procédure tooview sauvegarde et restauration des travaux qui ont été effectués dans hello des dernières 24 heures.</span><span class="sxs-lookup"><span data-stu-id="ce61e-121">Use hello following procedure tooview backup and restore jobs that were completed in hello last 24 hours.</span></span>

#### <a name="tooview-recent-jobs"></a><span data-ttu-id="ce61e-122">travaux récents tooview</span><span class="sxs-lookup"><span data-stu-id="ce61e-122">tooview recent jobs</span></span>
1. <span data-ttu-id="ce61e-123">Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ce61e-123">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="ce61e-124">Bonjour **étendue** volet, développez hello **travaux** nœud, puis cliquez sur **dernières 24 heures**.</span><span class="sxs-lookup"><span data-stu-id="ce61e-124">In hello **Scope** pane, expand hello **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="ce61e-125">Hello **résultats** volet affiche les tâches de sauvegarde pour hello des dernières 24 heures (maximum tooa 64 travaux).</span><span class="sxs-lookup"><span data-stu-id="ce61e-125">hello **Results** pane shows backup jobs for hello last 24 hours (tooa maximum of 64 jobs).</span></span> <span data-ttu-id="ce61e-126">Hello informations suivantes s’affichent dans hello **résultats** volet, en fonction de hello **vue** options que vous spécifiez :</span><span class="sxs-lookup"><span data-stu-id="ce61e-126">hello following information appears in hello **Results** pane, depending on hello **View** options you specify:</span></span>
   
   * <span data-ttu-id="ce61e-127">**Nom** hello – nom de l’instantané programmé de hello.</span><span class="sxs-lookup"><span data-stu-id="ce61e-127">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="ce61e-128">**Démarré** : date de hello et l’heure de début de l’instantané d’hello.</span><span class="sxs-lookup"><span data-stu-id="ce61e-128">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="ce61e-129">**Arrêté** – date de hello et l’heure instantané d’hello terminée ou a été arrêté.</span><span class="sxs-lookup"><span data-stu-id="ce61e-129">**Stopped** – hello date and time when hello snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="ce61e-130">**Écoulé** – durée hello entre hello **démarré** et **arrêté** fois.</span><span class="sxs-lookup"><span data-stu-id="ce61e-130">**Elapsed** – hello amount of time between hello **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="ce61e-131">**État** – hello état du travail de hello viennent de se terminer.</span><span class="sxs-lookup"><span data-stu-id="ce61e-131">**Status** – hello state of hello recently completed job.</span></span> <span data-ttu-id="ce61e-132">**Réussite** indique que la sauvegarde hello a été créée avec succès.</span><span class="sxs-lookup"><span data-stu-id="ce61e-132">**Success** indicates that hello backup was created successfully.</span></span> <span data-ttu-id="ce61e-133">**Échec de** indique que le travail hello ne s’est pas exécuté correctement.</span><span class="sxs-lookup"><span data-stu-id="ce61e-133">**Failed** indicates that hello job did not run successfully.</span></span>
   * <span data-ttu-id="ce61e-134">**Informations** : hello raison de l’échec de hello.</span><span class="sxs-lookup"><span data-stu-id="ce61e-134">**Information** – hello reason for hello failure.</span></span>
   * <span data-ttu-id="ce61e-135">**Octets traités (Mo)** – quantité hello de données à partir du groupe de volumes hello qui a été traité (en Mo).</span><span class="sxs-lookup"><span data-stu-id="ce61e-135">**Bytes processed (MB)** – hello amount of data from hello volume group that was processed (in MBs).</span></span> 
     
     ![Travaux exécutés hello des dernières 24 heures](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="ce61e-137">tooperform des actions supplémentaires sur une tâche spécifique, cliquez sur le nom de travail de hello Bonjour **résultats** volet et sélectionnez des options de menu hello.</span><span class="sxs-lookup"><span data-stu-id="ce61e-137">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>
   
    ![Supprimer un travail](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="ce61e-139">Afficher les tâches en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="ce61e-139">View currently running jobs</span></span>
<span data-ttu-id="ce61e-140">Utilisez hello suivant travaux tooview procédure en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ce61e-140">Use hello following procedure tooview jobs that are currently running.</span></span>

#### <a name="tooview-currently-running-jobs"></a><span data-ttu-id="ce61e-141">tooview travaux en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="ce61e-141">tooview currently running jobs</span></span>
1. <span data-ttu-id="ce61e-142">Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ce61e-142">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="ce61e-143">Bonjour **étendue** volet, développez hello **travaux** nœud, puis cliquez sur **en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="ce61e-143">In hello **Scope** pane, expand hello **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="ce61e-144">En fonction de hello **vue** options que vous spécifiez, hello informations suivantes s’affichent dans hello **résultats** volet :</span><span class="sxs-lookup"><span data-stu-id="ce61e-144">Depending on hello **View** options you specify, hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="ce61e-145">**Nom** hello – nom de l’instantané programmé de hello.</span><span class="sxs-lookup"><span data-stu-id="ce61e-145">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="ce61e-146">**Démarré** : date de hello et l’heure de début de l’instantané d’hello.</span><span class="sxs-lookup"><span data-stu-id="ce61e-146">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="ce61e-147">**Point de contrôle** – hello action en cours de sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="ce61e-147">**Checkpoint** – hello current action of hello backup.</span></span>
   * <span data-ttu-id="ce61e-148">**État** – hello pourcentage d’achèvement.</span><span class="sxs-lookup"><span data-stu-id="ce61e-148">**Status** – hello percentage of completion.</span></span>
   * <span data-ttu-id="ce61e-149">**Écoulé** – hello durée écoulée depuis le début de la sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="ce61e-149">**Elapsed** – hello amount of time that has passed since hello backup began.</span></span> 
   * <span data-ttu-id="ce61e-150">**Débit moyen (Mo)** – taux total d’octets de toothat de traitement des données de temps total nécessaire pour le traitement (Mo).</span><span class="sxs-lookup"><span data-stu-id="ce61e-150">**Average throughput (MB)** – ratio of total bytes of data processed toothat of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="ce61e-151">**Octets traités (Mo)** : nombre total d’octets de données traités (en Mo).</span><span class="sxs-lookup"><span data-stu-id="ce61e-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="ce61e-152">**Octets écrits (Mo)** : nombre total d’octets de données écrits (en Mo).</span><span class="sxs-lookup"><span data-stu-id="ce61e-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="ce61e-153">Il inclut les données de salutation ainsi que les métadonnées de hello et n’est donc généralement supérieur à hello octets traités.</span><span class="sxs-lookup"><span data-stu-id="ce61e-153">It includes hello data as well as hello metadata and hence is typically greater than hello Bytes Processed.</span></span>
     
     ![Tâches en cours d’exécution](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="ce61e-155">tooperform des actions supplémentaires sur une tâche spécifique, cliquez sur le nom de travail de hello Bonjour **résultats** volet et sélectionnez des options de menu hello.</span><span class="sxs-lookup"><span data-stu-id="ce61e-155">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce61e-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ce61e-156">Next steps</span></span>
* <span data-ttu-id="ce61e-157">Découvrez comment trop[utiliser le Gestionnaire d’instantanés StorSimple tooadminister votre solution StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="ce61e-157">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="ce61e-158">Découvrez comment trop[utiliser le catalogue de sauvegarde de gestionnaire d’instantanés StorSimple toomanage hello](storsimple-snapshot-manager-manage-backup-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="ce61e-158">Learn how too[use StorSimple Snapshot Manager toomanage hello backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

