---
title: "Stratégies de sauvegarde du Gestionnaire d’instantanés StorSimple | Microsoft Docs"
description: "Explique comment utiliser le composant logiciel enfichable MMC Gestionnaire d’instantanés StorSimple pour créer et gérer les stratégies de sauvegarde qui contrôlent les sauvegardes planifiées."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 218c89e403673c16c72da95aa2c1d685bbed5a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-backup-policies"></a><span data-ttu-id="e5de8-103">Utiliser le Gestionnaire d’instantanés StorSimple pour créer et gérer des stratégies de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5de8-103">Use StorSimple Snapshot Manager to create and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="e5de8-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e5de8-104">Overview</span></span>
<span data-ttu-id="e5de8-105">Une stratégie de sauvegarde permet de créer une planification de sauvegarde des données de volume localement ou dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="e5de8-105">A backup policy creates a schedule for backing up volume data locally or in the cloud.</span></span> <span data-ttu-id="e5de8-106">Lorsque vous créez une stratégie de sauvegarde, vous pouvez également spécifier une stratégie de rétention.</span><span class="sxs-lookup"><span data-stu-id="e5de8-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="e5de8-107">(Vous pouvez conserver un maximum de 64 instantanés). Pour plus d'informations sur les stratégies de sauvegarde, consultez la page [Types de sauvegarde](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) dans [Gamme StorSimple 8000 : une solution de cloud hybride](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5de8-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="e5de8-108">Ce didacticiel explique comment :</span><span class="sxs-lookup"><span data-stu-id="e5de8-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="e5de8-109">Créer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5de8-109">Create a backup policy</span></span>
* <span data-ttu-id="e5de8-110">Modifier une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5de8-110">Edit a backup policy</span></span>
* <span data-ttu-id="e5de8-111">Supprimer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5de8-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="e5de8-112">Créer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5de8-112">Create a backup policy</span></span>
<span data-ttu-id="e5de8-113">Pour créer une stratégie de sauvegarde, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="e5de8-113">Use the following procedure to create a new backup policy.</span></span>

#### <a name="to-create-a-backup-policy"></a><span data-ttu-id="e5de8-114">Pour créer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5de8-114">To create a backup policy</span></span>
1. <span data-ttu-id="e5de8-115">Cliquez sur l’icône de bureau pour démarrer le Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e5de8-115">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="e5de8-116">Dans le volet **Étendue**, cliquez avec le bouton droit sur **Stratégies de sauvegarde**, puis cliquez sur **Créer une stratégie de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="e5de8-116">In the **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![Créer une stratégie de sauvegarde](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="e5de8-118">La boîte de dialogue **Créer une stratégie** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e5de8-118">The **Create a Policy** dialog box appears.</span></span>

    ![Créer une stratégie - onglet Général](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="e5de8-120">Dans l’onglet **Général** , renseignez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e5de8-120">On the **General** tab, complete the following information:</span></span>

   1. <span data-ttu-id="e5de8-121">Dans la zone de texte **Nom** , tapez un nom pour la stratégie.</span><span class="sxs-lookup"><span data-stu-id="e5de8-121">In the **Name** text box, type a name for the policy.</span></span>
   2. <span data-ttu-id="e5de8-122">Dans la zone de texte **Groupe de volumes** , tapez le nom du groupe de volumes associé à la stratégie.</span><span class="sxs-lookup"><span data-stu-id="e5de8-122">In the **Volume group** text box, type the name of the volume group associated with the policy.</span></span>
   3. <span data-ttu-id="e5de8-123">Sélectionnez **Instantané local** ou **Instantané cloud**.</span><span class="sxs-lookup"><span data-stu-id="e5de8-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="e5de8-124">Sélectionnez le nombre d’instantanés à conserver.</span><span class="sxs-lookup"><span data-stu-id="e5de8-124">Select the number of snapshots to retain.</span></span> <span data-ttu-id="e5de8-125">Si vous sélectionnez **Tous**, 64 instantanés seront conservés (il s’agit du maximum).</span><span class="sxs-lookup"><span data-stu-id="e5de8-125">If you select **All**, 64 snapshots will be retained (the maximum).</span></span>
4. <span data-ttu-id="e5de8-126">Cliquez sur l'onglet **Planification** .</span><span class="sxs-lookup"><span data-stu-id="e5de8-126">Click the **Schedule** tab.</span></span>

    ![Créer une stratégie - onglet Planification](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="e5de8-128">Sous l’onglet **Planification** , renseignez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e5de8-128">On the **Schedule** tab, complete the following information:</span></span>

   1. <span data-ttu-id="e5de8-129">Cochez la case **Activer** pour planifier la prochaine sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e5de8-129">Click the **Enable** check box to schedule the next backup.</span></span>
   2. <span data-ttu-id="e5de8-130">Sous **Paramètres**, sélectionnez **Une fois**, **Quotidienne**, **Hebdomadaire** ou **Mensuelle**.</span><span class="sxs-lookup"><span data-stu-id="e5de8-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="e5de8-131">Dans la zone de texte **Début** , cliquez sur l’icône de calendrier et sélectionnez une date de début.</span><span class="sxs-lookup"><span data-stu-id="e5de8-131">In the **Start** text box, click the calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="e5de8-132">Sous **Paramètres avancés**, vous pouvez définir des planifications répétées facultatives et une date de fin.</span><span class="sxs-lookup"><span data-stu-id="e5de8-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="e5de8-133">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5de8-133">Click **OK**.</span></span>

<span data-ttu-id="e5de8-134">Une fois la stratégie de sauvegarde créée, les informations suivantes apparaissent dans le volet **Résultats** :</span><span class="sxs-lookup"><span data-stu-id="e5de8-134">After you create a backup policy, the following information appears in the **Results** pane:</span></span>

* <span data-ttu-id="e5de8-135">**Nom** : nom de la stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e5de8-135">**Name** – the name of backup policy.</span></span>
* <span data-ttu-id="e5de8-136">**Type** : instantané local ou instantané cloud.</span><span class="sxs-lookup"><span data-stu-id="e5de8-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="e5de8-137">**Groupe de volumes** : groupe de volumes associé à la stratégie.</span><span class="sxs-lookup"><span data-stu-id="e5de8-137">**Volume Group** – the volume group associated with the policy.</span></span>
* <span data-ttu-id="e5de8-138">**Rétention** : nombre d’instantanés conservés ; le maximum est 64.</span><span class="sxs-lookup"><span data-stu-id="e5de8-138">**Retention** – the number of snapshots retained; the maximum is 64.</span></span>
* <span data-ttu-id="e5de8-139">**Créé** : date à laquelle cette stratégie a été créée.</span><span class="sxs-lookup"><span data-stu-id="e5de8-139">**Created** – the date that this policy was created.</span></span>
* <span data-ttu-id="e5de8-140">**Activée** : indique si la stratégie est en vigueur. La valeur **True** indique qu’elle est en vigueur, la valeur **False** qu’elle ne l’est pas.</span><span class="sxs-lookup"><span data-stu-id="e5de8-140">**Enabled** – whether the policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="e5de8-141">Modifier une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5de8-141">Edit a backup policy</span></span>
<span data-ttu-id="e5de8-142">Pour modifier une stratégie de sauvegarde existante, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="e5de8-142">Use the following procedure to edit an existing backup policy.</span></span>

#### <a name="to-edit-a-backup-policy"></a><span data-ttu-id="e5de8-143">Pour modifier une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5de8-143">To edit a backup policy</span></span>
1. <span data-ttu-id="e5de8-144">Cliquez sur l’icône de bureau pour démarrer le Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e5de8-144">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="e5de8-145">Dans le volet **Étendue**, cliquez sur le nœud **Stratégies de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="e5de8-145">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="e5de8-146">Toutes les stratégies de sauvegarde apparaissent dans le volet **Résultats** .</span><span class="sxs-lookup"><span data-stu-id="e5de8-146">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="e5de8-147">Cliquez avec le bouton droit sur la stratégie à modifier, puis cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="e5de8-147">Right-click the policy that you want to edit, and then click **Edit**.</span></span>

    ![Modifier une stratégie de sauvegarde](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="e5de8-149">Quand la fenêtre **Créer une stratégie** s’affiche, entrez vos modifications, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5de8-149">When the **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="e5de8-150">Supprimer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5de8-150">Delete a backup policy</span></span>
<span data-ttu-id="e5de8-151">Pour supprimer une stratégie de sauvegarde, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="e5de8-151">Use the following procedure to delete a backup policy.</span></span>

#### <a name="to-delete-a-backup-policy"></a><span data-ttu-id="e5de8-152">Pour supprimer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5de8-152">To delete a backup policy</span></span>
1. <span data-ttu-id="e5de8-153">Cliquez sur l’icône de bureau pour démarrer le Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e5de8-153">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="e5de8-154">Dans le volet **Étendue**, cliquez sur le nœud **Stratégies de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="e5de8-154">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="e5de8-155">Toutes les stratégies de sauvegarde apparaissent dans le volet **Résultats** .</span><span class="sxs-lookup"><span data-stu-id="e5de8-155">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="e5de8-156">Cliquez avec le bouton droit sur la stratégie de sauvegarde à supprimer, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="e5de8-156">Right-click the backup policy that you want to delete, and then click **Delete**.</span></span>
4. <span data-ttu-id="e5de8-157">Quand le message de confirmation s’affiche, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="e5de8-157">When the confirmation message appears, click **Yes**.</span></span>

    ![Confirmation de la suppression de la stratégie de sauvegarde](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="e5de8-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e5de8-159">Next steps</span></span>
* <span data-ttu-id="e5de8-160">Découvrez comment [utiliser le Gestionnaire d’instantanés StorSimple pour gérer votre solution StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="e5de8-160">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="e5de8-161">Découvrez comment [utiliser le Gestionnaire d’instantanés StorSimple pour afficher et gérer les tâches de sauvegarde](storsimple-snapshot-manager-manage-backup-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="e5de8-161">Learn how to [use StorSimple Snapshot Manager to view and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
