---
title: "aaaManage vos stratégies de sauvegarde StorSimple | Documents Microsoft"
description: "Explique comment vous pouvez utiliser toocreate de service StorSimple Manager hello et gérer des sauvegardes manuelles, des planifications de sauvegarde et la rétention de sauvegarde."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 4a2db707-bbfc-425c-bfeb-bc5c97781873
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 7b01f29a8d8a096d9890c8406557021317b9baff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies-update-2"></a><span data-ttu-id="519c0-103">Utilisez hello StorSimple Manager service toomanage stratégies de sauvegarde (Update 2)</span><span class="sxs-lookup"><span data-stu-id="519c0-103">Use hello StorSimple Manager service toomanage backup policies (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="519c0-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="519c0-104">Overview</span></span>
<span data-ttu-id="519c0-105">Ce didacticiel explique comment toouse hello service StorSimple Manager **les stratégies de sauvegarde** page toocontrol les processus de sauvegarde et de rétention de sauvegarde pour vos volumes StorSimple.</span><span class="sxs-lookup"><span data-stu-id="519c0-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="519c0-106">Elle décrit également comment toocomplete une sauvegarde manuelle.</span><span class="sxs-lookup"><span data-stu-id="519c0-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="519c0-107">Lorsque vous sauvegardez un volume, vous pouvez choisir toocreate un instantané local ou un instantané cloud.</span><span class="sxs-lookup"><span data-stu-id="519c0-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="519c0-108">Si vous sauvegardez un volume épinglé localement, nous vous recommandons de spécifier un instantané cloud.</span><span class="sxs-lookup"><span data-stu-id="519c0-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="519c0-109">Le fait de prendre un grand nombre d'instantanés locaux d’un volume épinglé localement associé à un jeu de données qui possède une attrition élevée entraîne une situation dans laquelle vous pourriez rapidement manquer d'espace local.</span><span class="sxs-lookup"><span data-stu-id="519c0-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="519c0-110">Si vous choisissez tootake instantanés locaux, nous vous recommandons que vous occupent moins tooback instantanés quotidiens de l’état le plus récent hello, les conservez pendant un jour, puis supprimez.</span><span class="sxs-lookup"><span data-stu-id="519c0-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="519c0-111">Lorsque vous prenez un instantané cloud d’un volume attaché localement, vous copiez uniquement hello modifié données toohello dans le cloud, où il est dédupliqué et compressé.</span><span class="sxs-lookup"><span data-stu-id="519c0-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span> 

## <a name="hello-backup-policies-page"></a><span data-ttu-id="519c0-112">page de stratégies de sauvegarde Hello</span><span class="sxs-lookup"><span data-stu-id="519c0-112">hello Backup Policies page</span></span>
<span data-ttu-id="519c0-113">Hello **les stratégies de sauvegarde** page vous permet de toomanage les stratégies de sauvegarde et planification local et les instantanés cloud.</span><span class="sxs-lookup"><span data-stu-id="519c0-113">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="519c0-114">(Les stratégies de sauvegarde sont tooconfigure utilisé les planifications de sauvegarde et de rétention de sauvegarde pour une collection de volumes). Stratégies de sauvegarde permettent de tootake un instantané de plusieurs volumes simultanément.</span><span class="sxs-lookup"><span data-stu-id="519c0-114">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="519c0-115">Cela signifie que les sauvegardes de hello créées par une stratégie de sauvegarde sera copies cohérentes en cas d’incident.</span><span class="sxs-lookup"><span data-stu-id="519c0-115">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="519c0-116">Hello **les stratégies de sauvegarde** page répertorie les stratégies de sauvegarde hello, leurs types, les volumes de hello associé, le nombre de hello de sauvegardes conservées, et hello option tooenable ces stratégies.</span><span class="sxs-lookup"><span data-stu-id="519c0-116">hello **Backup Policies** page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="519c0-117">Hello **les stratégies de sauvegarde** page vous permet également de toofilter hello stratégies de sauvegarde existantes par un ou plusieurs des hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="519c0-117">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="519c0-118">**Nom de la stratégie** : hello nom associé à la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="519c0-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="519c0-119">Hello différents types de stratégies sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="519c0-119">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="519c0-120">Stratégies planifiées, créées explicitement par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="519c0-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="519c0-121">Stratégies automatiques, qui sont créés lors de la sauvegarde par défaut de hello pour cette option de volume a été activée lors de la création du volume hello.</span><span class="sxs-lookup"><span data-stu-id="519c0-121">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="519c0-122">Ces stratégies sont nommées *NomVolume*_Default où *NomVolume* fait référence nom toohello Hello volume StorSimple configuré par l’utilisateur hello Bonjour portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="519c0-122">These policies are named as *VolumeName*_Default where *VolumeName* refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="519c0-123">Hello les stratégies automatiques génèrent des instantanés cloud quotidiens commençant à l’heure de l’appareil 22:30.</span><span class="sxs-lookup"><span data-stu-id="519c0-123">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="519c0-124">Stratégies importées, initialement créées dans hello Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="519c0-124">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="519c0-125">Ils ont une balise qui décrit l’hôte de gestionnaire d’instantanés StorSimple de hello stratégies de hello ont été importées à partir de.</span><span class="sxs-lookup"><span data-stu-id="519c0-125">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="519c0-126">**Volumes** – hello volumes associés à la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="519c0-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="519c0-127">Tous les volumes de hello sont associés à une stratégie de sauvegarde sont regroupés ensemble lorsque les sauvegardes sont créées.</span><span class="sxs-lookup"><span data-stu-id="519c0-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="519c0-128">**Dernière sauvegarde réussie** : hello date et heure de hello dernière sauvegarde réussie qui a été effectuée avec cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="519c0-128">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="519c0-129">**Sauvegarde suivante** : hello date et heure de hello la prochaine sauvegarde planifiée qui sera initiée par cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="519c0-129">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="519c0-130">**Planifications** – hello nombre de planifications associées à stratégie de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="519c0-130">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="519c0-131">opérations Hello plus fréquemment que vous pouvez effectuer à partir de cette page sont :</span><span class="sxs-lookup"><span data-stu-id="519c0-131">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="519c0-132">Ajout d’une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="519c0-132">Add a backup policy</span></span> 
* <span data-ttu-id="519c0-133">Ajouter ou modifier une planification</span><span class="sxs-lookup"><span data-stu-id="519c0-133">Add or modify a schedule</span></span> 
* <span data-ttu-id="519c0-134">Supprimer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="519c0-134">Delete a backup policy</span></span> 
* <span data-ttu-id="519c0-135">Exécuter une sauvegarde manuelle</span><span class="sxs-lookup"><span data-stu-id="519c0-135">Take a manual backup</span></span> 
* <span data-ttu-id="519c0-136">Créer une stratégie de sauvegarde personnalisée comportant plusieurs volumes et planifications</span><span class="sxs-lookup"><span data-stu-id="519c0-136">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="519c0-137">Ajout d’une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="519c0-137">Add a backup policy</span></span>
<span data-ttu-id="519c0-138">Ajouter une planification de tooautomatically de stratégie de sauvegarde de vos sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="519c0-138">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="519c0-139">Effectuer hello Bonjour tooadd portail classique Azure une stratégie de sauvegarde de votre appareil StorSimple comme suit.</span><span class="sxs-lookup"><span data-stu-id="519c0-139">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="519c0-140">Après avoir ajouté la stratégie de hello, vous pouvez définir une planification (consultez [ajouter ou modifier une planification](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="519c0-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

<span data-ttu-id="519c0-141">![Vidéo disponible](./media/storsimple-manage-backup-policies-u2/Video_icon.png)**Vidéo disponible**</span><span class="sxs-lookup"><span data-stu-id="519c0-141">![Video available](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="519c0-142">toowatch une vidéo qui montre comment toocreate local ou cloud de sauvegarde stratégie, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="519c0-142">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="519c0-143">Ajouter ou modifier une planification</span><span class="sxs-lookup"><span data-stu-id="519c0-143">Add or modify a schedule</span></span>
<span data-ttu-id="519c0-144">Vous pouvez ajouter ou modifier une planification qui est attaché tooan stratégie de sauvegarde existant sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="519c0-144">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="519c0-145">Effectuer hello Bonjour tooadd de portail classique Azure comme suit ou modifier une planification.</span><span class="sxs-lookup"><span data-stu-id="519c0-145">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="519c0-146">Supprimer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="519c0-146">Delete a backup policy</span></span>
<span data-ttu-id="519c0-147">Effectuer hello suivant les étapes décrites dans hello toodelete portail classique Azure une stratégie de sauvegarde sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="519c0-147">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="519c0-148">Exécuter une sauvegarde manuelle</span><span class="sxs-lookup"><span data-stu-id="519c0-148">Take a manual backup</span></span>
<span data-ttu-id="519c0-149">Effectuer hello comme suit dans la sauvegarde (manuel) de hello toocreate portail classique Azure une demande pour un volume unique.</span><span class="sxs-lookup"><span data-stu-id="519c0-149">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="519c0-150">Créer une stratégie de sauvegarde personnalisée comportant plusieurs volumes et planifications</span><span class="sxs-lookup"><span data-stu-id="519c0-150">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="519c0-151">Effectuer hello Bonjour toocreate portail classique Azure une stratégie de sauvegarde personnalisée qui a plusieurs volumes et planifications, comme suit.</span><span class="sxs-lookup"><span data-stu-id="519c0-151">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a><span data-ttu-id="519c0-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="519c0-152">Next steps</span></span>
<span data-ttu-id="519c0-153">En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="519c0-153">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>
