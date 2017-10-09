---
title: aaaManage votre catalogue de sauvegarde StorSimple | Documents Microsoft
description: "Explique comment toouse hello toolist de page pour le Gestionnaire de périphériques StorSimple service catalogue de sauvegarde, sélectionnez et supprimer des jeux de sauvegarde."
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
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a><span data-ttu-id="bb85d-103">Utilisez hello le Gestionnaire de périphériques StorSimple service toomanage votre catalogue de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="bb85d-103">Use hello StorSimple Device Manager service toomanage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="bb85d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bb85d-104">Overview</span></span>
<span data-ttu-id="bb85d-105">Hello service du Gestionnaire de périphériques StorSimple **catalogue de sauvegarde** panneau affiche tous les jeux de sauvegarde hello qui sont créés lorsque les sauvegardes manuelles ou planifiées sont effectuées.</span><span class="sxs-lookup"><span data-stu-id="bb85d-105">hello StorSimple Device Manager service **Backup Catalog** blade displays all hello backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="bb85d-106">Vous pouvez utiliser cette toolist page toutes les sauvegardes hello pour une stratégie de sauvegarde ou un volume, sélectionnez ou supprimer les sauvegardes, ou utiliser une sauvegarde toorestore ou cloner un volume.</span><span class="sxs-lookup"><span data-stu-id="bb85d-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

<span data-ttu-id="bb85d-107">Ce didacticiel explique comment toolist, select et supprimer une jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="bb85d-107">This tutorial explains how toolist, select, and delete a backup set.</span></span> <span data-ttu-id="bb85d-108">toolearn comment toorestore votre périphérique de sauvegarde, accédez trop[restaurer votre appareil à partir d’un jeu de sauvegarde](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="bb85d-108">toolearn how toorestore your device from backup, go too[Restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span> <span data-ttu-id="bb85d-109">toolearn comment tooclone un volume, accédez trop[cloner un volume StorSimple](storsimple-8000-clone-volume-u2.md).</span><span class="sxs-lookup"><span data-stu-id="bb85d-109">toolearn how tooclone a volume, go too[Clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>

![Catalogue de sauvegarde](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

<span data-ttu-id="bb85d-111">Hello **catalogue de sauvegarde** panneau fournit un toonarrow requête votre sélection du jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="bb85d-111">hello **Backup Catalog** blade provides a query toonarrow your backup set selection.</span></span> <span data-ttu-id="bb85d-112">Vous pouvez filtrer les jeux de sauvegarde hello qui est récupérés, en fonction de hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="bb85d-112">You can filter hello backup sets that are retrieved, based on hello following parameters:</span></span>

* <span data-ttu-id="bb85d-113">**APPAREIL** – périphérique hello sur quel hello jeu de sauvegarde a été créé.</span><span class="sxs-lookup"><span data-stu-id="bb85d-113">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="bb85d-114">**Stratégie de sauvegarde ou Volume** – hello stratégie de sauvegarde ou volume associé à ce jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="bb85d-114">**Backup policy or Volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="bb85d-115">**Depuis et vers** : hello plage de date et heure de création de jeu de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="bb85d-115">**From and To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="bb85d-116">Hello jeux de sauvegarde filtrés sont ensuite sous forme de tableau en fonction de hello suivant des attributs :</span><span class="sxs-lookup"><span data-stu-id="bb85d-116">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="bb85d-117">**Nom** hello – nom de la stratégie de sauvegarde hello ou volume associé au jeu de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="bb85d-117">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="bb85d-118">**Taille** – hello taille réelle du jeu de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="bb85d-118">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="bb85d-119">**Créé le** : date de hello et l’heure de création des sauvegardes de hello.</span><span class="sxs-lookup"><span data-stu-id="bb85d-119">**Created On** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="bb85d-120">**Type** : les jeux de sauvegarde peuvent être des instantanés locaux ou des instantanés cloud.</span><span class="sxs-lookup"><span data-stu-id="bb85d-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="bb85d-121">Un instantané local est une sauvegarde de toutes vos données de volume stockées localement sur le périphérique de hello, tandis qu’un instantané cloud fait référence sauvegarde toohello des données de volume résidant dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="bb85d-121">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="bb85d-122">Les instantanés locaux offrent un accès plus rapide, alors que les instantanés cloud sont choisis pour la résilience des données.</span><span class="sxs-lookup"><span data-stu-id="bb85d-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="bb85d-123">**Initié par** : les sauvegardes hello peuvent être initiées automatiquement par une planification ou manuellement par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bb85d-123">**Initiated By** – hello backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="bb85d-124">Vous pouvez utiliser une sauvegarde de tooschedule de stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="bb85d-124">You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="bb85d-125">Vous pouvez également utiliser hello **sauvegarde** option tootake une sauvegarde manuelle.</span><span class="sxs-lookup"><span data-stu-id="bb85d-125">Alternatively, you can use hello **Take backup** option tootake a manual backup.</span></span>

## <a name="list-backup-sets-for-a-backup-policy"></a><span data-ttu-id="bb85d-126">Répertorier les jeux de sauvegarde pour une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="bb85d-126">List backup sets for a backup policy</span></span>
<span data-ttu-id="bb85d-127">Les étapes suivantes de hello complète toolist toutes les sauvegardes de hello pour une stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="bb85d-127">Complete hello following steps toolist all hello backups for a backup policy.</span></span>

#### <a name="toolist-backup-sets"></a><span data-ttu-id="bb85d-128">jeux de sauvegarde toolist</span><span class="sxs-lookup"><span data-stu-id="bb85d-128">toolist backup sets</span></span>
1. <span data-ttu-id="bb85d-129">Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **catalogue de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="bb85d-129">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>

2. <span data-ttu-id="bb85d-130">Filtrage des sélections de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bb85d-130">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="bb85d-131">Spécifiez la plage de temps hello.</span><span class="sxs-lookup"><span data-stu-id="bb85d-131">Specify hello time range.</span></span>
   2. <span data-ttu-id="bb85d-132">Sélectionnez le périphérique approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="bb85d-132">Select hello appropriate device.</span></span>
   3. <span data-ttu-id="bb85d-133">Filtrer par **stratégie de sauvegarde** tooview hello sauvegardes hello correspondantes.</span><span class="sxs-lookup"><span data-stu-id="bb85d-133">Filter by **Backup policy** tooview hello corresponding hello backups.</span></span>
   3. <span data-ttu-id="bb85d-134">Dans la liste déroulante de stratégie de sauvegarde hello, choisissez **tous les** tooview tous hello hello sélectionné des sauvegardes appareil.</span><span class="sxs-lookup"><span data-stu-id="bb85d-134">From hello backup policy dropdown list, choose **All** tooview all hello backups on hello selected device.</span></span>
   4. <span data-ttu-id="bb85d-135">Cliquez sur **appliquer** tooexecute cette requête.</span><span class="sxs-lookup"><span data-stu-id="bb85d-135">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="bb85d-136">les sauvegardes de Hello associées de stratégie de sauvegarde hello sélectionné doivent apparaître dans la liste hello des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="bb85d-136">hello backups associated with hello selected backup policy should appear in hello list of backup sets.</span></span>

      ![Accédez toobackup catalogue](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a><span data-ttu-id="bb85d-138">Sélectionner un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="bb85d-138">Select a backup set</span></span>
<span data-ttu-id="bb85d-139">Hello complet suivant les étapes tooselect une sauvegarde définis pour une stratégie de sauvegarde ou volume.</span><span class="sxs-lookup"><span data-stu-id="bb85d-139">Complete hello following steps tooselect a backup set for a volume or backup policy.</span></span>

#### <a name="tooselect-a-backup-set"></a><span data-ttu-id="bb85d-140">tooselect un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="bb85d-140">tooselect a backup set</span></span>
1. <span data-ttu-id="bb85d-141">Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **catalogue de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="bb85d-141">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="bb85d-142">Filtrage des sélections de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bb85d-142">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="bb85d-143">Spécifiez la plage de temps hello.</span><span class="sxs-lookup"><span data-stu-id="bb85d-143">Specify hello time range.</span></span> 
   2. <span data-ttu-id="bb85d-144">Sélectionnez le périphérique approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="bb85d-144">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="bb85d-145">Filtrer par la stratégie de sauvegarde ou de volume pour la sauvegarde hello que vous souhaitez tooselect.</span><span class="sxs-lookup"><span data-stu-id="bb85d-145">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="bb85d-146">Cliquez sur **appliquer** tooexecute cette requête.</span><span class="sxs-lookup"><span data-stu-id="bb85d-146">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="bb85d-147">Hello sauvegardes associées de stratégie de sauvegarde ou volume hello sélectionné doivent apparaître dans la liste hello des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="bb85d-147">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Accédez toobackup catalogue](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="bb85d-149">Sélectionnez un jeu de sauvegarde et développez-le.</span><span class="sxs-lookup"><span data-stu-id="bb85d-149">Select and expand a backup set.</span></span> <span data-ttu-id="bb85d-150">Vous pouvez maintenant voir les jeux de sauvegarde hello ventilées par volumes hello qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="bb85d-150">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="bb85d-151">Hello **restaurer** et **supprimer** options sont disponibles via le menu contextuel de hello (clic droit) pour le jeu de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="bb85d-151">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="bb85d-152">Vous pouvez effectuer une de ces actions sur un jeu de sauvegarde hello que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="bb85d-152">You can perform either of these actions on hello backup set that you selected.</span></span>

    ![Accédez toobackup catalogue](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a><span data-ttu-id="bb85d-154">Supprimer un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="bb85d-154">Delete a backup set</span></span>
<span data-ttu-id="bb85d-155">Suppression d’une sauvegarde lorsque vous ne souhaitez plus des données hello tooretain associées.</span><span class="sxs-lookup"><span data-stu-id="bb85d-155">Delete a backup when you no longer wish tooretain hello data associated with it.</span></span> <span data-ttu-id="bb85d-156">Effectuer hello suivant les étapes toodelete un jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="bb85d-156">Perform hello following steps toodelete a backup set.</span></span>

#### <a name="toodelete-a-backup-set"></a><span data-ttu-id="bb85d-157">toodelete un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="bb85d-157">toodelete a backup set</span></span>
 <span data-ttu-id="bb85d-158">Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **catalogue de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="bb85d-158">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="bb85d-159">Filtrage des sélections de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bb85d-159">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="bb85d-160">Spécifiez la plage de temps hello.</span><span class="sxs-lookup"><span data-stu-id="bb85d-160">Specify hello time range.</span></span> 
   2. <span data-ttu-id="bb85d-161">Sélectionnez le périphérique approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="bb85d-161">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="bb85d-162">Filtrer par la stratégie de sauvegarde ou de volume pour la sauvegarde hello que vous souhaitez tooselect.</span><span class="sxs-lookup"><span data-stu-id="bb85d-162">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="bb85d-163">Cliquez sur **appliquer** tooexecute cette requête.</span><span class="sxs-lookup"><span data-stu-id="bb85d-163">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="bb85d-164">Hello sauvegardes associées de stratégie de sauvegarde ou volume hello sélectionné doivent apparaître dans la liste hello des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="bb85d-164">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Accédez toobackup catalogue](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="bb85d-166">Sélectionnez un jeu de sauvegarde et développez-le.</span><span class="sxs-lookup"><span data-stu-id="bb85d-166">Select and expand a backup set.</span></span> <span data-ttu-id="bb85d-167">Vous pouvez maintenant voir les jeux de sauvegarde hello ventilées par volumes hello qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="bb85d-167">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="bb85d-168">Hello **restaurer** et **supprimer** options sont disponibles via le menu contextuel de hello (clic droit) pour le jeu de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="bb85d-168">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="bb85d-169">Cliquez sur le jeu de sauvegarde hello sélectionné et à partir du menu contextuel de hello, sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="bb85d-169">Right-click hello selected backup set and from hello context menu, select **Delete**.</span></span>

    ![Accédez toobackup catalogue](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. <span data-ttu-id="bb85d-171">Lorsque vous êtes invité à confirmer l’opération, passez en revue les informations hello affiché, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="bb85d-171">When prompted for confirmation, review hello displayed information and click **Delete**.</span></span> <span data-ttu-id="bb85d-172">sauvegarde sélectionnée de Hello est supprimé définitivement.</span><span class="sxs-lookup"><span data-stu-id="bb85d-172">hello selected backup is deleted permanently.</span></span>

    ![Accédez toobackup catalogue](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. <span data-ttu-id="bb85d-174">Vous êtes averti lorsqu’une suppression de hello est en cours d’exécution et lorsqu’il a terminé avec succès.</span><span class="sxs-lookup"><span data-stu-id="bb85d-174">You will be notified when hello deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="bb85d-175">Après que la suppression de hello s’effectue, actualiser la requête hello sur cette page.</span><span class="sxs-lookup"><span data-stu-id="bb85d-175">After hello deletion is done, refresh hello query on this page.</span></span> <span data-ttu-id="bb85d-176">jeu de sauvegarde Hello supprimé n’apparaît plus dans liste hello des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="bb85d-176">hello deleted backup set will no longer appear in hello list of backup sets.</span></span>

    ![Accédez toobackup catalogue](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a><span data-ttu-id="bb85d-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bb85d-178">Next steps</span></span>
* <span data-ttu-id="bb85d-179">Découvrez comment trop[utilisez hello toorestore du catalogue de sauvegarde de votre appareil à partir d’un jeu de sauvegarde](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="bb85d-179">Learn how too[use hello backup catalog toorestore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="bb85d-180">Découvrez comment trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="bb85d-180">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

