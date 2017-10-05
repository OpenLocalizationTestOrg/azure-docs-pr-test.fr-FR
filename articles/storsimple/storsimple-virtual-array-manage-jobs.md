---
title: "Afficher et gérer les tâches StorSimple Virtual Array | Microsoft Docs"
description: "Décrit la page Tâches du service StorSimple Device Manager et explique comment l’utiliser pour effectuer le suivi des tâches récentes et actuelles du StorSimple Virtual Array."
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
ms.openlocfilehash: 3fd1c262a8ce94d8e98f2b066a8028d974b15b1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-jobs-for-the-storsimple-virtual-array"></a><span data-ttu-id="545fa-103">Utiliser le service StorSimple Device Manager pour afficher les tâches du StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="545fa-103">Use the StorSimple Device Manager service to view jobs for the StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="545fa-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="545fa-104">Overview</span></span>
<span data-ttu-id="545fa-105">Le panneau **Tâches** offre un portail centralisé unique pour afficher et gérer les tâches qui sont lancées sur les Virtual Arrays connectés à votre service StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="545fa-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="545fa-106">Vous pouvez consulter les tâches en cours d’exécution, terminées et en échec pour plusieurs appareils virtuels.</span><span class="sxs-lookup"><span data-stu-id="545fa-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="545fa-107">Les résultats sont présentés sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="545fa-107">Results are presented in a tabular format.</span></span>

![Panneau Tâches](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="545fa-109">Vous pouvez rechercher rapidement les tâches qui vous intéressent en filtrant sur les champs, à savoir :</span><span class="sxs-lookup"><span data-stu-id="545fa-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="545fa-110">**Période** : les tâches peuvent être filtrées selon la date et l’heure.</span><span class="sxs-lookup"><span data-stu-id="545fa-110">**Time range** – Jobs can be filtered based on the date and time range.</span></span>
* <span data-ttu-id="545fa-111">**Appareils** : les tâches sont initiées sur un appareil spécifique connecté à votre service.</span><span class="sxs-lookup"><span data-stu-id="545fa-111">**Devices** – Jobs are initiated on a specific device connected to your service.</span></span> <span data-ttu-id="545fa-112">Les tâches filtrées sont ensuite affichées sous forme de tableau sur la base des attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="545fa-112">The filtered jobs are then tabulated based on the following attributes:</span></span>
  
  * <span data-ttu-id="545fa-113">**Nom** : le nom des tâches peut présenter la valeur **Toutes**, **Sauvegarder**, **Cloner**, **Effectuer un basculement**, **Télécharger les mises à jour** ou **Installer les mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="545fa-113">**Name** – The job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="545fa-114">**État** : l’état des tâches peut présenter la valeur **Toutes**, **En cours**, **Réussite**, **Échec** ou **Annulé**.</span><span class="sxs-lookup"><span data-stu-id="545fa-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="545fa-115">**Entité** : les tâches peuvent être associées à un volume, un partage ou un appareil.</span><span class="sxs-lookup"><span data-stu-id="545fa-115">**Entity** – The jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="545fa-116">**Appareil** : nom de l'appareil sur lequel la tâche a été lancée.</span><span class="sxs-lookup"><span data-stu-id="545fa-116">**Device** – The name of the device on which the job was started.</span></span>
  * <span data-ttu-id="545fa-117">**Démarré le** : heure à laquelle la tâche a été lancée.</span><span class="sxs-lookup"><span data-stu-id="545fa-117">**Started on** – The time when the job was started.</span></span>
  * <span data-ttu-id="545fa-118">**Durée**: durée d’exécution de la tâche.</span><span class="sxs-lookup"><span data-stu-id="545fa-118">**Duration** – The duration for on which the job was run.</span></span>
* <span data-ttu-id="545fa-119">**État** : vous pouvez rechercher la totalité des tâches ou celles en cours d’exécution, terminées ou en échec.</span><span class="sxs-lookup"><span data-stu-id="545fa-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="545fa-120">**Type de tâche** : le type de tâche peut présenter la valeur Toutes, Sauvegarder, Restaurer, Effectuer un basculement, Télécharger les mises à jour ou Installer les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="545fa-120">**Job type** – The job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="545fa-121">La liste des tâches est actualisée toutes les 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="545fa-121">The list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="545fa-122">Affichage des détails d’une tâche</span><span class="sxs-lookup"><span data-stu-id="545fa-122">View job details</span></span>
<span data-ttu-id="545fa-123">Pour afficher les détails d’une tâche, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="545fa-123">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="545fa-124">Pour afficher les détails d’une tâche</span><span class="sxs-lookup"><span data-stu-id="545fa-124">To view job details</span></span>
1. <span data-ttu-id="545fa-125">Dans le panneau **Tâches**, affichez la ou les tâches qui vous intéressent en exécutant une requête avec les filtres appropriés.</span><span class="sxs-lookup"><span data-stu-id="545fa-125">On the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="545fa-126">Vous pouvez rechercher des tâches terminées ou en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="545fa-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="545fa-127">Sélectionnez une tâche dans la liste des tâches sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="545fa-127">Select a job from the tabular list of jobs.</span></span>
   
    ![Panneau Tâches](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="545fa-129">En bas de la page, cliquez sur **Détails**.</span><span class="sxs-lookup"><span data-stu-id="545fa-129">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="545fa-130">La boîte de dialogue **Détails** indique l’état, les détails et les statistiques horaires.</span><span class="sxs-lookup"><span data-stu-id="545fa-130">In the **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="545fa-131">La figure suivante illustre la boîte de dialogue **Détails du travail Sauvegarde** .</span><span class="sxs-lookup"><span data-stu-id="545fa-131">The following illustration shows an example of the **Backup Job Details** dialog box.</span></span>
   
    ![Détails du travail](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-the-virtual-machine-is-paused-in-the-hypervisor"></a><span data-ttu-id="545fa-133">Échec des tâches lorsque la machine virtuelle est en pause dans l'hyperviseur</span><span class="sxs-lookup"><span data-stu-id="545fa-133">Job failures when the virtual machine is paused in the hypervisor</span></span>
<span data-ttu-id="545fa-134">Lorsqu’une tâche est en cours sur votre StorSimple Virtual Array et que l’appareil (machine virtuelle approvisionnée dans l’hyperviseur) est en pause pendant plus de 15 minutes, la tâche échoue.</span><span class="sxs-lookup"><span data-stu-id="545fa-134">When a job is in progress on your StorSimple Virtual Array and the device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, the job fails.</span></span> <span data-ttu-id="545fa-135">Ceci en raison du fait que l’heure de votre StorSimple Virtual Array est désynchronisée avec l'heure de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="545fa-135">This is due to your StorSimple Virtual Array time being out of sync with the Microsoft Azure time.</span></span> 

<span data-ttu-id="545fa-136">L’erreur suivante s’affiche : « Your device time is out of sync with the Microsoft Azure time by more than 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="545fa-136">You will see the following error: "Your device time is out of sync with the Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="545fa-137">Ensure that the hypervisor and the device times are synchronized with an NTP server.</span><span class="sxs-lookup"><span data-stu-id="545fa-137">Ensure that the hypervisor and the device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="545fa-138">Verify that there are no connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="545fa-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="545fa-139">To troubleshoot connectivity issues, run diagnostic tests from the local web UI of your virtual device. » (L’heure de votre appareil est désynchronisée de plus de 15 minutes par rapport à l’heure de Microsoft Azure. Assurez-vous que l’heure de l’hyperviseur et l’heure de l’appareil sont synchronisées à l’aide d’un serveur NTP. Vérifiez qu’il n’existe aucun problème de connectivité. Pour résoudre les problèmes de connectivité, exécutez des tests de diagnostic à partir de l’interface utilisateur web locale de votre appareil virtuel.)</span><span class="sxs-lookup"><span data-stu-id="545fa-139">To troubleshoot connectivity issues, run diagnostic tests from the local web UI of your virtual device."</span></span>

<span data-ttu-id="545fa-140">Cet échec concerne les tâches de sauvegarde, de restauration, de mise à jour et de basculement.</span><span class="sxs-lookup"><span data-stu-id="545fa-140">These failures apply to backup, restore, update, and failover jobs.</span></span> <span data-ttu-id="545fa-141">Si votre machine virtuelle est provisionnée dans Hyper-V, elle finit par synchroniser son heure avec celle de votre hyperviseur.</span><span class="sxs-lookup"><span data-stu-id="545fa-141">If your virtual machine is provisioned in Hyper-V, the machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="545fa-142">Une fois que ce sera le cas, vous pourrez redémarrer votre tâche.</span><span class="sxs-lookup"><span data-stu-id="545fa-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="545fa-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="545fa-143">Next steps</span></span>
<span data-ttu-id="545fa-144">[Découvrez comment utiliser l’interface utilisateur web locale pour gérer votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="545fa-144">[Learn how to use the local web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

