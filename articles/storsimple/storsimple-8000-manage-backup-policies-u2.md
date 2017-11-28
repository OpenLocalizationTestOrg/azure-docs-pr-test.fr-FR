---
title: "stratégies de sauvegarde aaaManage StorSimple 8000 series | Documents Microsoft"
description: "Explique comment vous pouvez utiliser toocreate de service de gestionnaire de périphériques StorSimple hello et gérer des sauvegardes manuelles, de planifications de sauvegarde et de rétention des sauvegardes sur un appareil de série StorSimple 8000."
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a><span data-ttu-id="5ad83-103">Utiliser le service du Gestionnaire de périphériques StorSimple hello dans les stratégies de sauvegarde toomanage portail Azure</span><span class="sxs-lookup"><span data-stu-id="5ad83-103">Use hello StorSimple Device Manager service in Azure portal toomanage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="5ad83-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5ad83-104">Overview</span></span>

<span data-ttu-id="5ad83-105">Ce didacticiel explique comment toouse hello service du Gestionnaire de périphériques StorSimple **stratégie de sauvegarde** les processus de sauvegarde toocontrol lame et de rétention de sauvegarde pour vos volumes StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5ad83-105">This tutorial explains how toouse hello StorSimple Device Manager service **Backup policy** blade toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="5ad83-106">Elle décrit également comment toocomplete une sauvegarde manuelle.</span><span class="sxs-lookup"><span data-stu-id="5ad83-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="5ad83-107">Lorsque vous sauvegardez un volume, vous pouvez choisir toocreate un instantané local ou un instantané cloud.</span><span class="sxs-lookup"><span data-stu-id="5ad83-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="5ad83-108">Si vous sauvegardez un volume épinglé localement, nous vous recommandons de spécifier un instantané cloud.</span><span class="sxs-lookup"><span data-stu-id="5ad83-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="5ad83-109">Le fait de prendre un grand nombre d'instantanés locaux d’un volume épinglé localement associé à un jeu de données qui possède une attrition élevée entraîne une situation dans laquelle vous pourriez rapidement manquer d'espace local.</span><span class="sxs-lookup"><span data-stu-id="5ad83-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="5ad83-110">Si vous choisissez tootake instantanés locaux, nous vous recommandons que vous occupent moins tooback instantanés quotidiens de l’état le plus récent hello, les conservez pendant un jour, puis supprimez.</span><span class="sxs-lookup"><span data-stu-id="5ad83-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="5ad83-111">Lorsque vous prenez un instantané cloud d’un volume attaché localement, vous copiez uniquement hello modifié données toohello dans le cloud, où il est dédupliqué et compressé.</span><span class="sxs-lookup"><span data-stu-id="5ad83-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span>

## <a name="hello-backup-policy-blade"></a><span data-ttu-id="5ad83-112">panneau Hello de la stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="5ad83-112">hello Backup policy blade</span></span>

<span data-ttu-id="5ad83-113">Hello **stratégie de sauvegarde** Panneau de votre appareil StorSimple vous permet de toomanage les stratégies de sauvegarde et planification local et les instantanés cloud.</span><span class="sxs-lookup"><span data-stu-id="5ad83-113">hello **Backup policy** blade for your StorSimple device allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="5ad83-114">Stratégies de sauvegarde sont tooconfigure utilisé les planifications de sauvegarde et de rétention des sauvegardes pour un ensemble de volumes.</span><span class="sxs-lookup"><span data-stu-id="5ad83-114">Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="5ad83-115">Stratégies de sauvegarde permettent de tootake un instantané de plusieurs volumes simultanément.</span><span class="sxs-lookup"><span data-stu-id="5ad83-115">Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="5ad83-116">Cela signifie que les sauvegardes de hello créées par une stratégie de sauvegarde sera copies cohérentes en cas d’incident.</span><span class="sxs-lookup"><span data-stu-id="5ad83-116">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="5ad83-117">Liste tabulaire des stratégies de sauvegarde de Hello permet également de vous toofilter hello stratégies de sauvegarde existantes par un ou plusieurs des hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="5ad83-117">hello backup policies tabular listing also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="5ad83-118">**Nom de la stratégie** : hello nom associé à la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="5ad83-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="5ad83-119">Hello différents types de stratégies sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="5ad83-119">hello different types of policies include:</span></span>

  * <span data-ttu-id="5ad83-120">Stratégies planifiées, créées explicitement par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="5ad83-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="5ad83-121">Stratégies importées, initialement créées dans hello Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5ad83-121">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="5ad83-122">Ils ont une balise qui décrit l’hôte de gestionnaire d’instantanés StorSimple de hello stratégies de hello ont été importées à partir de.</span><span class="sxs-lookup"><span data-stu-id="5ad83-122">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5ad83-123">Stratégies de sauvegarde automatique ou par défaut ne sont plus activés lors de la création du volume hello.</span><span class="sxs-lookup"><span data-stu-id="5ad83-123">Automatic or default backup policies are no longer enabled at hello time of volume creation.</span></span>

* <span data-ttu-id="5ad83-124">**Dernière sauvegarde réussie** : hello date et heure de hello dernière sauvegarde réussie qui a été effectuée avec cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="5ad83-124">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="5ad83-125">**Sauvegarde suivante** : hello date et heure de hello la prochaine sauvegarde planifiée qui sera initiée par cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="5ad83-125">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="5ad83-126">**Volumes** – hello volumes associés à la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="5ad83-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="5ad83-127">Tous les volumes de hello sont associés à une stratégie de sauvegarde sont regroupés ensemble lorsque les sauvegardes sont créées.</span><span class="sxs-lookup"><span data-stu-id="5ad83-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="5ad83-128">**Planifications** – hello nombre de planifications associées à stratégie de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="5ad83-128">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="5ad83-129">opérations Hello plus fréquemment que vous pouvez effectuer pour les stratégies de sauvegarde sont :</span><span class="sxs-lookup"><span data-stu-id="5ad83-129">hello frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="5ad83-130">Ajout d’une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="5ad83-130">Add a backup policy</span></span>
* <span data-ttu-id="5ad83-131">Ajouter ou modifier une planification</span><span class="sxs-lookup"><span data-stu-id="5ad83-131">Add or modify a schedule</span></span>
* <span data-ttu-id="5ad83-132">Ajouter ou supprimer un volume</span><span class="sxs-lookup"><span data-stu-id="5ad83-132">Add or remove a volume</span></span>
* <span data-ttu-id="5ad83-133">Supprimer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="5ad83-133">Delete a backup policy</span></span>
* <span data-ttu-id="5ad83-134">Exécuter une sauvegarde manuelle</span><span class="sxs-lookup"><span data-stu-id="5ad83-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="5ad83-135">Ajout d’une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="5ad83-135">Add a backup policy</span></span>

<span data-ttu-id="5ad83-136">Ajouter une planification de tooautomatically de stratégie de sauvegarde de vos sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="5ad83-136">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="5ad83-137">Lorsque vous créez un volume, aucune stratégie de sauvegarde par défaut n’est associée à votre volume.</span><span class="sxs-lookup"><span data-stu-id="5ad83-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="5ad83-138">Vous devez tooadd et affectez un stratégie de sauvegarde tooprotect volume de données.</span><span class="sxs-lookup"><span data-stu-id="5ad83-138">You need tooadd and assign a backup policy tooprotect volume data.</span></span>

<span data-ttu-id="5ad83-139">Effectuer hello Bonjour tooadd portail Azure pour votre appareil StorSimple une stratégie de sauvegarde comme suit.</span><span class="sxs-lookup"><span data-stu-id="5ad83-139">Perform hello following steps in hello Azure portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="5ad83-140">Après avoir ajouté la stratégie de hello, vous pouvez définir une planification (consultez [ajouter ou modifier une planification](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="5ad83-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="5ad83-141">Ajouter ou modifier une planification</span><span class="sxs-lookup"><span data-stu-id="5ad83-141">Add or modify a schedule</span></span>

<span data-ttu-id="5ad83-142">Vous pouvez ajouter ou modifier une planification qui est attaché tooan stratégie de sauvegarde existant sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5ad83-142">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="5ad83-143">Effectuer hello comme suit dans hello tooadd portail Azure ou modifier une planification.</span><span class="sxs-lookup"><span data-stu-id="5ad83-143">Perform hello following steps in hello Azure portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="5ad83-144">Ajouter ou supprimer un volume</span><span class="sxs-lookup"><span data-stu-id="5ad83-144">Add or remove a volume</span></span>

<span data-ttu-id="5ad83-145">Vous pouvez ajouter ou supprimer un volume stratégie de sauvegarde tooa sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5ad83-145">You can add or remove a volume assigned tooa backup policy on your StorSimple device.</span></span> <span data-ttu-id="5ad83-146">Effectuer hello comme suit dans hello tooadd portail Azure ou supprimer un volume.</span><span class="sxs-lookup"><span data-stu-id="5ad83-146">Perform hello following steps in hello Azure portal tooadd or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="5ad83-147">Supprimer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="5ad83-147">Delete a backup policy</span></span>

<span data-ttu-id="5ad83-148">Effectuer hello suivant les étapes décrites dans hello toodelete portail Azure une stratégie de sauvegarde sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5ad83-148">Perform hello following steps in hello Azure portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="5ad83-149">Exécuter une sauvegarde manuelle</span><span class="sxs-lookup"><span data-stu-id="5ad83-149">Take a manual backup</span></span>

<span data-ttu-id="5ad83-150">Effectuer hello comme suit dans la sauvegarde (manuel) de hello toocreate portail Azure une demande pour un volume unique.</span><span class="sxs-lookup"><span data-stu-id="5ad83-150">Perform hello following steps in hello Azure portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="5ad83-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5ad83-151">Next steps</span></span>

<span data-ttu-id="5ad83-152">En savoir plus sur [à l’aide de hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="5ad83-152">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

