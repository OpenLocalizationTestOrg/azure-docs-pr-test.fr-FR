---
title: "Tâches de sauvegarde du Gestionnaire d’instantanés StorSimple | Microsoft Docs"
description: "Explique comment utiliser le composant logiciel enfichable MMC Gestionnaire d’instantanés StorSimple pour afficher et gérer les tâches de sauvegarde planifiées, en cours d’exécution et terminées."
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
ms.openlocfilehash: 03e306b62250f2bb033cc14e856a59760b5406c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-view-and-manage-backup-jobs"></a><span data-ttu-id="59023-103">Utiliser le Gestionnaire d’instantanés StorSimple pour afficher et gérer les tâches de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="59023-103">Use StorSimple Snapshot Manager to view and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="59023-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="59023-104">Overview</span></span>
<span data-ttu-id="59023-105">Le nœud **Tâches** dans le volet **Étendue** présente les tâches de sauvegarde **planifiées**, des **dernières 24 heures** et **en cours** que vous avez lancées de façon interactive ou à l’aide d’une stratégie configurée.</span><span class="sxs-lookup"><span data-stu-id="59023-105">The **Jobs** node in the **Scope** pane shows the **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="59023-106">Ce didacticiel explique comment utiliser le nœud **Tâches** pour afficher des informations sur les tâches de sauvegarde planifiées, récentes et en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="59023-106">This tutorial explains how you can use the **Jobs** node to display information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="59023-107">(La liste des tâches et les informations correspondantes s’affichent dans le volet **Résultats**.) Vous pouvez également cliquer avec le bouton droit sur une tâche répertoriée et afficher un menu contextuel présentant les actions disponibles.</span><span class="sxs-lookup"><span data-stu-id="59023-107">(The list of jobs and corresponding information appears in the **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="59023-108">Afficher les tâches planifiées</span><span class="sxs-lookup"><span data-stu-id="59023-108">View scheduled jobs</span></span>
<span data-ttu-id="59023-109">Pour afficher les tâches de sauvegarde planifiées, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="59023-109">Use the following procedure to view scheduled backup jobs.</span></span>

#### <a name="to-view-scheduled-jobs"></a><span data-ttu-id="59023-110">Pour afficher les tâches planifiées</span><span class="sxs-lookup"><span data-stu-id="59023-110">To view scheduled jobs</span></span>
1. <span data-ttu-id="59023-111">Cliquez sur l’icône de bureau pour démarrer le Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="59023-111">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="59023-112">Dans le volet **Étendue**, développez le nœud **Tâches**, puis cliquez sur **Planifiées**.</span><span class="sxs-lookup"><span data-stu-id="59023-112">In the **Scope** pane, expand the **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="59023-113">Les informations suivantes sont affichées dans le volet **Résultats** :</span><span class="sxs-lookup"><span data-stu-id="59023-113">The following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="59023-114">**Nom** : nom de l’instantané planifié</span><span class="sxs-lookup"><span data-stu-id="59023-114">**Name** – the name of the scheduled snapshot</span></span>
   * <span data-ttu-id="59023-115">**Exécution suivante** : date et heure du prochain instantané planifié</span><span class="sxs-lookup"><span data-stu-id="59023-115">**Next Run** – the date and time of the next scheduled snapshot</span></span>
   * <span data-ttu-id="59023-116">**Dernière exécution** : date et heure de l’instantané planifié le plus récent</span><span class="sxs-lookup"><span data-stu-id="59023-116">**Last Run** – the date and time of the most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="59023-117">Pour les instantanés ponctuels, les informations des colonnes **Exécution suivante** et **Dernière exécution** sont identiques.</span><span class="sxs-lookup"><span data-stu-id="59023-117">For one-time only snapshots, the **Next Run** and **Last Run** will be the same.</span></span>
     
     ![Tâches de sauvegarde planifiées](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="59023-119">Pour effectuer des actions supplémentaires sur une tâche spécifique, cliquez avec le bouton droit sur le nom de la tâche dans le volet **Résultats** et sélectionnez les options de menu de votre choix.</span><span class="sxs-lookup"><span data-stu-id="59023-119">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="59023-120">Afficher les tâches récentes</span><span class="sxs-lookup"><span data-stu-id="59023-120">View recent jobs</span></span>
<span data-ttu-id="59023-121">Pour afficher les tâches de sauvegarde et de restauration effectuées au cours des 24 dernières heures, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="59023-121">Use the following procedure to view backup and restore jobs that were completed in the last 24 hours.</span></span>

#### <a name="to-view-recent-jobs"></a><span data-ttu-id="59023-122">Pour afficher les tâches récentes</span><span class="sxs-lookup"><span data-stu-id="59023-122">To view recent jobs</span></span>
1. <span data-ttu-id="59023-123">Cliquez sur l’icône de bureau pour démarrer le Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="59023-123">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="59023-124">Dans le volet **Étendue**, développez le nœud **Tâches**, puis cliquez sur **Dernières 24 heures**.</span><span class="sxs-lookup"><span data-stu-id="59023-124">In the **Scope** pane, expand the **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="59023-125">Le volet **Résultats** affiche les tâches de sauvegarde des dernières 24 heures (avec un maximum de 64 tâches).</span><span class="sxs-lookup"><span data-stu-id="59023-125">The **Results** pane shows backup jobs for the last 24 hours (to a maximum of 64 jobs).</span></span> <span data-ttu-id="59023-126">Les informations suivantes apparaissent dans le volet **Résultats**, selon les options spécifiées pour **Affichage** :</span><span class="sxs-lookup"><span data-stu-id="59023-126">The following information appears in the **Results** pane, depending on the **View** options you specify:</span></span>
   
   * <span data-ttu-id="59023-127">**Nom** : nom de l’instantané planifié.</span><span class="sxs-lookup"><span data-stu-id="59023-127">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="59023-128">**Démarré** : date et heure de début de l’instantané.</span><span class="sxs-lookup"><span data-stu-id="59023-128">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="59023-129">**Arrêté** : date et l’heure de fin ou d’arrêt de l’instantané.</span><span class="sxs-lookup"><span data-stu-id="59023-129">**Stopped** – the date and time when the snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="59023-130">**Écoulé** : intervalle de temps entre le **démarrage** et l’**arrêt**.</span><span class="sxs-lookup"><span data-stu-id="59023-130">**Elapsed** – the amount of time between the **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="59023-131">**État** : état de la tâche terminée récemment.</span><span class="sxs-lookup"><span data-stu-id="59023-131">**Status** – the state of the recently completed job.</span></span> <span data-ttu-id="59023-132">**Succès** indique que la sauvegarde a bien été créée.</span><span class="sxs-lookup"><span data-stu-id="59023-132">**Success** indicates that the backup was created successfully.</span></span> <span data-ttu-id="59023-133">**Échec** indique que la tâche ne s’est pas exécutée correctement.</span><span class="sxs-lookup"><span data-stu-id="59023-133">**Failed** indicates that the job did not run successfully.</span></span>
   * <span data-ttu-id="59023-134">**Informations** : raison de l’échec.</span><span class="sxs-lookup"><span data-stu-id="59023-134">**Information** – the reason for the failure.</span></span>
   * <span data-ttu-id="59023-135">**Octets traités (Mo)** : volume de données du groupe de volumes qui ont été traitées (en Mo).</span><span class="sxs-lookup"><span data-stu-id="59023-135">**Bytes processed (MB)** – the amount of data from the volume group that was processed (in MBs).</span></span> 
     
     ![Tâches exécutées au cours des 24 dernières heures](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="59023-137">Pour effectuer des actions supplémentaires sur une tâche spécifique, cliquez avec le bouton droit sur le nom de la tâche dans le volet **Résultats** et sélectionnez les options de menu de votre choix.</span><span class="sxs-lookup"><span data-stu-id="59023-137">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>
   
    ![Supprimer un travail](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="59023-139">Afficher les tâches en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="59023-139">View currently running jobs</span></span>
<span data-ttu-id="59023-140">Pour afficher les tâches en cours d’exécution, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="59023-140">Use the following procedure to view jobs that are currently running.</span></span>

#### <a name="to-view-currently-running-jobs"></a><span data-ttu-id="59023-141">Pour afficher les tâches en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="59023-141">To view currently running jobs</span></span>
1. <span data-ttu-id="59023-142">Cliquez sur l’icône de bureau pour démarrer le Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="59023-142">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="59023-143">Dans le volet **Étendue**, développez le nœud **Tâches**, puis cliquez sur **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="59023-143">In the **Scope** pane, expand the **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="59023-144">Selon les options spécifiées pour **Affichage**, les informations suivantes apparaissent dans le volet **Résultats** :</span><span class="sxs-lookup"><span data-stu-id="59023-144">Depending on the **View** options you specify, the following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="59023-145">**Nom** : nom de l’instantané planifié.</span><span class="sxs-lookup"><span data-stu-id="59023-145">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="59023-146">**Démarré** : date et heure de début de l’instantané.</span><span class="sxs-lookup"><span data-stu-id="59023-146">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="59023-147">**Point de contrôle** : action actuelle de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="59023-147">**Checkpoint** – the current action of the backup.</span></span>
   * <span data-ttu-id="59023-148">**État** : pourcentage d’achèvement.</span><span class="sxs-lookup"><span data-stu-id="59023-148">**Status** – the percentage of completion.</span></span>
   * <span data-ttu-id="59023-149">**Écoulé** : intervalle de temps écoulé depuis le début de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="59023-149">**Elapsed** – the amount of time that has passed since the backup began.</span></span> 
   * <span data-ttu-id="59023-150">**Débit moyen (Mo/s)** : rapport entre le nombre total d’octets de données traités et la durée totale de traitement (Mo).</span><span class="sxs-lookup"><span data-stu-id="59023-150">**Average throughput (MB)** – ratio of total bytes of data processed to that of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="59023-151">**Octets traités (Mo)** : nombre total d’octets de données traités (en Mo).</span><span class="sxs-lookup"><span data-stu-id="59023-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="59023-152">**Octets écrits (Mo)** : nombre total d’octets de données écrits (en Mo).</span><span class="sxs-lookup"><span data-stu-id="59023-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="59023-153">Cela inclut les données et les métadonnées : la valeur de ce paramètre est donc généralement supérieure à la valeur du paramètre Octets traités.</span><span class="sxs-lookup"><span data-stu-id="59023-153">It includes the data as well as the metadata and hence is typically greater than the Bytes Processed.</span></span>
     
     ![Tâches en cours d’exécution](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="59023-155">Pour effectuer des actions supplémentaires sur une tâche spécifique, cliquez avec le bouton droit sur le nom de la tâche dans le volet **Résultats** et sélectionnez les options de menu de votre choix.</span><span class="sxs-lookup"><span data-stu-id="59023-155">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59023-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="59023-156">Next steps</span></span>
* <span data-ttu-id="59023-157">Découvrez comment [utiliser le Gestionnaire d’instantanés StorSimple pour gérer votre solution StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="59023-157">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="59023-158">Découvrez comment [utiliser le Gestionnaire d’instantanés StorSimple pour gérer le catalogue de sauvegarde](storsimple-snapshot-manager-manage-backup-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="59023-158">Learn how to [use StorSimple Snapshot Manager to manage the backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

