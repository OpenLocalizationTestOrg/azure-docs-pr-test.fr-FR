---
title: didacticiel de sauvegarde Azure StorSimple Virtual Array aaaMicrosoft | Documents Microsoft
description: "Décrit comment tooback des StorSimple Virtual Array et les volumes."
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
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="cd954-103">Sauvegarde de partages ou de volumes sur votre StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="cd954-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="cd954-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="cd954-104">Overview</span></span>

<span data-ttu-id="cd954-105">Hello StorSimple Virtual Array est un hybride cloud stockage local périphérique virtuel qui peut être configuré comme un serveur de fichiers ou un serveur iSCSI.</span><span class="sxs-lookup"><span data-stu-id="cd954-105">hello StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="cd954-106">unité de stockage virtuelle Hello permet hello utilisateur toocreate des sauvegardes planifiées et manuelles de tous les partages de hello ou volumes sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="cd954-106">hello virtual array allows hello user toocreate scheduled and manual backups of all hello shares or volumes on hello device.</span></span> <span data-ttu-id="cd954-107">Configuré comme serveur de fichiers, il permet également la récupération au niveau de l’élément.</span><span class="sxs-lookup"><span data-stu-id="cd954-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="cd954-108">Ce didacticiel décrit comment toocreate planifiées et sauvegardes manuelles et effectuer la récupération au niveau élément toorestore un fichier supprimé sur votre tableau virtuel.</span><span class="sxs-lookup"><span data-stu-id="cd954-108">This tutorial describes how toocreate scheduled and manual backups and perform item-level recovery toorestore a deleted file on your virtual array.</span></span>

<span data-ttu-id="cd954-109">Ce didacticiel s’applique toohello StorSimple tableaux virtuels uniquement.</span><span class="sxs-lookup"><span data-stu-id="cd954-109">This tutorial applies toohello StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="cd954-110">Pour plus d’informations sur la 8000 série, accédez trop[créer une sauvegarde pour appareil de 8000 série](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="cd954-110">For information on 8000 series, go too[Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="cd954-111">Sauvegarder des partages et des volumes</span><span class="sxs-lookup"><span data-stu-id="cd954-111">Back up shares and volumes</span></span>

<span data-ttu-id="cd954-112">Les sauvegardes fournissent une protection jusqu’à une date et une heure, et optimisent la récupération tout en réduisant les délais de restauration pour les partages et les sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="cd954-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="cd954-113">Vous pouvez sauvegarder un partage ou un volume sur votre appareil StorSimple de deux manières : **planifiée** ou **manuelle**.</span><span class="sxs-lookup"><span data-stu-id="cd954-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="cd954-114">Chacune des méthodes de hello est expliqué dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="cd954-114">Each of hello methods is discussed in hello following sections.</span></span>

## <a name="change-hello-backup-start-time"></a><span data-ttu-id="cd954-115">Modifier l’heure de début de la sauvegarde hello</span><span class="sxs-lookup"><span data-stu-id="cd954-115">Change hello backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="cd954-116">Dans cette version, les sauvegardes planifiées sont créés par une stratégie par défaut qui s’exécute tous les jours à une heure spécifiée et la sauvegarde de tous les partages de hello ou volumes sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="cd954-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all hello shares or volumes on hello device.</span></span> <span data-ttu-id="cd954-117">Il n’est pas possible de toocreate des stratégies personnalisées pour les sauvegardes planifiées pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="cd954-117">It is not possible toocreate custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="cd954-118">Votre StorSimple Virtual Array a une stratégie de sauvegarde par défaut qui commence à une heure spécifiée (22:30) et sauvegarde toutes les hello partages ou volumes sur l’appareil de hello une fois par jour.</span><span class="sxs-lookup"><span data-stu-id="cd954-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all hello shares or volumes on hello device once a day.</span></span> <span data-ttu-id="cd954-119">Vous pouvez modifier le temps de hello auxquelles démarrage de la sauvegarde hello, mais les fréquences de hello et hello rétention (qui spécifie le nombre de hello de sauvegardes tooretain) ne peut pas être modifiée.</span><span class="sxs-lookup"><span data-stu-id="cd954-119">You can change hello time at which hello backup starts, but hello frequency and hello retention (which specifies hello number of backups tooretain) cannot be changed.</span></span> <span data-ttu-id="cd954-120">Au cours de ces sauvegardes, un appareil virtuel entier hello est sauvegardé.</span><span class="sxs-lookup"><span data-stu-id="cd954-120">During these backups, hello entire virtual device is backed up.</span></span> <span data-ttu-id="cd954-121">Cela pourrait potentiellement hello les performances du périphérique de hello et affecter des charges de travail hello déployés sur le périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="cd954-121">This could potentially impact hello performance of hello device and affect hello workloads deployed on hello device.</span></span> <span data-ttu-id="cd954-122">Par conséquent, nous vous recommandons de planifier ces sauvegardes pendant les heures creuses.</span><span class="sxs-lookup"><span data-stu-id="cd954-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="cd954-123">heure de début de sauvegarde par défaut de hello toochange, effectuer hello Bonjour comme suit [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cd954-123">toochange hello default backup start time, perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a><span data-ttu-id="cd954-124">toochange hello heure de début de stratégie de sauvegarde par défaut hello</span><span class="sxs-lookup"><span data-stu-id="cd954-124">toochange hello start time for hello default backup policy</span></span>

1. <span data-ttu-id="cd954-125">Accédez trop**périphériques**.</span><span class="sxs-lookup"><span data-stu-id="cd954-125">Go too**Devices**.</span></span> <span data-ttu-id="cd954-126">liste de Hello des appareils inscrits auprès du service Gestionnaire de périphériques StorSimple s’affichera.</span><span class="sxs-lookup"><span data-stu-id="cd954-126">hello list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![Accédez toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="cd954-128">Sélectionnez votre appareil, puis cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="cd954-128">Select and click your device.</span></span> <span data-ttu-id="cd954-129">Hello **paramètres** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="cd954-129">hello **Settings** blade will be displayed.</span></span> <span data-ttu-id="cd954-130">Accédez trop**gérer > stratégies de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="cd954-130">Go too**Manage > Backup policies**.</span></span>
   
    ![sélectionner votre appareil](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="cd954-132">Bonjour **stratégies de sauvegarde** panneau, heure de début hello par défaut est 22:30.</span><span class="sxs-lookup"><span data-stu-id="cd954-132">In hello **Backup policies** blade, hello default start time is 22:30.</span></span> <span data-ttu-id="cd954-133">Vous pouvez spécifier la nouvelle heure de début hello pour une planification quotidienne de hello dans le fuseau horaire.</span><span class="sxs-lookup"><span data-stu-id="cd954-133">You can specify hello new start time for hello daily schedule in device time zone.</span></span>
   
    ![Accédez toobackup stratégies](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="cd954-135">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="cd954-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="cd954-136">Exécuter une sauvegarde manuelle</span><span class="sxs-lookup"><span data-stu-id="cd954-136">Take a manual backup</span></span>

<span data-ttu-id="cd954-137">En outre tooscheduled des sauvegardes, vous pouvez exécuter une sauvegarde de (à la demande) manuelle de données de l’appareil à tout moment.</span><span class="sxs-lookup"><span data-stu-id="cd954-137">In addition tooscheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="cd954-138">toocreate une sauvegarde manuelle</span><span class="sxs-lookup"><span data-stu-id="cd954-138">toocreate a manual backup</span></span>

1. <span data-ttu-id="cd954-139">Accédez trop**périphériques**.</span><span class="sxs-lookup"><span data-stu-id="cd954-139">Go too**Devices**.</span></span> <span data-ttu-id="cd954-140">Sélectionnez votre appareil et avec le bouton droit **...**  à hello plus à droite de la ligne sélectionnée de hello.</span><span class="sxs-lookup"><span data-stu-id="cd954-140">Select your device and right-click **...** at hello far right in hello selected row.</span></span> <span data-ttu-id="cd954-141">Dans le menu contextuel de hello, sélectionnez **sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="cd954-141">From hello context menu, select **Take backup**.</span></span>
   
    ![Accédez tootake sauvegarde](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="cd954-143">Bonjour **sauvegarde** panneau, cliquez sur **sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="cd954-143">In hello **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="cd954-144">Cette opération sauvegarde tous les partages de hello sur le serveur de fichiers hello ou tous les volumes hello sur votre serveur iSCSI.</span><span class="sxs-lookup"><span data-stu-id="cd954-144">This will backup all hello shares on hello file server or all hello volumes on your iSCSI server.</span></span> 
   
    ![démarrage de sauvegarde](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="cd954-146">Une sauvegarde à la demande démarre ; vous constatez qu’un travail de sauvegarde a démarré.</span><span class="sxs-lookup"><span data-stu-id="cd954-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![démarrage de sauvegarde](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="cd954-148">Une fois le travail de hello terminé, vous êtes averti à nouveau.</span><span class="sxs-lookup"><span data-stu-id="cd954-148">Once hello job has successfully completed, you are notified again.</span></span> <span data-ttu-id="cd954-149">processus de sauvegarde Hello démarre ensuite.</span><span class="sxs-lookup"><span data-stu-id="cd954-149">hello backup process then starts.</span></span>
   
    ![travail de sauvegarde créé](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="cd954-151">progression de hello tootrack de sauvegardes de hello et examinez les détails de la tâche hello, cliquez sur la notification de hello.</span><span class="sxs-lookup"><span data-stu-id="cd954-151">tootrack hello progress of hello backups and look at hello job details, click hello notification.</span></span> <span data-ttu-id="cd954-152">Vous accéderez trop **détails de la tâche**.</span><span class="sxs-lookup"><span data-stu-id="cd954-152">This takes you too **Job details**.</span></span>
   
     ![détails du travail de sauvegarde](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="cd954-154">Une fois hello sauvegarde est terminée, passez trop**Gestion > catalogue de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="cd954-154">After hello backup is complete, go too**Management > Backup catalog**.</span></span> <span data-ttu-id="cd954-155">Vous verrez un instantané cloud de tous les partages de hello (ou volumes) sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="cd954-155">You will see a cloud snapshot of all hello shares (or volumes) on your device.</span></span>
   
    ![Sauvegarde terminée](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="cd954-157">Afficher les sauvegardes existantes</span><span class="sxs-lookup"><span data-stu-id="cd954-157">View existing backups</span></span>
<span data-ttu-id="cd954-158">tooview les sauvegardes existantes hello, effectuer hello Bonjour portail Azure comme suit.</span><span class="sxs-lookup"><span data-stu-id="cd954-158">tooview hello existing backups, perform hello following steps in hello Azure portal.</span></span>

#### <a name="tooview-existing-backups"></a><span data-ttu-id="cd954-159">sauvegardes existantes tooview</span><span class="sxs-lookup"><span data-stu-id="cd954-159">tooview existing backups</span></span>

1. <span data-ttu-id="cd954-160">Accédez trop**périphériques** panneau.</span><span class="sxs-lookup"><span data-stu-id="cd954-160">Go too**Devices** blade.</span></span> <span data-ttu-id="cd954-161">Sélectionnez votre appareil, puis cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="cd954-161">Select and click your device.</span></span> <span data-ttu-id="cd954-162">Bonjour **paramètres** panneau, accédez trop**Gestion > catalogue de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="cd954-162">In hello **Settings** blade, go too**Management > Backup Catalog**.</span></span>
   
    ![Accédez toobackup catalogue](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="cd954-164">Spécifiez hello suivant toobe de critères utilisé pour le filtrage :</span><span class="sxs-lookup"><span data-stu-id="cd954-164">Specify hello following criteria toobe used for filtering:</span></span>
   
    - <span data-ttu-id="cd954-165">**Période** : peut être **Dernière heure**, **Dernières 24 heures**, **Derniers 7 jours**, **30 derniers jours**, **Année dernière** et **Date personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="cd954-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="cd954-166">**Appareils** – permet de sélectionner à partir de la liste de hello des serveurs de fichiers ou des serveurs iSCSI inscrits auprès du service Gestionnaire de périphériques StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cd954-166">**Devices** – select from hello list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="cd954-167">**Initialisé** : peut être automatiquement **Planifié** (par une stratégie de sauvegarde) ou lancé **Manuellement** (par vous).</span><span class="sxs-lookup"><span data-stu-id="cd954-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Filtrer les sauvegardes](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="cd954-169">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="cd954-169">Click **Apply**.</span></span> <span data-ttu-id="cd954-170">liste filtrée des sauvegardes Hello s’affiche dans hello **catalogue de sauvegarde** panneau.</span><span class="sxs-lookup"><span data-stu-id="cd954-170">hello filtered list of backups is displayed in hello **Backup catalog** blade.</span></span> <span data-ttu-id="cd954-171">Uniquement 100 éléments de sauvegarde peuvent s’afficher simultanément.</span><span class="sxs-lookup"><span data-stu-id="cd954-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Catalogue de sauvegarde mis à jour](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="cd954-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cd954-173">Next steps</span></span>

<span data-ttu-id="cd954-174">En savoir plus sur la [gestion de votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="cd954-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

