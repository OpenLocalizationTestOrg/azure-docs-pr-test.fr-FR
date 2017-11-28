---
title: "Restauration d’un volume StorSimple à partir d’une sauvegarde | Microsoft Docs"
description: "Explique comment utiliser la page Catalogue de sauvegarde du service StorSimple Manager pour restaurer un volume StorSimple à partir d’un jeu de sauvegarde."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 12484338f5b4d489604d70a657ef0992b6267297
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="4d569-103">Restauration d’un volume StorSimple à partir d’un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="4d569-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="4d569-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4d569-104">Overview</span></span>
<span data-ttu-id="4d569-105">La page **Catalogue de sauvegarde** affiche tous les jeux de sauvegarde créés lors de sauvegardes manuelles ou automatisées.</span><span class="sxs-lookup"><span data-stu-id="4d569-105">The **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="4d569-106">Vous pouvez utiliser cette page pour répertorier toutes les sauvegardes pour une stratégie de sauvegarde ou un volume, sélectionner ou supprimer des sauvegardes, ou utiliser une sauvegarde pour restaurer ou cloner un volume.</span><span class="sxs-lookup"><span data-stu-id="4d569-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

 ![Page Catalogue de sauvegarde](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="4d569-108">Ce didacticiel explique comment utiliser la page **Catalogue de sauvegarde** pour restaurer un volume sur l’appareil à partir d’un jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4d569-108">This tutorial explains how to use the **Backup Catalog** page to restore a volume on your device from a backup set.</span></span>

## <a name="how-to-use-the-backup-catalog"></a><span data-ttu-id="4d569-109">Utilisation du catalogue de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="4d569-109">How to use the backup catalog</span></span>
<span data-ttu-id="4d569-110">La page **Catalogue de sauvegarde** comprend une zone de requête qui vous permet d’affiner la sélection des ensembles de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4d569-110">The **Backup Catalog** page provides a query that helps you to narrow your backup set selection.</span></span> <span data-ttu-id="4d569-111">Vous pouvez filtrer les jeux de sauvegarde récupérés selon les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="4d569-111">You can filter the backup sets that are retrieved based on the following parameters:</span></span>

* <span data-ttu-id="4d569-112">**Appareil** : appareil sur lequel le jeu de sauvegarde a été créé.</span><span class="sxs-lookup"><span data-stu-id="4d569-112">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="4d569-113">**Stratégie de sauvegarde** ou **volume** : stratégie de sauvegarde ou volume associé à ce jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4d569-113">**Backup policy** or **volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="4d569-114">**De** et **À** : plage de dates et d’heures de création du jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4d569-114">**From** and **To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="4d569-115">Les jeux de sauvegarde filtrés sont ensuite affichés sous forme de tableau sur la base des attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="4d569-115">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="4d569-116">**Nom** : nom de la stratégie de sauvegarde ou du volume associé à ce jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4d569-116">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="4d569-117">**Taille** : taille réelle du jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4d569-117">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="4d569-118">**Créé le** : date et heure auxquelles les sauvegardes ont été créées.</span><span class="sxs-lookup"><span data-stu-id="4d569-118">**Created on** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="4d569-119">**Type** : les jeux de sauvegarde peuvent être des instantanés locaux ou des instantanés cloud.</span><span class="sxs-lookup"><span data-stu-id="4d569-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="4d569-120">Un instantané local est une sauvegarde de toutes les données de volume stockées localement sur l’appareil, tandis qu’un instantané cloud correspond à la sauvegarde des données de volume résidant dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="4d569-120">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="4d569-121">Les instantanés locaux offrent un accès plus rapide, alors que les instantanés cloud sont choisis pour la résilience des données.</span><span class="sxs-lookup"><span data-stu-id="4d569-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="4d569-122">**Initié par** : les sauvegardes peuvent être lancées automatiquement suivant une planification ou manuellement par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4d569-122">**Initiated by** – The backups can be initiated automatically according to a schedule or manually by a user.</span></span> <span data-ttu-id="4d569-123">(Vous pouvez utiliser une stratégie de sauvegarde pour planifier des sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="4d569-123">(You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="4d569-124">Vous pouvez également utiliser l’option **Effectuer une sauvegarde** pour effectuer une sauvegarde interactive.)</span><span class="sxs-lookup"><span data-stu-id="4d569-124">Alternatively, you can use the **Take backup** option to take an interactive backup.)</span></span>

## <a name="how-to-restore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="4d569-125">Comment restaurer votre volume StorSimple à partir d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="4d569-125">How to restore your StorSimple volume from a backup</span></span>
<span data-ttu-id="4d569-126">Vous pouvez utiliser la page **Catalogue de sauvegarde** pour restaurer votre volume StorSimple à partir d’une sauvegarde spécifique.</span><span class="sxs-lookup"><span data-stu-id="4d569-126">You can use the **Backup Catalog** page to restore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="4d569-127">La restauration à partir d’une sauvegarde remplace les volumes existants à partir de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4d569-127">Restoring from a backup will replace the existing volumes from the backup.</span></span> <span data-ttu-id="4d569-128">Cela peut entraîner la perte des données qui ont été écrites après la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4d569-128">This may cause the loss of any data that was written after the backup was taken.</span></span>
> 
> 

<span data-ttu-id="4d569-129">Avant de lancer la restauration d’un volume, assurez-vous que celui-ci est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="4d569-129">Before you initiate a restore on a volume, ensure that the volume is offline.</span></span> <span data-ttu-id="4d569-130">Vous devrez mettre le volume hors connexion sur l’ordinateur hôte en premier, puis sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4d569-130">You will need to take the volume offline on the host first and then the device.</span></span> <span data-ttu-id="4d569-131">Suivez les étapes de la [Mise hors connexion d’un volume](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="4d569-131">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="4d569-132">Procédez comme suit pour restaurer un volume à partir d’un jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4d569-132">Perform the following steps to restore a volume from a backup set.</span></span>

### <a name="to-restore-from-a-backup-set"></a><span data-ttu-id="4d569-133">Pour restaurer à partir d’un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="4d569-133">To restore from a backup set</span></span>
1. <span data-ttu-id="4d569-134">Dans la page du service StorSimple Manager, cliquez sur l’onglet **Catalogue de sauvegarde** .</span><span class="sxs-lookup"><span data-stu-id="4d569-134">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
   
    ![Catalogue de sauvegarde](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="4d569-136">Sélectionnez un jeu de sauvegarde comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d569-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="4d569-137">Sélectionnez l’appareil approprié.</span><span class="sxs-lookup"><span data-stu-id="4d569-137">Select the appropriate device.</span></span>
   2. <span data-ttu-id="4d569-138">Dans la liste déroulante, choisissez la stratégie de sauvegarde ou le volume pour la sauvegarde à sélectionner.</span><span class="sxs-lookup"><span data-stu-id="4d569-138">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="4d569-139">Indiquez l’intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="4d569-139">Specify the time range.</span></span>
   4. <span data-ttu-id="4d569-140">Cliquez sur l’icône en forme de coche </span><span class="sxs-lookup"><span data-stu-id="4d569-140">Click the check icon</span></span> ![icône en forme de coche](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="4d569-142">pour exécuter cette requête.</span><span class="sxs-lookup"><span data-stu-id="4d569-142">to execute this query.</span></span>
      
      <span data-ttu-id="4d569-143">Les sauvegardes associées au volume ou à la stratégie de sauvegarde sélectionné doivent figurer dans la liste des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4d569-143">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="4d569-144">Développez le jeu de sauvegarde pour afficher les volumes associés.</span><span class="sxs-lookup"><span data-stu-id="4d569-144">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="4d569-145">Ces volumes doivent être mis hors connexion sur l’hôte et l’appareil avant leur restauration.</span><span class="sxs-lookup"><span data-stu-id="4d569-145">These volumes must be taken offline on the host and device before you can restore them.</span></span> <span data-ttu-id="4d569-146">Suivez les étapes de la [Mise hors connexion d’un volume](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="4d569-146">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="4d569-147">Veillez à mettre les volumes hors connexion sur l’ordinateur hôte avant de les mettre hors connexion sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4d569-147">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span></span> <span data-ttu-id="4d569-148">Sans quoi, vous vous exposez à un risque d’altération des données.</span><span class="sxs-lookup"><span data-stu-id="4d569-148">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="4d569-149">Sélectionnez un jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4d569-149">Select a backup set.</span></span> <span data-ttu-id="4d569-150">Cliquez sur **Restaurer** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="4d569-150">Click **Restore** at the bottom of the page.</span></span>
5. <span data-ttu-id="4d569-151">Vous êtes invité à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="4d569-151">You will be prompted for confirmation.</span></span> 
   
    ![Page Confirmation](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="4d569-153">Passez en revue les informations de restauration, puis cliquez sur l’icône en forme de coche ![icône en forme de coche](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span><span class="sxs-lookup"><span data-stu-id="4d569-153">Review the restore information and click the check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="4d569-154">Cette opération lance une tâche de restauration que vous pouvez afficher en accédant à la page **Tâches** .</span><span class="sxs-lookup"><span data-stu-id="4d569-154">This will initiate a restore job that you can view by accessing the **Jobs** page.</span></span> 
7. <span data-ttu-id="4d569-155">Une fois la restauration terminée, vous pouvez vérifier que le contenu de vos volumes a été remplacé par les volumes provenant de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4d569-155">After the restore is complete, you can verify that the contents of your volumes are replaced by volumes from the backup.</span></span>

<span data-ttu-id="4d569-156">![Vidéo disponible](./media/storsimple-restore-from-backup-set/Video_icon.png) **Vidéo disponible**</span><span class="sxs-lookup"><span data-stu-id="4d569-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="4d569-157">Pour visionner une vidéo expliquant comment utiliser les fonctionnalités de clonage et de restauration dans StorSimple pour récupérer des fichiers supprimés, cliquez [ici](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="4d569-157">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d569-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d569-158">Next steps</span></span>
* <span data-ttu-id="4d569-159">Découvrez comment [gérer des volumes StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="4d569-159">Learn how to [Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="4d569-160">Découvrez comment [utiliser le service StorSimple Manager pour gérer votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="4d569-160">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

