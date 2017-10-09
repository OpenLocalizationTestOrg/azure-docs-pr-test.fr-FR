---
title: "aaaManage vos stratégies de sauvegarde StorSimple | Documents Microsoft"
description: "Explique comment vous pouvez utiliser toocreate de service StorSimple Manager hello et gérer des sauvegardes manuelles, des planifications de sauvegarde et la rétention de sauvegarde."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a><span data-ttu-id="6c22a-103">Utiliser des stratégies de sauvegarde hello StorSimple Manager service toomanage</span><span class="sxs-lookup"><span data-stu-id="6c22a-103">Use hello StorSimple Manager service toomanage backup policies</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="6c22a-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6c22a-104">Overview</span></span>
<span data-ttu-id="6c22a-105">Ce didacticiel explique comment toouse hello service StorSimple Manager **les stratégies de sauvegarde** page toocontrol les processus de sauvegarde et de rétention de sauvegarde pour vos volumes StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6c22a-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="6c22a-106">Elle décrit également comment toocomplete une sauvegarde manuelle.</span><span class="sxs-lookup"><span data-stu-id="6c22a-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="6c22a-107">Hello **les stratégies de sauvegarde** page vous permet de toomanage les stratégies de sauvegarde et planification local et les instantanés cloud.</span><span class="sxs-lookup"><span data-stu-id="6c22a-107">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="6c22a-108">(Les stratégies de sauvegarde sont tooconfigure utilisé les planifications de sauvegarde et de rétention de sauvegarde pour une collection de volumes). Stratégies de sauvegarde permettent de tootake un instantané de plusieurs volumes simultanément.</span><span class="sxs-lookup"><span data-stu-id="6c22a-108">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="6c22a-109">Cela signifie que les sauvegardes de hello créées par une stratégie de sauvegarde sera copies cohérentes en cas d’incident.</span><span class="sxs-lookup"><span data-stu-id="6c22a-109">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="6c22a-110">Cette page répertorie les stratégies de sauvegarde hello, leurs types, les volumes de hello associé, le nombre de hello de sauvegardes conservées et hello option tooenable ces stratégies.</span><span class="sxs-lookup"><span data-stu-id="6c22a-110">This page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="6c22a-111">Hello **les stratégies de sauvegarde** page vous permet également de toofilter hello stratégies de sauvegarde existantes par un ou plusieurs des hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="6c22a-111">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="6c22a-112">**Nom de la stratégie** : hello nom associé à la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="6c22a-112">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="6c22a-113">Hello différents types de stratégies sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="6c22a-113">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="6c22a-114">Stratégies planifiées, créées explicitement par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="6c22a-114">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="6c22a-115">Stratégies automatiques, qui sont créés lors de la sauvegarde par défaut de hello pour cette option de volume a été activée lors de la création du volume hello.</span><span class="sxs-lookup"><span data-stu-id="6c22a-115">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="6c22a-116">Ces stratégies sont nommés Nomvolume_pardéfaut où nom de Volume fait référence nom toohello Hello volume StorSimple configuré par l’utilisateur hello Bonjour portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="6c22a-116">These policies are named as VolumeName_Default where Volume name refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="6c22a-117">Hello les stratégies automatiques génèrent des instantanés cloud quotidiens commençant à l’heure de l’appareil 22:30.</span><span class="sxs-lookup"><span data-stu-id="6c22a-117">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="6c22a-118">Stratégies importées, initialement créées dans hello Gestionnaire d’instantanés StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6c22a-118">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="6c22a-119">Ils ont une balise qui décrit l’hôte de gestionnaire d’instantanés StorSimple de hello stratégies de hello ont été importées à partir de.</span><span class="sxs-lookup"><span data-stu-id="6c22a-119">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="6c22a-120">**Volumes** – hello volumes associés à la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="6c22a-120">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="6c22a-121">Tous les volumes de hello sont associés à une stratégie de sauvegarde sont regroupés ensemble lorsque les sauvegardes sont créées.</span><span class="sxs-lookup"><span data-stu-id="6c22a-121">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="6c22a-122">**Dernière sauvegarde réussie** : hello date et heure de hello dernière sauvegarde réussie qui a été effectuée avec cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="6c22a-122">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="6c22a-123">**Sauvegarde suivante** : hello date et heure de hello la prochaine sauvegarde planifiée qui sera initiée par cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="6c22a-123">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="6c22a-124">**Planifications** – hello nombre de planifications associées à stratégie de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="6c22a-124">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="6c22a-125">opérations Hello plus fréquemment que vous pouvez effectuer à partir de cette page sont :</span><span class="sxs-lookup"><span data-stu-id="6c22a-125">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="6c22a-126">Ajout d’une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="6c22a-126">Add a backup policy</span></span> 
* <span data-ttu-id="6c22a-127">Ajouter ou modifier une planification</span><span class="sxs-lookup"><span data-stu-id="6c22a-127">Add or modify a schedule</span></span> 
* <span data-ttu-id="6c22a-128">Supprimer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="6c22a-128">Delete a backup policy</span></span> 
* <span data-ttu-id="6c22a-129">Exécuter une sauvegarde manuelle</span><span class="sxs-lookup"><span data-stu-id="6c22a-129">Take a manual backup</span></span> 
* <span data-ttu-id="6c22a-130">Créer une stratégie de sauvegarde personnalisée comportant plusieurs volumes et planifications</span><span class="sxs-lookup"><span data-stu-id="6c22a-130">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="6c22a-131">Ajout d’une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="6c22a-131">Add a backup policy</span></span>
<span data-ttu-id="6c22a-132">Ajouter une planification de tooautomatically de stratégie de sauvegarde de vos sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="6c22a-132">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="6c22a-133">Effectuer hello Bonjour tooadd portail classique Azure une stratégie de sauvegarde de votre appareil StorSimple comme suit.</span><span class="sxs-lookup"><span data-stu-id="6c22a-133">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="6c22a-134">Après avoir ajouté la stratégie de hello, vous pouvez définir une planification (consultez [ajouter ou modifier une planification](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="6c22a-134">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

<span data-ttu-id="6c22a-135">![Vidéo disponible](./media/storsimple-manage-backup-policies/Video_icon.png)**Vidéo disponible**</span><span class="sxs-lookup"><span data-stu-id="6c22a-135">![Video available](./media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="6c22a-136">toowatch une vidéo qui montre comment toocreate local ou cloud de sauvegarde stratégie, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="6c22a-136">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="6c22a-137">Ajouter ou modifier une planification</span><span class="sxs-lookup"><span data-stu-id="6c22a-137">Add or modify a schedule</span></span>
<span data-ttu-id="6c22a-138">Vous pouvez ajouter ou modifier une planification qui est attaché tooan stratégie de sauvegarde existant sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6c22a-138">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="6c22a-139">Effectuer hello Bonjour tooadd de portail classique Azure comme suit ou modifier une planification.</span><span class="sxs-lookup"><span data-stu-id="6c22a-139">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="6c22a-140">Supprimer une stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="6c22a-140">Delete a backup policy</span></span>
<span data-ttu-id="6c22a-141">Effectuer hello suivant les étapes décrites dans hello toodelete portail classique Azure une stratégie de sauvegarde sur votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6c22a-141">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="6c22a-142">Exécuter une sauvegarde manuelle</span><span class="sxs-lookup"><span data-stu-id="6c22a-142">Take a manual backup</span></span>
<span data-ttu-id="6c22a-143">Effectuer hello comme suit dans la sauvegarde (manuel) de hello toocreate portail classique Azure une demande pour un volume unique.</span><span class="sxs-lookup"><span data-stu-id="6c22a-143">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="6c22a-144">Créer une stratégie de sauvegarde personnalisée comportant plusieurs volumes et planifications</span><span class="sxs-lookup"><span data-stu-id="6c22a-144">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="6c22a-145">Effectuer hello Bonjour toocreate portail classique Azure une stratégie de sauvegarde personnalisée qui a plusieurs volumes et planifications, comme suit.</span><span class="sxs-lookup"><span data-stu-id="6c22a-145">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a><span data-ttu-id="6c22a-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c22a-146">Next steps</span></span>
<span data-ttu-id="6c22a-147">En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6c22a-147">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

