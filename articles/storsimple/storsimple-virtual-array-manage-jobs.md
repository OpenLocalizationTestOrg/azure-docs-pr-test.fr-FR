---
title: "aaaView et gérer des tâches de StorSimple Virtual Array | Documents Microsoft"
description: "Décrit la page de travaux du service de gestionnaire de périphérique StorSimple hello et comment toouse il tootrack des travaux récents et en cours pour hello StorSimple Virtual Array."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a><span data-ttu-id="f5a92-103">Utilisez des tâches de tooview de service de gestionnaire de périphériques StorSimple hello pour hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="f5a92-103">Use hello StorSimple Device Manager service tooview jobs for hello StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="f5a92-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f5a92-104">Overview</span></span>
<span data-ttu-id="f5a92-105">Hello **travaux** panneau fournit un portail centralisé unique pour afficher et gérer des travaux qui est démarrés sur les réseaux virtuels sont connecté tooyour service du Gestionnaire de périphériques StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f5a92-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="f5a92-106">Vous pouvez consulter les tâches en cours d’exécution, terminées et en échec pour plusieurs appareils virtuels.</span><span class="sxs-lookup"><span data-stu-id="f5a92-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="f5a92-107">Les résultats sont présentés sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="f5a92-107">Results are presented in a tabular format.</span></span>

![Panneau Tâches](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="f5a92-109">Vous pouvez rechercher rapidement les travaux qui hello que vous intéressent en filtrant sur des champs tels que :</span><span class="sxs-lookup"><span data-stu-id="f5a92-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="f5a92-110">**Intervalle de temps** – travaux peuvent être filtrées hello en fonction de date et la plage horaire.</span><span class="sxs-lookup"><span data-stu-id="f5a92-110">**Time range** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="f5a92-111">**Appareils** – travaux sont initiés sur un service de tooyour périphérique connecté.</span><span class="sxs-lookup"><span data-stu-id="f5a92-111">**Devices** – Jobs are initiated on a specific device connected tooyour service.</span></span> <span data-ttu-id="f5a92-112">Hello travaux filtrés est ensuite sous forme de tableau en fonction de hello suivant d’attributs :</span><span class="sxs-lookup"><span data-stu-id="f5a92-112">hello filtered jobs are then tabulated based on hello following attributes:</span></span>
  
  * <span data-ttu-id="f5a92-113">**Nom** – nom de la tâche hello peut être **tous les**, **sauvegarde**, **Clone**, **basculer**, **télécharger les mises à jour** , ou **installer les mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="f5a92-113">**Name** – hello job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="f5a92-114">**État** : l’état des tâches peut présenter la valeur **Toutes**, **En cours**, **Réussite**, **Échec** ou **Annulé**.</span><span class="sxs-lookup"><span data-stu-id="f5a92-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="f5a92-115">**Entité** – les travaux hello peuvent être associés à un volume, partage ou périphérique.</span><span class="sxs-lookup"><span data-stu-id="f5a92-115">**Entity** – hello jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="f5a92-116">**APPAREIL** hello – nom de l’appareil hello sur quel hello travail a été démarré.</span><span class="sxs-lookup"><span data-stu-id="f5a92-116">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="f5a92-117">**Démarré sur** – heure hello auxquelles hello travail a démarré.</span><span class="sxs-lookup"><span data-stu-id="f5a92-117">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="f5a92-118">**Durée** : hello durée sur laquelle travail hello a été exécutée.</span><span class="sxs-lookup"><span data-stu-id="f5a92-118">**Duration** – hello duration for on which hello job was run.</span></span>
* <span data-ttu-id="f5a92-119">**État** : vous pouvez rechercher la totalité des tâches ou celles en cours d’exécution, terminées ou en échec.</span><span class="sxs-lookup"><span data-stu-id="f5a92-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="f5a92-120">**Type de tâche** – type de tâche hello peut être all, sauvegarde, restauration, basculement, télécharger des mises à jour ou installer des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="f5a92-120">**Job type** – hello job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="f5a92-121">Hello de la liste des travaux est actualisée toutes les 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="f5a92-121">hello list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="f5a92-122">Affichage des détails d’une tâche</span><span class="sxs-lookup"><span data-stu-id="f5a92-122">View job details</span></span>
<span data-ttu-id="f5a92-123">Effectuer hello suivant détaille de hello tooview étapes d’un travail.</span><span class="sxs-lookup"><span data-stu-id="f5a92-123">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="f5a92-124">Détails de la tâche tooview</span><span class="sxs-lookup"><span data-stu-id="f5a92-124">tooview job details</span></span>
1. <span data-ttu-id="f5a92-125">Sur hello **travaux** panneau, une ou plusieurs tâches hello affichage vous intéressent en exécutant une requête avec les filtres appropriés.</span><span class="sxs-lookup"><span data-stu-id="f5a92-125">On hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="f5a92-126">Vous pouvez rechercher des tâches terminées ou en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f5a92-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="f5a92-127">Sélectionnez une tâche à partir de la liste tabulaire de hello des tâches.</span><span class="sxs-lookup"><span data-stu-id="f5a92-127">Select a job from hello tabular list of jobs.</span></span>
   
    ![Panneau Tâches](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="f5a92-129">Au bas de hello de page de hello, cliquez sur **détails**.</span><span class="sxs-lookup"><span data-stu-id="f5a92-129">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="f5a92-130">Bonjour **détails** boîte de dialogue, vous pouvez afficher le statut, les détails et les statistiques de temps.</span><span class="sxs-lookup"><span data-stu-id="f5a92-130">In hello **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="f5a92-131">Hello l’illustration suivante montre un exemple de hello **détails de la tâche sauvegarde** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f5a92-131">hello following illustration shows an example of hello **Backup Job Details** dialog box.</span></span>
   
    ![Détails du travail](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a><span data-ttu-id="f5a92-133">Échecs des tâches lors de la machine virtuelle de hello est suspendu dans hello hyperviseur</span><span class="sxs-lookup"><span data-stu-id="f5a92-133">Job failures when hello virtual machine is paused in hello hypervisor</span></span>
<span data-ttu-id="f5a92-134">Lorsqu’une tâche est en cours sur votre StorSimple Virtual Array et le périphérique de hello (ordinateur virtuel configuré dans l’hyperviseur) est en pause est supérieure à 15 minutes, échec du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="f5a92-134">When a job is in progress on your StorSimple Virtual Array and hello device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, hello job fails.</span></span> <span data-ttu-id="f5a92-135">Cela en raison du temps de StorSimple Virtual Array tooyour est synchronisée avec l’heure de Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f5a92-135">This is due tooyour StorSimple Virtual Array time being out of sync with hello Microsoft Azure time.</span></span> 

<span data-ttu-id="f5a92-136">Vous verrez hello l’erreur suivante : « votre heure de l’appareil est synchronisé avec le temps de Microsoft Azure hello de plus de 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="f5a92-136">You will see hello following error: "Your device time is out of sync with hello Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="f5a92-137">Vérifiez que hello hyperviseur et les heures d’unité de hello sont synchronisées avec un serveur NTP.</span><span class="sxs-lookup"><span data-stu-id="f5a92-137">Ensure that hello hypervisor and hello device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="f5a92-138">Verify that there are no connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="f5a92-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="f5a92-139">tootroubleshoot des problèmes de connectivité, exécutez les tests de diagnostic à partir de hello local interface utilisateur web de votre appareil virtuel. »</span><span class="sxs-lookup"><span data-stu-id="f5a92-139">tootroubleshoot connectivity issues, run diagnostic tests from hello local web UI of your virtual device."</span></span>

<span data-ttu-id="f5a92-140">Ces échecs s’appliquent à des travaux toobackup, de restauration, de mise à jour et de basculement.</span><span class="sxs-lookup"><span data-stu-id="f5a92-140">These failures apply toobackup, restore, update, and failover jobs.</span></span> <span data-ttu-id="f5a92-141">Si votre machine virtuelle est configurée dans Hyper-V, machine de hello synchronise finalement heure avec votre hyperviseur.</span><span class="sxs-lookup"><span data-stu-id="f5a92-141">If your virtual machine is provisioned in Hyper-V, hello machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="f5a92-142">Une fois que ce sera le cas, vous pourrez redémarrer votre tâche.</span><span class="sxs-lookup"><span data-stu-id="f5a92-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5a92-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f5a92-143">Next steps</span></span>
<span data-ttu-id="f5a92-144">[Découvrez comment toouse hello tooadminister de l’interface utilisateur web locale votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="f5a92-144">[Learn how toouse hello local web UI tooadminister your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

