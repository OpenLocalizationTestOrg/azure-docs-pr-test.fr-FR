---
title: "Gérer votre catalogue de sauvegarde StorSimple | Microsoft Docs"
description: "Explique comment utiliser la page Catalogue de sauvegarde du service StorSimple Device Manager pour répertorier, sélectionner et supprimer des jeux de sauvegarde."
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
ms.openlocfilehash: ac2577c6cd350d6d437d55e61ec73d954cb24893
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-your-backup-catalog"></a><span data-ttu-id="6618f-103">Utiliser le service StorSimple Device Manager pour gérer votre catalogue de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="6618f-103">Use the StorSimple Device Manager service to manage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="6618f-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6618f-104">Overview</span></span>
<span data-ttu-id="6618f-105">Le panneau **Catalogue de sauvegarde** du service StorSimple Device Manager affiche tous les jeux de sauvegarde créés lors de sauvegardes manuelles ou planifiées.</span><span class="sxs-lookup"><span data-stu-id="6618f-105">The StorSimple Device Manager service **Backup Catalog** blade displays all the backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="6618f-106">Vous pouvez utiliser cette page pour répertorier toutes les sauvegardes pour une stratégie de sauvegarde ou un volume, sélectionner ou supprimer des sauvegardes, ou utiliser une sauvegarde pour restaurer ou cloner un volume.</span><span class="sxs-lookup"><span data-stu-id="6618f-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

<span data-ttu-id="6618f-107">Ce didacticiel explique comment répertorier, sélectionner et supprimer un jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-107">This tutorial explains how to list, select, and delete a backup set.</span></span> <span data-ttu-id="6618f-108">Pour savoir comment restaurer votre appareil à partir d’une sauvegarde, accédez à [Restaurer l’appareil à partir d’un jeu de sauvegarde](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="6618f-108">To learn how to restore your device from backup, go to [Restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span> <span data-ttu-id="6618f-109">Pour découvrir comment cloner un volume, accédez à [Cloner un volume StorSimple](storsimple-8000-clone-volume-u2.md).</span><span class="sxs-lookup"><span data-stu-id="6618f-109">To learn how to clone a volume, go to [Clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>

![Catalogue de sauvegarde](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

<span data-ttu-id="6618f-111">Le panneau **Catalogue de sauvegarde** comprend une zone de requête pour affiner la sélection des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-111">The **Backup Catalog** blade provides a query to narrow your backup set selection.</span></span> <span data-ttu-id="6618f-112">Vous pouvez filtrer les jeux de sauvegarde récupérés selon les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="6618f-112">You can filter the backup sets that are retrieved, based on the following parameters:</span></span>

* <span data-ttu-id="6618f-113">**Appareil** : appareil sur lequel le jeu de sauvegarde a été créé.</span><span class="sxs-lookup"><span data-stu-id="6618f-113">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="6618f-114">**Stratégie de sauvegarde ou volume** : stratégie de sauvegarde ou volume associé à ce jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-114">**Backup policy or Volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="6618f-115">**De et À** : plage de dates et d’heures de création du jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-115">**From and To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="6618f-116">Les jeux de sauvegarde filtrés sont ensuite affichés sous forme de tableau sur la base des attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="6618f-116">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="6618f-117">**Nom** : nom de la stratégie de sauvegarde ou du volume associé à ce jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-117">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="6618f-118">**Taille** : taille réelle du jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-118">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="6618f-119">**Créé le** : date et heure auxquelles les sauvegardes ont été créées.</span><span class="sxs-lookup"><span data-stu-id="6618f-119">**Created On** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="6618f-120">**Type** : les jeux de sauvegarde peuvent être des instantanés locaux ou des instantanés cloud.</span><span class="sxs-lookup"><span data-stu-id="6618f-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="6618f-121">Un instantané local est une sauvegarde de toutes les données de volume stockées localement sur l’appareil, tandis qu’un instantané cloud correspond à la sauvegarde des données de volume résidant dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="6618f-121">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="6618f-122">Les instantanés locaux offrent un accès plus rapide, alors que les instantanés cloud sont choisis pour la résilience des données.</span><span class="sxs-lookup"><span data-stu-id="6618f-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="6618f-123">**Initié par** : les sauvegardes peuvent être lancées automatiquement par une planification ou manuellement par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6618f-123">**Initiated By** – The backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="6618f-124">Vous pouvez utiliser une stratégie de sauvegarde pour planifier des sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="6618f-124">You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="6618f-125">Vous pouvez également utiliser l'option **Effectuer une sauvegarde** pour effectuer une sauvegarde manuelle.</span><span class="sxs-lookup"><span data-stu-id="6618f-125">Alternatively, you can use the **Take backup** option to take a manual backup.</span></span>

## <a name="list-backup-sets-for-a-backup-policy"></a><span data-ttu-id="6618f-126">Répertorier les jeux de sauvegarde pour une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="6618f-126">List backup sets for a backup policy</span></span>
<span data-ttu-id="6618f-127">Procédez comme suit pour répertorier toutes les sauvegardes pour une stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-127">Complete the following steps to list all the backups for a backup policy.</span></span>

#### <a name="to-list-backup-sets"></a><span data-ttu-id="6618f-128">Pour répertorier les jeux de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="6618f-128">To list backup sets</span></span>
1. <span data-ttu-id="6618f-129">Accédez à votre service StorSimple Device Manager et cliquez sur **Catalogue de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="6618f-129">Go to your StorSimple Device Manager service and click **Backup catalog**.</span></span>

2. <span data-ttu-id="6618f-130">Filtrez les sélections comme suit :</span><span class="sxs-lookup"><span data-stu-id="6618f-130">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="6618f-131">Indiquez l’intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="6618f-131">Specify the time range.</span></span>
   2. <span data-ttu-id="6618f-132">Sélectionnez l’appareil approprié.</span><span class="sxs-lookup"><span data-stu-id="6618f-132">Select the appropriate device.</span></span>
   3. <span data-ttu-id="6618f-133">Filtrez par **Stratégie de sauvegarde** pour afficher les sauvegardes correspondantes.</span><span class="sxs-lookup"><span data-stu-id="6618f-133">Filter by **Backup policy** to view the corresponding the backups.</span></span>
   3. <span data-ttu-id="6618f-134">Dans la liste déroulante de la stratégie de sauvegarde, choisissez **Tout** pour afficher toutes les sauvegardes sur l’appareil sélectionné.</span><span class="sxs-lookup"><span data-stu-id="6618f-134">From the backup policy dropdown list, choose **All** to view all the backups on the selected device.</span></span>
   4. <span data-ttu-id="6618f-135">Cliquez sur **Appliquer** pour exécuter cette requête.</span><span class="sxs-lookup"><span data-stu-id="6618f-135">Click **Apply** to execute this query.</span></span>
      
      <span data-ttu-id="6618f-136">Les sauvegardes associées à la stratégie de sauvegarde sélectionnée doivent figurer dans la liste des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-136">The backups associated with the selected backup policy should appear in the list of backup sets.</span></span>

      ![Accéder au catalogue de sauvegarde](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a><span data-ttu-id="6618f-138">Sélectionner un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="6618f-138">Select a backup set</span></span>
<span data-ttu-id="6618f-139">Procédez comme suit pour sélectionner un jeu de sauvegarde pour un volume ou une stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-139">Complete the following steps to select a backup set for a volume or backup policy.</span></span>

#### <a name="to-select-a-backup-set"></a><span data-ttu-id="6618f-140">Pour sélectionner un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="6618f-140">To select a backup set</span></span>
1. <span data-ttu-id="6618f-141">Accédez à votre service StorSimple Device Manager et cliquez sur **Catalogue de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="6618f-141">Go to your StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="6618f-142">Filtrez les sélections comme suit :</span><span class="sxs-lookup"><span data-stu-id="6618f-142">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="6618f-143">Indiquez l’intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="6618f-143">Specify the time range.</span></span> 
   2. <span data-ttu-id="6618f-144">Sélectionnez l’appareil approprié.</span><span class="sxs-lookup"><span data-stu-id="6618f-144">Select the appropriate device.</span></span> 
   3. <span data-ttu-id="6618f-145">Filtrez par volume ou stratégie de sauvegarde pour la sauvegarde à sélectionner.</span><span class="sxs-lookup"><span data-stu-id="6618f-145">Filter by volume or backup policy for the backup that you wish to select.</span></span>
   4. <span data-ttu-id="6618f-146">Cliquez sur **Appliquer** pour exécuter cette requête.</span><span class="sxs-lookup"><span data-stu-id="6618f-146">Click **Apply** to execute this query.</span></span>
      
      <span data-ttu-id="6618f-147">Les sauvegardes associées au volume ou à la stratégie de sauvegarde sélectionné doivent figurer dans la liste des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-147">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>

      ![Accéder au catalogue de sauvegarde](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="6618f-149">Sélectionnez un jeu de sauvegarde et développez-le.</span><span class="sxs-lookup"><span data-stu-id="6618f-149">Select and expand a backup set.</span></span> <span data-ttu-id="6618f-150">Vous pouvez maintenant voir les jeux de sauvegarde répartis par les volumes qu’ils contiennent.</span><span class="sxs-lookup"><span data-stu-id="6618f-150">You can now see the backup sets broken down by the volumes that it contains.</span></span> <span data-ttu-id="6618f-151">Les options **Restaurer** et **Supprimer** sont disponibles via le menu contextuel (clic droit) du jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-151">The **Restore** and **Delete** options are available via the context menu (right-click) for the backup set.</span></span> <span data-ttu-id="6618f-152">Vous pouvez effectuer une de ces actions sur le jeu de sauvegarde que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="6618f-152">You can perform either of these actions on the backup set that you selected.</span></span>

    ![Accéder au catalogue de sauvegarde](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a><span data-ttu-id="6618f-154">Supprimer un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="6618f-154">Delete a backup set</span></span>
<span data-ttu-id="6618f-155">Supprimez une sauvegarde quand vous ne souhaitez plus conserver les données qui lui sont associées.</span><span class="sxs-lookup"><span data-stu-id="6618f-155">Delete a backup when you no longer wish to retain the data associated with it.</span></span> <span data-ttu-id="6618f-156">Procédez comme suit pour supprimer un jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-156">Perform the following steps to delete a backup set.</span></span>

#### <a name="to-delete-a-backup-set"></a><span data-ttu-id="6618f-157">Pour supprimer un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="6618f-157">To delete a backup set</span></span>
 <span data-ttu-id="6618f-158">Accédez à votre service StorSimple Device Manager et cliquez sur **Catalogue de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="6618f-158">Go to your StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="6618f-159">Filtrez les sélections comme suit :</span><span class="sxs-lookup"><span data-stu-id="6618f-159">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="6618f-160">Indiquez l’intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="6618f-160">Specify the time range.</span></span> 
   2. <span data-ttu-id="6618f-161">Sélectionnez l’appareil approprié.</span><span class="sxs-lookup"><span data-stu-id="6618f-161">Select the appropriate device.</span></span> 
   3. <span data-ttu-id="6618f-162">Filtrez par volume ou stratégie de sauvegarde pour la sauvegarde à sélectionner.</span><span class="sxs-lookup"><span data-stu-id="6618f-162">Filter by volume or backup policy for the backup that you wish to select.</span></span>
   4. <span data-ttu-id="6618f-163">Cliquez sur **Appliquer** pour exécuter cette requête.</span><span class="sxs-lookup"><span data-stu-id="6618f-163">Click **Apply** to execute this query.</span></span>
      
      <span data-ttu-id="6618f-164">Les sauvegardes associées au volume ou à la stratégie de sauvegarde sélectionné doivent figurer dans la liste des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-164">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>

      ![Accéder au catalogue de sauvegarde](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="6618f-166">Sélectionnez un jeu de sauvegarde et développez-le.</span><span class="sxs-lookup"><span data-stu-id="6618f-166">Select and expand a backup set.</span></span> <span data-ttu-id="6618f-167">Vous pouvez maintenant voir les jeux de sauvegarde répartis par les volumes qu’ils contiennent.</span><span class="sxs-lookup"><span data-stu-id="6618f-167">You can now see the backup sets broken down by the volumes that it contains.</span></span> <span data-ttu-id="6618f-168">Les options **Restaurer** et **Supprimer** sont disponibles via le menu contextuel (clic droit) du jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-168">The **Restore** and **Delete** options are available via the context menu (right-click) for the backup set.</span></span> <span data-ttu-id="6618f-169">Cliquez avec le bouton droit sur le jeu de sauvegarde sélectionné et sélectionnez **Supprimer** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="6618f-169">Right-click the selected backup set and from the context menu, select **Delete**.</span></span>

    ![Accéder au catalogue de sauvegarde](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. <span data-ttu-id="6618f-171">Lorsque vous êtes invité à confirmer l’opération, passez en revue les informations affichées et cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="6618f-171">When prompted for confirmation, review the displayed information and click **Delete**.</span></span> <span data-ttu-id="6618f-172">La sauvegarde sélectionnée est supprimée définitivement.</span><span class="sxs-lookup"><span data-stu-id="6618f-172">The selected backup is deleted permanently.</span></span>

    ![Accéder au catalogue de sauvegarde](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. <span data-ttu-id="6618f-174">Vous serez informé de la progression de la suppression et de son issue.</span><span class="sxs-lookup"><span data-stu-id="6618f-174">You will be notified when the deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="6618f-175">Une fois la suppression terminée, actualisez la requête dans cette page.</span><span class="sxs-lookup"><span data-stu-id="6618f-175">After the deletion is done, refresh the query on this page.</span></span> <span data-ttu-id="6618f-176">Le jeu de sauvegarde supprimé n’apparaîtra plus dans la liste des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6618f-176">The deleted backup set will no longer appear in the list of backup sets.</span></span>

    ![Accéder au catalogue de sauvegarde](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a><span data-ttu-id="6618f-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6618f-178">Next steps</span></span>
* <span data-ttu-id="6618f-179">Découvrez comment [utiliser le catalogue de sauvegarde pour restaurer l’appareil à partir d’un jeu de sauvegarde](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="6618f-179">Learn how to [use the backup catalog to restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="6618f-180">Découvrez comment [utiliser le service StorSimple Device Manager pour gérer votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6618f-180">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

