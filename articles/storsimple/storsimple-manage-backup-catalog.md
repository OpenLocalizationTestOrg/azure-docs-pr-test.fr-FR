---
title: "Gérer votre catalogue de sauvegarde StorSimple | Microsoft Docs"
description: "Explique comment utiliser la page Catalogue de sauvegarde du service StorSimple Manager pour répertorier, sélectionner et supprimer des jeux de sauvegarde pour un volume."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 5ee9855e1428c7a2d871d9c215d302c5c3b7101a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-your-backup-catalog"></a><span data-ttu-id="1e71b-103">Utiliser le service StorSimple Manager pour gérer votre catalogue de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="1e71b-103">Use the StorSimple Manager service to manage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="1e71b-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1e71b-104">Overview</span></span>
<span data-ttu-id="1e71b-105">La page **Catalogue de sauvegarde** du service StorSimple Manager affiche tous les jeux de sauvegarde créés lors de sauvegardes manuelles ou planifiées.</span><span class="sxs-lookup"><span data-stu-id="1e71b-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="1e71b-106">Vous pouvez utiliser cette page pour répertorier toutes les sauvegardes pour une stratégie de sauvegarde ou un volume, sélectionner ou supprimer des sauvegardes, ou utiliser une sauvegarde pour restaurer ou cloner un volume.</span><span class="sxs-lookup"><span data-stu-id="1e71b-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

<span data-ttu-id="1e71b-107">Ce didacticiel explique comment répertorier, sélectionner et supprimer un jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="1e71b-107">This tutorial explains how to list, select, and delete a backup set.</span></span> <span data-ttu-id="1e71b-108">Pour savoir comment restaurer votre appareil à partir d’une sauvegarde, accédez à [Restaurer l’appareil à partir d’un jeu de sauvegarde](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="1e71b-108">To learn how to restore your device from backup, go to [Restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span> <span data-ttu-id="1e71b-109">Pour découvrir comment cloner un volume, accédez à [Cloner un volume StorSimple](storsimple-clone-volume.md).</span><span class="sxs-lookup"><span data-stu-id="1e71b-109">To learn how to clone a volume, go to [Clone a StorSimple volume](storsimple-clone-volume.md).</span></span>

![Catalogue de sauvegarde](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

<span data-ttu-id="1e71b-111">La page **Catalogue de sauvegarde** comprend une zone de requête pour affiner la sélection des ensembles de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="1e71b-111">The **Backup Catalog** page provides a query to narrow your backup set selection.</span></span> <span data-ttu-id="1e71b-112">Vous pouvez filtrer les jeux de sauvegarde récupérés selon les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="1e71b-112">You can filter the backup sets that are retrieved, based on the following parameters:</span></span>

* <span data-ttu-id="1e71b-113">**Appareil** : appareil sur lequel le jeu de sauvegarde a été créé.</span><span class="sxs-lookup"><span data-stu-id="1e71b-113">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="1e71b-114">**Stratégie de sauvegarde ou volume** : stratégie de sauvegarde ou volume associé à ce jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="1e71b-114">**Backup Policy or Volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="1e71b-115">**De et À** : plage de dates et d’heures de création du jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="1e71b-115">**From and To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="1e71b-116">Les jeux de sauvegarde filtrés sont ensuite affichés sous forme de tableau sur la base des attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="1e71b-116">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="1e71b-117">**Nom** : nom de la stratégie de sauvegarde ou du volume associé à ce jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="1e71b-117">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="1e71b-118">**Taille** : taille réelle du jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="1e71b-118">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="1e71b-119">**Créé le** : date et heure auxquelles les sauvegardes ont été créées.</span><span class="sxs-lookup"><span data-stu-id="1e71b-119">**Created On** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="1e71b-120">**Type** : les jeux de sauvegarde peuvent être des instantanés locaux ou des instantanés cloud.</span><span class="sxs-lookup"><span data-stu-id="1e71b-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="1e71b-121">Un instantané local est une sauvegarde de toutes les données de volume stockées localement sur l’appareil, tandis qu’un instantané cloud correspond à la sauvegarde des données de volume résidant dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="1e71b-121">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="1e71b-122">Les instantanés locaux offrent un accès plus rapide, alors que les instantanés cloud sont choisis pour la résilience des données.</span><span class="sxs-lookup"><span data-stu-id="1e71b-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="1e71b-123">**Initié par** : les sauvegardes peuvent être lancées automatiquement par une planification ou manuellement par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1e71b-123">**Initiated By** – The backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="1e71b-124">Vous pouvez utiliser une stratégie de sauvegarde pour planifier des sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="1e71b-124">You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="1e71b-125">Vous pouvez également utiliser l'option **Effectuer une sauvegarde** pour effectuer une sauvegarde manuelle.</span><span class="sxs-lookup"><span data-stu-id="1e71b-125">Alternatively, you can use the **Take backup** option to take a manual backup.</span></span>

## <a name="list-backup-sets-for-a-volume"></a><span data-ttu-id="1e71b-126">Répertorier les jeux de sauvegarde pour un volume</span><span class="sxs-lookup"><span data-stu-id="1e71b-126">List backup sets for a volume</span></span>
<span data-ttu-id="1e71b-127">Procédez comme suit pour répertorier toutes les sauvegardes pour un volume.</span><span class="sxs-lookup"><span data-stu-id="1e71b-127">Complete the following steps to list all the backups for a volume.</span></span>

#### <a name="to-list-backup-sets"></a><span data-ttu-id="1e71b-128">Pour répertorier les jeux de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="1e71b-128">To list backup sets</span></span>
1. <span data-ttu-id="1e71b-129">Dans la page du service StorSimple Manager, cliquez sur l’onglet **Catalogue de sauvegarde** .</span><span class="sxs-lookup"><span data-stu-id="1e71b-129">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="1e71b-130">Filtrez les sélections comme suit :</span><span class="sxs-lookup"><span data-stu-id="1e71b-130">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="1e71b-131">Sélectionnez l’appareil approprié.</span><span class="sxs-lookup"><span data-stu-id="1e71b-131">Select the appropriate device.</span></span>
   2. <span data-ttu-id="1e71b-132">Dans la liste déroulante, choisissez un volume pour afficher les sauvegardes correspondantes.</span><span class="sxs-lookup"><span data-stu-id="1e71b-132">In the drop-down list, choose a volume to view the corresponding the backups.</span></span>
   3. <span data-ttu-id="1e71b-133">Indiquez l’intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="1e71b-133">Specify the time range.</span></span>
   4. <span data-ttu-id="1e71b-134">Cliquez sur l’icône en forme de coche </span><span class="sxs-lookup"><span data-stu-id="1e71b-134">Click the check icon</span></span> ![Icône en forme de coche](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="1e71b-136">pour exécuter cette requête.</span><span class="sxs-lookup"><span data-stu-id="1e71b-136">to execute this query.</span></span>
      
      <span data-ttu-id="1e71b-137">Les sauvegardes associées au volume sélectionné doivent figurer dans la liste des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="1e71b-137">The backups associated with the selected volume should appear in the list of backup sets.</span></span>

## <a name="select-a-backup-set"></a><span data-ttu-id="1e71b-138">Sélectionner un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="1e71b-138">Select a backup set</span></span>
<span data-ttu-id="1e71b-139">Procédez comme suit pour sélectionner un jeu de sauvegarde pour un volume ou une stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="1e71b-139">Complete the following steps to select a backup set for a volume or backup policy.</span></span>

#### <a name="to-select-a-backup-set"></a><span data-ttu-id="1e71b-140">Pour sélectionner un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="1e71b-140">To select a backup set</span></span>
1. <span data-ttu-id="1e71b-141">Dans la page du service StorSimple Manager, cliquez sur l’onglet **Catalogue de sauvegarde** .</span><span class="sxs-lookup"><span data-stu-id="1e71b-141">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="1e71b-142">Filtrez les sélections comme suit :</span><span class="sxs-lookup"><span data-stu-id="1e71b-142">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="1e71b-143">Sélectionnez l’appareil approprié.</span><span class="sxs-lookup"><span data-stu-id="1e71b-143">Select the appropriate device.</span></span>
   2. <span data-ttu-id="1e71b-144">Dans la liste déroulante, choisissez la stratégie de sauvegarde ou le volume pour la sauvegarde à sélectionner.</span><span class="sxs-lookup"><span data-stu-id="1e71b-144">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="1e71b-145">Indiquez l’intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="1e71b-145">Specify the time range.</span></span>
   4. <span data-ttu-id="1e71b-146">Cliquez sur l’icône en forme de coche </span><span class="sxs-lookup"><span data-stu-id="1e71b-146">Click the check icon</span></span> ![Icône en forme de coche](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="1e71b-148">pour exécuter cette requête.</span><span class="sxs-lookup"><span data-stu-id="1e71b-148">to execute this query.</span></span>
      
      <span data-ttu-id="1e71b-149">Les sauvegardes associées au volume ou à la stratégie de sauvegarde sélectionné doivent figurer dans la liste des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="1e71b-149">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="1e71b-150">Sélectionnez un jeu de sauvegarde et développez-le.</span><span class="sxs-lookup"><span data-stu-id="1e71b-150">Select and expand a backup set.</span></span> <span data-ttu-id="1e71b-151">Les options **Restaurer** et **Supprimer** apparaissent en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="1e71b-151">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="1e71b-152">Vous pouvez effectuer une de ces actions sur le jeu de sauvegarde que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="1e71b-152">You can perform either of these actions on the backup set that you selected.</span></span>

## <a name="delete-a-backup-set"></a><span data-ttu-id="1e71b-153">Supprimer un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="1e71b-153">Delete a backup set</span></span>
<span data-ttu-id="1e71b-154">Supprimez une sauvegarde quand vous ne souhaitez plus conserver les données qui lui sont associées.</span><span class="sxs-lookup"><span data-stu-id="1e71b-154">Delete a backup when you no longer wish to retain the data associated with it.</span></span> <span data-ttu-id="1e71b-155">Procédez comme suit pour supprimer un jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="1e71b-155">Perform the following steps to delete a backup set.</span></span>

#### <a name="to-delete-a-backup-set"></a><span data-ttu-id="1e71b-156">Pour supprimer un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="1e71b-156">To delete a backup set</span></span>
1. <span data-ttu-id="1e71b-157">Dans la page du service StorSimple Manager, cliquez sur l’onglet **Catalogue de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="1e71b-157">On the StorSimple Manager service page, click the **Backup Catalog tab**.</span></span>
2. <span data-ttu-id="1e71b-158">Filtrez les sélections comme suit :</span><span class="sxs-lookup"><span data-stu-id="1e71b-158">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="1e71b-159">Sélectionnez l’appareil approprié.</span><span class="sxs-lookup"><span data-stu-id="1e71b-159">Select the appropriate device.</span></span>
   2. <span data-ttu-id="1e71b-160">Dans la liste déroulante, choisissez la stratégie de sauvegarde ou le volume pour la sauvegarde à sélectionner.</span><span class="sxs-lookup"><span data-stu-id="1e71b-160">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="1e71b-161">Indiquez l’intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="1e71b-161">Specify the time range.</span></span>
   4. <span data-ttu-id="1e71b-162">Cliquez sur l’icône en forme de coche </span><span class="sxs-lookup"><span data-stu-id="1e71b-162">Click the check icon</span></span> ![Icône en forme de coche](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="1e71b-164">pour exécuter cette requête.</span><span class="sxs-lookup"><span data-stu-id="1e71b-164">to execute this query.</span></span>
      
      <span data-ttu-id="1e71b-165">Les sauvegardes associées au volume ou à la stratégie de sauvegarde sélectionné doivent figurer dans la liste des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="1e71b-165">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="1e71b-166">Sélectionnez un jeu de sauvegarde et développez-le.</span><span class="sxs-lookup"><span data-stu-id="1e71b-166">Select and expand a backup set.</span></span> <span data-ttu-id="1e71b-167">Les options **Restaurer** et **Supprimer** apparaissent en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="1e71b-167">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="1e71b-168">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="1e71b-168">Click **Delete**.</span></span>
4. <span data-ttu-id="1e71b-169">Vous serez informé de la progression de la suppression et de son issue.</span><span class="sxs-lookup"><span data-stu-id="1e71b-169">You will be notified when the deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="1e71b-170">Une fois la suppression terminée, actualisez la requête dans cette page.</span><span class="sxs-lookup"><span data-stu-id="1e71b-170">After the deletion is done, refresh the query on this page.</span></span> <span data-ttu-id="1e71b-171">Le jeu de sauvegarde supprimé n’apparaîtra plus dans la liste des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="1e71b-171">The deleted backup set will no longer appear in the list of backup sets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e71b-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1e71b-172">Next steps</span></span>
* <span data-ttu-id="1e71b-173">Découvrez comment [utiliser le catalogue de sauvegarde pour restaurer l’appareil à partir d’un jeu de sauvegarde](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="1e71b-173">Learn how to [use the backup catalog to restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="1e71b-174">Découvrez comment [utiliser le service StorSimple Manager pour gérer votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="1e71b-174">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

