---
title: Didacticiel de sauvegarde de Microsoft Azure StorSimple Virtual Array | Microsoft Azure
description: "Décrit comment sauvegarder des partages et des volumes StorSimple Virtual Array."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c926f0c80ce56cac3106ad97ec3ec2e18a8e2cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="53fe9-103">Sauvegarde de partages ou de volumes sur votre StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="53fe9-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="53fe9-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="53fe9-104">Overview</span></span>

<span data-ttu-id="53fe9-105">StorSimple Virtual Array est un périphérique virtuel local de stockage cloud hybride qui peut être configuré comme un serveur de fichiers ou un serveur iSCSI.</span><span class="sxs-lookup"><span data-stu-id="53fe9-105">The StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="53fe9-106">Le tableau virtuel vous permet de créer des sauvegardes planifiées et manuelles de l’ensemble des partages ou des volumes sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="53fe9-106">The virtual array allows the user to create scheduled and manual backups of all the shares or volumes on the device.</span></span> <span data-ttu-id="53fe9-107">Configuré comme serveur de fichiers, il permet également la récupération au niveau de l’élément.</span><span class="sxs-lookup"><span data-stu-id="53fe9-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="53fe9-108">Ce didacticiel vous explique comment créer des sauvegardes planifiées et manuelles et effectuer une récupération au niveau de l’élément pour restaurer un fichier supprimé sur votre tableau virtuel.</span><span class="sxs-lookup"><span data-stu-id="53fe9-108">This tutorial describes how to create scheduled and manual backups and perform item-level recovery to restore a deleted file on your virtual array.</span></span>

<span data-ttu-id="53fe9-109">Ce didacticiel s’applique uniquement aux instances StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="53fe9-109">This tutorial applies to the StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="53fe9-110">Pour plus d’informations sur la gamme 8000, accédez à [Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md) (Créer une sauvegarde pour un appareil de la gamme 8000).</span><span class="sxs-lookup"><span data-stu-id="53fe9-110">For information on 8000 series, go to [Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="53fe9-111">Sauvegarder des partages et des volumes</span><span class="sxs-lookup"><span data-stu-id="53fe9-111">Back up shares and volumes</span></span>

<span data-ttu-id="53fe9-112">Les sauvegardes fournissent une protection jusqu’à une date et une heure, et optimisent la récupération tout en réduisant les délais de restauration pour les partages et les sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="53fe9-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="53fe9-113">Vous pouvez sauvegarder un partage ou un volume sur votre appareil StorSimple de deux manières : **planifiée** ou **manuelle**.</span><span class="sxs-lookup"><span data-stu-id="53fe9-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="53fe9-114">Chacune des méthodes est abordée dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="53fe9-114">Each of the methods is discussed in the following sections.</span></span>

## <a name="change-the-backup-start-time"></a><span data-ttu-id="53fe9-115">Modifier l’heure de début de la sauvegarde</span><span class="sxs-lookup"><span data-stu-id="53fe9-115">Change the backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="53fe9-116">Dans cette version, les sauvegardes planifiées sont créées à l’aide d’une stratégie par défaut qui s'exécute tous les jours à un moment précis et sauvegarde tous les partages ou volumes sur l'appareil.</span><span class="sxs-lookup"><span data-stu-id="53fe9-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all the shares or volumes on the device.</span></span> <span data-ttu-id="53fe9-117">Il n'est pour l’instant pas possible de créer des stratégies personnalisées pour les sauvegardes planifiées.</span><span class="sxs-lookup"><span data-stu-id="53fe9-117">It is not possible to create custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="53fe9-118">Votre instance StorSimple Virtual Array comporte une stratégie de sauvegarde par défaut qui démarre à une heure spécifique de la journée (22h30) et sauvegarde une fois par jour tous les partages ou volumes sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="53fe9-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all the shares or volumes on the device once a day.</span></span> <span data-ttu-id="53fe9-119">Vous pouvez modifier l'heure à laquelle la sauvegarde démarre, mais la fréquence et la durée de rétention (qui spécifie le nombre de sauvegardes à conserver) ne peuvent pas être modifiées.</span><span class="sxs-lookup"><span data-stu-id="53fe9-119">You can change the time at which the backup starts, but the frequency and the retention (which specifies the number of backups to retain) cannot be changed.</span></span> <span data-ttu-id="53fe9-120">Au cours de ces sauvegardes, l’ensemble de l’appareil virtuel est sauvegardé.</span><span class="sxs-lookup"><span data-stu-id="53fe9-120">During these backups, the entire virtual device is backed up.</span></span> <span data-ttu-id="53fe9-121">Cela pourrait affecter les performances de l’appareil et les charges de travail déployées dessus.</span><span class="sxs-lookup"><span data-stu-id="53fe9-121">This could potentially impact the performance of the device and affect the workloads deployed on the device.</span></span> <span data-ttu-id="53fe9-122">Par conséquent, nous vous recommandons de planifier ces sauvegardes pendant les heures creuses.</span><span class="sxs-lookup"><span data-stu-id="53fe9-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="53fe9-123">Pour modifier l’heure de début par défaut de la sauvegarde, suivez la procédure suivante dans le [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="53fe9-123">To change the default backup start time, perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="to-change-the-start-time-for-the-default-backup-policy"></a><span data-ttu-id="53fe9-124">Pour modifier l'heure de début de la stratégie de sauvegarde par défaut</span><span class="sxs-lookup"><span data-stu-id="53fe9-124">To change the start time for the default backup policy</span></span>

1. <span data-ttu-id="53fe9-125">Accédez à la page **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="53fe9-125">Go to **Devices**.</span></span> <span data-ttu-id="53fe9-126">La liste des appareils enregistrés avec votre service StorSimple Device Manager s’affiche.</span><span class="sxs-lookup"><span data-stu-id="53fe9-126">The list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![accéder à la page appareils](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="53fe9-128">Sélectionnez votre appareil, puis cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="53fe9-128">Select and click your device.</span></span> <span data-ttu-id="53fe9-129">Le panneau **Paramètres** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="53fe9-129">The **Settings** blade will be displayed.</span></span> <span data-ttu-id="53fe9-130">Accédez à **Gérer > Stratégies de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="53fe9-130">Go to **Manage > Backup policies**.</span></span>
   
    ![sélectionner votre appareil](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="53fe9-132">Dans le panneau **Stratégies de sauvegarde**, l’heure de début par défaut est 22:30.</span><span class="sxs-lookup"><span data-stu-id="53fe9-132">In the **Backup policies** blade, the default start time is 22:30.</span></span> <span data-ttu-id="53fe9-133">Vous pouvez spécifier la nouvelle heure de début de la sauvegarde quotidienne dans le fuseau horaire de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="53fe9-133">You can specify the new start time for the daily schedule in device time zone.</span></span>
   
    ![accéder aux stratégies de sauvegarde](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="53fe9-135">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="53fe9-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="53fe9-136">Exécuter une sauvegarde manuelle</span><span class="sxs-lookup"><span data-stu-id="53fe9-136">Take a manual backup</span></span>

<span data-ttu-id="53fe9-137">Outre les sauvegardes planifiées, vous pouvez à tout moment effectuer une sauvegarde manuelle (à la demande) sur les données de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="53fe9-137">In addition to scheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="to-create-a-manual-backup"></a><span data-ttu-id="53fe9-138">Création d’une sauvegarde manuelle</span><span class="sxs-lookup"><span data-stu-id="53fe9-138">To create a manual backup</span></span>

1. <span data-ttu-id="53fe9-139">Accédez à la page **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="53fe9-139">Go to **Devices**.</span></span> <span data-ttu-id="53fe9-140">Sélectionnez votre appareil, puis cliquez sur **...**, tout à droite sur la ligne sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="53fe9-140">Select your device and right-click **...** at the far right in the selected row.</span></span> <span data-ttu-id="53fe9-141">Dans le menu contextuel, sélectionnez **Take backup** (Effectuer la sauvegarde).</span><span class="sxs-lookup"><span data-stu-id="53fe9-141">From the context menu, select **Take backup**.</span></span>
   
    ![accéder à l’option d’exécution de la sauvegarde](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="53fe9-143">Dans le panneau **Take backup** (Effectuer la sauvegarde), cliquez sur **Take backup** (Effectuer la sauvegarde).</span><span class="sxs-lookup"><span data-stu-id="53fe9-143">In the **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="53fe9-144">Cette opération sauvegarde tous les partages sur le fichier de serveurs, ou l’ensemble des volumes sur votre serveur iSCSI.</span><span class="sxs-lookup"><span data-stu-id="53fe9-144">This will backup all the shares on the file server or all the volumes on your iSCSI server.</span></span> 
   
    ![démarrage de sauvegarde](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="53fe9-146">Une sauvegarde à la demande démarre ; vous constatez qu’un travail de sauvegarde a démarré.</span><span class="sxs-lookup"><span data-stu-id="53fe9-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![démarrage de sauvegarde](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="53fe9-148">Une fois le travail terminé, vous être de nouveau averti.</span><span class="sxs-lookup"><span data-stu-id="53fe9-148">Once the job has successfully completed, you are notified again.</span></span> <span data-ttu-id="53fe9-149">Le processus de sauvegarde peut démarrer.</span><span class="sxs-lookup"><span data-stu-id="53fe9-149">The backup process then starts.</span></span>
   
    ![travail de sauvegarde créé](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="53fe9-151">Pour suivre l’avancement de vos sauvegardes et consulter les détails du travail, cliquez sur la notification.</span><span class="sxs-lookup"><span data-stu-id="53fe9-151">To track the progress of the backups and look at the job details, click the notification.</span></span> <span data-ttu-id="53fe9-152">Vous accédez à **Détails du travail**.</span><span class="sxs-lookup"><span data-stu-id="53fe9-152">This takes you to  **Job details**.</span></span>
   
     ![détails du travail de sauvegarde](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="53fe9-154">Une fois la sauvegarde terminée, accédez à **Gestion > Catalogue de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="53fe9-154">After the backup is complete, go to **Management > Backup catalog**.</span></span> <span data-ttu-id="53fe9-155">Vous verrez un instantané cloud de tous les partages (ou volumes) sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="53fe9-155">You will see a cloud snapshot of all the shares (or volumes) on your device.</span></span>
   
    ![Sauvegarde terminée](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="53fe9-157">Afficher les sauvegardes existantes</span><span class="sxs-lookup"><span data-stu-id="53fe9-157">View existing backups</span></span>
<span data-ttu-id="53fe9-158">Pour afficher les sauvegardes existantes, procédez comme suit dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="53fe9-158">To view the existing backups, perform the following steps in the Azure portal.</span></span>

#### <a name="to-view-existing-backups"></a><span data-ttu-id="53fe9-159">Pour afficher les sauvegardes existantes</span><span class="sxs-lookup"><span data-stu-id="53fe9-159">To view existing backups</span></span>

1. <span data-ttu-id="53fe9-160">Accédez au panneau **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="53fe9-160">Go to **Devices** blade.</span></span> <span data-ttu-id="53fe9-161">Sélectionnez votre appareil, puis cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="53fe9-161">Select and click your device.</span></span> <span data-ttu-id="53fe9-162">Dans le panneau **Paramètres**, accédez à **Gestion > Catalogue de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="53fe9-162">In the **Settings** blade, go to **Management > Backup Catalog**.</span></span>
   
    ![Accéder au catalogue de sauvegarde](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="53fe9-164">Spécifiez les critères suivants à utiliser pour le filtrage :</span><span class="sxs-lookup"><span data-stu-id="53fe9-164">Specify the following criteria to be used for filtering:</span></span>
   
    - <span data-ttu-id="53fe9-165">**Période** : peut être **Dernière heure**, **Dernières 24 heures**, **Derniers 7 jours**, **30 derniers jours**, **Année dernière** et **Date personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="53fe9-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="53fe9-166">**Appareils** : effectuez votre sélection dans la liste des serveurs de fichiers ou des serveurs iSCSI enregistrés avec votre service de gStorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="53fe9-166">**Devices** – select from the list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="53fe9-167">**Initialisé** : peut être automatiquement **Planifié** (par une stratégie de sauvegarde) ou lancé **Manuellement** (par vous).</span><span class="sxs-lookup"><span data-stu-id="53fe9-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Filtrer les sauvegardes](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="53fe9-169">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="53fe9-169">Click **Apply**.</span></span> <span data-ttu-id="53fe9-170">La liste filtrée des sauvegardes s’affiche dans le panneau **Catalogue de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="53fe9-170">The filtered list of backups is displayed in the **Backup catalog** blade.</span></span> <span data-ttu-id="53fe9-171">Uniquement 100 éléments de sauvegarde peuvent s’afficher simultanément.</span><span class="sxs-lookup"><span data-stu-id="53fe9-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Catalogue de sauvegarde mis à jour](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="53fe9-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="53fe9-173">Next steps</span></span>

<span data-ttu-id="53fe9-174">En savoir plus sur la [gestion de votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="53fe9-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

