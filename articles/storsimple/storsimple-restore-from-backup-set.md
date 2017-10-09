---
title: "un volume StorSimple à partir de la sauvegarde d’aaaRestore | Documents Microsoft"
description: "Explique comment toouse hello StorSimple Manager service catalogue de sauvegarde page toorestore un volume StorSimple à partir d’un jeu de sauvegarde."
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
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="9874e-103">Restauration d’un volume StorSimple à partir d’un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9874e-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="9874e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9874e-104">Overview</span></span>
<span data-ttu-id="9874e-105">Hello **catalogue de sauvegarde** page affiche tous les jeux de sauvegarde hello qui sont créés lorsque des sauvegardes manuelles ou automatisées sont effectuées.</span><span class="sxs-lookup"><span data-stu-id="9874e-105">hello **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="9874e-106">Vous pouvez utiliser cette toolist page toutes les sauvegardes hello pour une stratégie de sauvegarde ou un volume, sélectionnez ou supprimer les sauvegardes, ou utiliser une sauvegarde toorestore ou cloner un volume.</span><span class="sxs-lookup"><span data-stu-id="9874e-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

 ![Page Catalogue de sauvegarde](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="9874e-108">Ce didacticiel explique comment toouse hello **catalogue de sauvegarde** page toorestore un volume sur votre appareil à partir d’un jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9874e-108">This tutorial explains how toouse hello **Backup Catalog** page toorestore a volume on your device from a backup set.</span></span>

## <a name="how-toouse-hello-backup-catalog"></a><span data-ttu-id="9874e-109">Comment toouse hello catalogue de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9874e-109">How toouse hello backup catalog</span></span>
<span data-ttu-id="9874e-110">Hello **catalogue de sauvegarde** page fournit une requête qui vous permet de toonarrow votre sélection du jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9874e-110">hello **Backup Catalog** page provides a query that helps you toonarrow your backup set selection.</span></span> <span data-ttu-id="9874e-111">Vous pouvez filtrer hello jeux de sauvegarde qui est récupérés en fonction de hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="9874e-111">You can filter hello backup sets that are retrieved based on hello following parameters:</span></span>

* <span data-ttu-id="9874e-112">**APPAREIL** – périphérique hello sur quel hello jeu de sauvegarde a été créé.</span><span class="sxs-lookup"><span data-stu-id="9874e-112">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="9874e-113">**Stratégie de sauvegarde** ou **volume** – hello stratégie de sauvegarde ou volume associé à ce jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9874e-113">**Backup policy** or **volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="9874e-114">**À partir de** et **à** : hello plage de date et heure de création de jeu de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="9874e-114">**From** and **To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="9874e-115">Hello jeux de sauvegarde filtrés sont ensuite sous forme de tableau en fonction de hello suivant des attributs :</span><span class="sxs-lookup"><span data-stu-id="9874e-115">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="9874e-116">**Nom** hello – nom de la stratégie de sauvegarde hello ou volume associé au jeu de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="9874e-116">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="9874e-117">**Taille** – hello taille réelle du jeu de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="9874e-117">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="9874e-118">**Créé sur** : date de hello et l’heure de création des sauvegardes de hello.</span><span class="sxs-lookup"><span data-stu-id="9874e-118">**Created on** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="9874e-119">**Type** : les jeux de sauvegarde peuvent être des instantanés locaux ou des instantanés cloud.</span><span class="sxs-lookup"><span data-stu-id="9874e-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="9874e-120">Un instantané local est une sauvegarde de toutes vos données de volume stockées localement sur le périphérique de hello, tandis qu’un instantané cloud fait référence sauvegarde toohello des données de volume résidant dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="9874e-120">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="9874e-121">Les instantanés locaux offrent un accès plus rapide, alors que les instantanés cloud sont choisis pour la résilience des données.</span><span class="sxs-lookup"><span data-stu-id="9874e-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="9874e-122">**Initié par** : les sauvegardes hello peuvent être lancées automatiquement en fonction de tooa planification ou manuellement par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9874e-122">**Initiated by** – hello backups can be initiated automatically according tooa schedule or manually by a user.</span></span> <span data-ttu-id="9874e-123">(Vous pouvez utiliser les sauvegardes tooschedule stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9874e-123">(You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="9874e-124">Vous pouvez également utiliser hello **sauvegarde** option tootake une sauvegarde interactive.)</span><span class="sxs-lookup"><span data-stu-id="9874e-124">Alternatively, you can use hello **Take backup** option tootake an interactive backup.)</span></span>

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="9874e-125">Comment toorestore votre volume StorSimple à partir d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9874e-125">How toorestore your StorSimple volume from a backup</span></span>
<span data-ttu-id="9874e-126">Vous pouvez utiliser hello **catalogue de sauvegarde** page toorestore votre volume StorSimple à partir d’une sauvegarde spécifique.</span><span class="sxs-lookup"><span data-stu-id="9874e-126">You can use hello **Backup Catalog** page toorestore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="9874e-127">Restauration à partir d’une sauvegarde remplace les volumes existants hello à partir de la sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="9874e-127">Restoring from a backup will replace hello existing volumes from hello backup.</span></span> <span data-ttu-id="9874e-128">Cela peut entraîner une perte de hello de toutes les données écrites après que hello sauvegarde a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="9874e-128">This may cause hello loss of any data that was written after hello backup was taken.</span></span>
> 
> 

<span data-ttu-id="9874e-129">Avant de lancer une restauration sur un volume, vérifiez que le volume de hello est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="9874e-129">Before you initiate a restore on a volume, ensure that hello volume is offline.</span></span> <span data-ttu-id="9874e-130">Vous devez tout d’abord les volumes hello tootake hors connexion sur l’ordinateur hôte de hello et puis hello appareil.</span><span class="sxs-lookup"><span data-stu-id="9874e-130">You will need tootake hello volume offline on hello host first and then hello device.</span></span> <span data-ttu-id="9874e-131">Suivez les étapes de hello dans [mettre un volume hors connexion](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="9874e-131">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="9874e-132">Effectuer hello suivant les étapes toorestore un volume à partir d’un jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9874e-132">Perform hello following steps toorestore a volume from a backup set.</span></span>

### <a name="toorestore-from-a-backup-set"></a><span data-ttu-id="9874e-133">toorestore à partir d’un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9874e-133">toorestore from a backup set</span></span>
1. <span data-ttu-id="9874e-134">Sur la page du service StorSimple Manager hello, cliquez sur hello **catalogue de sauvegarde** onglet.</span><span class="sxs-lookup"><span data-stu-id="9874e-134">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
   
    ![Catalogue de sauvegarde](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="9874e-136">Sélectionnez un jeu de sauvegarde comme suit :</span><span class="sxs-lookup"><span data-stu-id="9874e-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="9874e-137">Sélectionnez le périphérique approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="9874e-137">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="9874e-138">Dans la liste déroulante hello, choisissez que vous souhaitez tooselect la stratégie de sauvegarde ou volume hello pour la sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="9874e-138">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="9874e-139">Spécifiez la plage de temps hello.</span><span class="sxs-lookup"><span data-stu-id="9874e-139">Specify hello time range.</span></span>
   4. <span data-ttu-id="9874e-140">Cliquez sur une icône de coche hello</span><span class="sxs-lookup"><span data-stu-id="9874e-140">Click hello check icon</span></span> ![icône en forme de coche](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="9874e-142">tooexecute cette requête.</span><span class="sxs-lookup"><span data-stu-id="9874e-142">tooexecute this query.</span></span>
      
      <span data-ttu-id="9874e-143">Hello sauvegardes associées de stratégie de sauvegarde ou volume hello sélectionné doivent apparaître dans la liste hello des jeux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9874e-143">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="9874e-144">Développez hello jeu de sauvegarde tooview hello associée des volumes.</span><span class="sxs-lookup"><span data-stu-id="9874e-144">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="9874e-145">Ces volumes doivent être mis hors connexion sur l’hôte de hello et de périphérique avant de les restaurer.</span><span class="sxs-lookup"><span data-stu-id="9874e-145">These volumes must be taken offline on hello host and device before you can restore them.</span></span> <span data-ttu-id="9874e-146">Suivez les étapes de hello dans [mettre un volume hors connexion](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="9874e-146">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="9874e-147">Assurez-vous que vous avez effectué des volumes hello hors connexion sur l’ordinateur hôte de hello tout d’abord, avant de mettre hors connexion les volumes hello sur le périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="9874e-147">Make sure that you have taken hello volumes offline on hello host first, before you take hello volumes offline on hello device.</span></span> <span data-ttu-id="9874e-148">Si vous ne prenez pas les volumes hello hors connexion sur l’ordinateur hôte de hello, il pourrait endommager toodata corruption.</span><span class="sxs-lookup"><span data-stu-id="9874e-148">If you do not take hello volumes offline on hello host, it could potentially lead toodata corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="9874e-149">Sélectionnez un jeu de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9874e-149">Select a backup set.</span></span> <span data-ttu-id="9874e-150">Cliquez sur **restaurer** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="9874e-150">Click **Restore** at hello bottom of hello page.</span></span>
5. <span data-ttu-id="9874e-151">Vous êtes invité à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="9874e-151">You will be prompted for confirmation.</span></span> 
   
    ![Page Confirmation](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="9874e-153">Passez en revue les informations de restauration hello et cliquez sur une icône de coche hello ![icône de coche](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span><span class="sxs-lookup"><span data-stu-id="9874e-153">Review hello restore information and click hello check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="9874e-154">Ceci lancera un travail de restauration que vous pouvez afficher en accédant à hello **travaux** page.</span><span class="sxs-lookup"><span data-stu-id="9874e-154">This will initiate a restore job that you can view by accessing hello **Jobs** page.</span></span> 
7. <span data-ttu-id="9874e-155">Une fois la restauration de hello est terminée, vous pouvez vérifier que le contenu hello de vos volumes est remplacés par les volumes de sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="9874e-155">After hello restore is complete, you can verify that hello contents of your volumes are replaced by volumes from hello backup.</span></span>

<span data-ttu-id="9874e-156">![Vidéo disponible](./media/storsimple-restore-from-backup-set/Video_icon.png)**Vidéo disponible**</span><span class="sxs-lookup"><span data-stu-id="9874e-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="9874e-157">toowatch une vidéo qui montre comment vous pouvez utiliser hello clone et restaurer les fonctionnalités dans les fichiers de StorSimple toorecover supprimé, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="9874e-157">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9874e-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9874e-158">Next steps</span></span>
* <span data-ttu-id="9874e-159">Découvrez comment trop[StorSimple de gérer les volumes](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="9874e-159">Learn how too[Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="9874e-160">Découvrez comment trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="9874e-160">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

