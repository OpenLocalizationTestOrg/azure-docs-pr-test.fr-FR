---
title: "les stratégies de sauvegarde de gestionnaire d’instantanés aaaStorSimple | Documents Microsoft"
description: "Décrit comment toouse hello StorSimple Snapshot Manager MMC enfichable toocreate et gérer des stratégies de sauvegarde hello qui contrôlent les sauvegardes planifiées."
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
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a><span data-ttu-id="2e611-103">Utilisez le Gestionnaire d’instantanés StorSimple toocreate et gérer des stratégies de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="2e611-103">Use StorSimple Snapshot Manager toocreate and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="2e611-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="2e611-104">Overview</span></span>
<span data-ttu-id="2e611-105">Une stratégie de sauvegarde crée une planification de sauvegarde des données de volume local ou dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="2e611-105">A backup policy creates a schedule for backing up volume data locally or in hello cloud.</span></span> <span data-ttu-id="2e611-106">Lorsque vous créez une stratégie de sauvegarde, vous pouvez également spécifier une stratégie de rétention.</span><span class="sxs-lookup"><span data-stu-id="2e611-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="2e611-107">(Vous pouvez conserver un maximum de 64 instantanés). Pour plus d'informations sur les stratégies de sauvegarde, consultez la page [Types de sauvegarde](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) dans [Gamme StorSimple 8000 : une solution de cloud hybride](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2e611-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="2e611-108">Ce didacticiel explique comment :</span><span class="sxs-lookup"><span data-stu-id="2e611-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="2e611-109">Créer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="2e611-109">Create a backup policy</span></span>
* <span data-ttu-id="2e611-110">Modifier une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="2e611-110">Edit a backup policy</span></span>
* <span data-ttu-id="2e611-111">Supprimer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="2e611-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="2e611-112">Créer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="2e611-112">Create a backup policy</span></span>
<span data-ttu-id="2e611-113">Utilisez hello suivant la procédure toocreate une stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="2e611-113">Use hello following procedure toocreate a new backup policy.</span></span>

#### <a name="toocreate-a-backup-policy"></a><span data-ttu-id="2e611-114">toocreate une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="2e611-114">toocreate a backup policy</span></span>
1. <span data-ttu-id="2e611-115">Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2e611-115">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="2e611-116">Bonjour **étendue** volet, avec le bouton droit **stratégies de sauvegarde**, puis cliquez sur **créer une stratégie de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="2e611-116">In hello **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![Créer une stratégie de sauvegarde](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="2e611-118">Hello **créer une stratégie** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="2e611-118">hello **Create a Policy** dialog box appears.</span></span>

    ![Créer une stratégie - onglet Général](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="2e611-120">Sur hello **général** onglet, hello complète informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2e611-120">On hello **General** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="2e611-121">Bonjour **nom** zone de texte, tapez un nom pour la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="2e611-121">In hello **Name** text box, type a name for hello policy.</span></span>
   2. <span data-ttu-id="2e611-122">Bonjour **groupe de volumes** zone de texte, le nom de groupe de volumes hello associé hello stratégie hello de type.</span><span class="sxs-lookup"><span data-stu-id="2e611-122">In hello **Volume group** text box, type hello name of hello volume group associated with hello policy.</span></span>
   3. <span data-ttu-id="2e611-123">Sélectionnez **Instantané local** ou **Instantané cloud**.</span><span class="sxs-lookup"><span data-stu-id="2e611-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="2e611-124">Sélectionnez nombre hello de captures instantanées tooretain.</span><span class="sxs-lookup"><span data-stu-id="2e611-124">Select hello number of snapshots tooretain.</span></span> <span data-ttu-id="2e611-125">Si vous sélectionnez **tous les**, 64 instantanés à conserver (hello maximale).</span><span class="sxs-lookup"><span data-stu-id="2e611-125">If you select **All**, 64 snapshots will be retained (hello maximum).</span></span>
4. <span data-ttu-id="2e611-126">Cliquez sur hello **planification** onglet.</span><span class="sxs-lookup"><span data-stu-id="2e611-126">Click hello **Schedule** tab.</span></span>

    ![Créer une stratégie - onglet Planification](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="2e611-128">Sur hello **planification** onglet, hello complète informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2e611-128">On hello **Schedule** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="2e611-129">Cliquez sur hello **activer** sauvegarde suivante de case à cocher tooschedule hello.</span><span class="sxs-lookup"><span data-stu-id="2e611-129">Click hello **Enable** check box tooschedule hello next backup.</span></span>
   2. <span data-ttu-id="2e611-130">Sous **Paramètres**, sélectionnez **Une fois**, **Quotidienne**, **Hebdomadaire** ou **Mensuelle**.</span><span class="sxs-lookup"><span data-stu-id="2e611-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="2e611-131">Bonjour **Démarrer** zone de texte, cliquez sur icône du calendrier hello et sélectionnez une date de début.</span><span class="sxs-lookup"><span data-stu-id="2e611-131">In hello **Start** text box, click hello calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="2e611-132">Sous **Paramètres avancés**, vous pouvez définir des planifications répétées facultatives et une date de fin.</span><span class="sxs-lookup"><span data-stu-id="2e611-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="2e611-133">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e611-133">Click **OK**.</span></span>

<span data-ttu-id="2e611-134">Après avoir créé une stratégie de sauvegarde, hello informations suivantes s’affiche dans hello **résultats** volet :</span><span class="sxs-lookup"><span data-stu-id="2e611-134">After you create a backup policy, hello following information appears in hello **Results** pane:</span></span>

* <span data-ttu-id="2e611-135">**Nom** hello – nom de la stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="2e611-135">**Name** – hello name of backup policy.</span></span>
* <span data-ttu-id="2e611-136">**Type** : instantané local ou instantané cloud.</span><span class="sxs-lookup"><span data-stu-id="2e611-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="2e611-137">**Groupe de volumes** : hello associé hello stratégie de groupe de volumes.</span><span class="sxs-lookup"><span data-stu-id="2e611-137">**Volume Group** – hello volume group associated with hello policy.</span></span>
* <span data-ttu-id="2e611-138">**Rétention** hello – nombre d’instantanés conservés ; hello maximale est 64.</span><span class="sxs-lookup"><span data-stu-id="2e611-138">**Retention** – hello number of snapshots retained; hello maximum is 64.</span></span>
* <span data-ttu-id="2e611-139">**Créé** – date hello que cette stratégie a été créée.</span><span class="sxs-lookup"><span data-stu-id="2e611-139">**Created** – hello date that this policy was created.</span></span>
* <span data-ttu-id="2e611-140">**Activé** : indique si la stratégie de hello est actuellement en vigueur : **True** indique qu’il est appliqué. **False** indique qu’il n’est pas en vigueur.</span><span class="sxs-lookup"><span data-stu-id="2e611-140">**Enabled** – whether hello policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="2e611-141">Modifier une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="2e611-141">Edit a backup policy</span></span>
<span data-ttu-id="2e611-142">Utilisez hello suivant la procédure tooedit une stratégie de sauvegarde existante.</span><span class="sxs-lookup"><span data-stu-id="2e611-142">Use hello following procedure tooedit an existing backup policy.</span></span>

#### <a name="tooedit-a-backup-policy"></a><span data-ttu-id="2e611-143">tooedit une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="2e611-143">tooedit a backup policy</span></span>
1. <span data-ttu-id="2e611-144">Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2e611-144">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="2e611-145">Bonjour **étendue** volet, cliquez sur hello **stratégies de sauvegarde** nœud.</span><span class="sxs-lookup"><span data-stu-id="2e611-145">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="2e611-146">Toutes les stratégies de sauvegarde hello apparaissent dans hello **résultats** volet.</span><span class="sxs-lookup"><span data-stu-id="2e611-146">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="2e611-147">Cliquez sur stratégie hello que vous souhaitez tooedit, puis cliquez sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="2e611-147">Right-click hello policy that you want tooedit, and then click **Edit**.</span></span>

    ![Modifier une stratégie de sauvegarde](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="2e611-149">Hello lorsque **créer une stratégie de** fenêtre s’affiche, entrez vos modifications, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e611-149">When hello **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="2e611-150">Supprimer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="2e611-150">Delete a backup policy</span></span>
<span data-ttu-id="2e611-151">Utilisez hello suivant la procédure toodelete une stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="2e611-151">Use hello following procedure toodelete a backup policy.</span></span>

#### <a name="toodelete-a-backup-policy"></a><span data-ttu-id="2e611-152">toodelete une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="2e611-152">toodelete a backup policy</span></span>
1. <span data-ttu-id="2e611-153">Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2e611-153">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="2e611-154">Bonjour **étendue** volet, cliquez sur hello **stratégies de sauvegarde** nœud.</span><span class="sxs-lookup"><span data-stu-id="2e611-154">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="2e611-155">Toutes les stratégies de sauvegarde hello apparaissent dans hello **résultats** volet.</span><span class="sxs-lookup"><span data-stu-id="2e611-155">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="2e611-156">Cliquez sur la stratégie de sauvegarde hello que vous souhaitez toodelete, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="2e611-156">Right-click hello backup policy that you want toodelete, and then click **Delete**.</span></span>
4. <span data-ttu-id="2e611-157">Lorsque le message de confirmation hello s’affiche, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="2e611-157">When hello confirmation message appears, click **Yes**.</span></span>

    ![Confirmation de la suppression de la stratégie de sauvegarde](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="2e611-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e611-159">Next steps</span></span>
* <span data-ttu-id="2e611-160">Découvrez comment trop[utiliser le Gestionnaire d’instantanés StorSimple tooadminister votre solution StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="2e611-160">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="2e611-161">Découvrez comment trop[utiliser le Gestionnaire d’instantanés StorSimple tooview et gérer des travaux de sauvegarde](storsimple-snapshot-manager-manage-backup-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="2e611-161">Learn how too[use StorSimple Snapshot Manager tooview and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
