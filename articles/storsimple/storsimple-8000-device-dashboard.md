---
title: "Appareil de série aaaUse StorSimple 8000 résumé | Documents Microsoft"
description: "Décrit le périphérique de service du Gestionnaire de périphériques StorSimple hello résumé et comment toouse il tooview storage metrics et les initiateurs connectés et les rechercher hello numéro de série et le nom qualifié."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a><span data-ttu-id="57238-103">Utiliser l’appareil hello résumé dans le service Gestionnaire de périphériques StorSimple</span><span class="sxs-lookup"><span data-stu-id="57238-103">Use hello device summary in StorSimple Device Manager service</span></span>

## <a name="overview"></a><span data-ttu-id="57238-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="57238-104">Overview</span></span>
<span data-ttu-id="57238-105">panneau Résumé du périphérique StorSimple Hello vous donne une vue d’ensemble des informations relatives à un périphérique StorSimple spécifique, en revanche toohello service panneau Résumé, qui fournit des informations sur tous les appareils hello inclus dans votre solution Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="57238-105">hello StorSimple device summary blade gives you an overview of information for a specific StorSimple device, in contrast toohello service summary blade, which gives you information about all hello devices included in your Microsoft Azure StorSimple solution.</span></span>

<span data-ttu-id="57238-106">panneau Résumé du périphérique Hello fournit un résumé d’un appareil de série StorSimple 8000 est inscrit avec une donnée StorSimple Gestionnaire de périphériques, mise en évidence les problèmes de périphériques qui nécessitent une intervention d’un administrateur système.</span><span class="sxs-lookup"><span data-stu-id="57238-106">hello device summary blade provides a summary view of a StorSimple 8000 series device that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="57238-107">Ce didacticiel présente panneau Résumé du périphérique hello, explique la fonction et le contenu de hello et décrit les tâches hello que vous pouvez effectuer à partir de ce panneau.</span><span class="sxs-lookup"><span data-stu-id="57238-107">This tutorial introduces hello device summary blade, explains hello content and function, and describes hello tasks that you can perform from this blade.</span></span>

<span data-ttu-id="57238-108">panneau Résumé du périphérique Hello affiche hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="57238-108">hello device summary blade displays hello following information:</span></span>

![Panneau de synthèse de l’appareil](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a><span data-ttu-id="57238-110">Barre de commandes de gestion</span><span class="sxs-lookup"><span data-stu-id="57238-110">Management command bar</span></span>

<span data-ttu-id="57238-111">Dans le panneau de périphérique StorSimple hello, vous voyez les options hello gestion de votre périphérique StorSimple.</span><span class="sxs-lookup"><span data-stu-id="57238-111">In hello StorSimple device blade, you see hello options for managing your StorSimple device.</span></span> <span data-ttu-id="57238-112">Vous consultez les commandes de gestion hello haut hello du Panneau de hello et sur le côté gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="57238-112">You see hello management commands across hello top of hello blade and on hello left side.</span></span> <span data-ttu-id="57238-113">Utilisez ces options tooadd partages ou des volumes, ou mettre à jour ou basculer votre appareil.</span><span class="sxs-lookup"><span data-stu-id="57238-113">Use these options tooadd shares or volumes, or update or fail over your device.</span></span>

![Barre de commandes de gestion](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a><span data-ttu-id="57238-115">Essentials</span><span class="sxs-lookup"><span data-stu-id="57238-115">Essentials</span></span>

<span data-ttu-id="57238-116">zone d’essentials Hello capture certaines des propriétés importantes de hello comme état de hello, modèle, IQN cible et version du logiciel hello.</span><span class="sxs-lookup"><span data-stu-id="57238-116">hello essentials area captures some of hello important properties such as, hello status, model, target IQN, and hello software version.</span></span> 

![Éléments principaux des appareils](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a><span data-ttu-id="57238-118">Surveillance</span><span class="sxs-lookup"><span data-stu-id="57238-118">Monitoring</span></span>

* <span data-ttu-id="57238-119">Hello **alertes** vignette fournit un instantané de toutes les alertes actives hello pour votre appareil, regroupée par gravité.</span><span class="sxs-lookup"><span data-stu-id="57238-119">hello **Alerts** tile provides a snapshot of all hello active alerts for your device, grouped by alert severity.</span></span>

    ![Vignette Alertes](./media/storsimple-8000-device-dashboard/device-summary4.png)

    <span data-ttu-id="57238-121">Cliquez sur Bonjour vignette tooopen Bonjour **alertes** panneau, puis cliquez sur un individu alerte tooview supplémentaire plus d’informations sur cette alerte, y compris les actions recommandées.</span><span class="sxs-lookup"><span data-stu-id="57238-121">Click hello tile tooopen hello **Alerts** blade and then click an individual alert tooview additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="57238-122">Vous pouvez également effacer les alerte hello si hello est résolu.</span><span class="sxs-lookup"><span data-stu-id="57238-122">You can also clear hello alert if hello issue has been resolved.</span></span>

    ![Cliquer sur la vignette Alertes](./media/storsimple-8000-device-dashboard/device-summary10.png)

* <span data-ttu-id="57238-124">Hello **état et l’intégrité** vignette fournit des informations sur l’intégrité du composant hello matériel pour un périphérique, notamment l’état du périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="57238-124">hello **Status and health** tile provides insights into hello hardware component health for a device including hello device status.</span></span> <span data-ttu-id="57238-125">état du périphérique Hello peut être hors connexion, en ligne, désactivé ou prêt tooset up.</span><span class="sxs-lookup"><span data-stu-id="57238-125">hello device status may be offline, online, deactivated, or ready tooset up.</span></span>

    ![Vignette État et intégrité](./media/storsimple-8000-device-dashboard/device-summary5.png)

* <span data-ttu-id="57238-127">Hello **Volumes** vignette fournit un résumé du nombre de hello de volumes de votre appareil, regroupés par état.</span><span class="sxs-lookup"><span data-stu-id="57238-127">hello **Volumes** tile provides a summary of hello number of volumes in your device grouped by status.</span></span>

    ![Vignette Volumes](./media/storsimple-8000-device-dashboard/device-summary6.png)

    <span data-ttu-id="57238-129">Cliquez sur Bonjour vignette tooopen Bonjour **Volumes** liste panneau, puis cliquez sur un volume individuel de tooview ou modifier ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="57238-129">Click hello tile tooopen hello **Volumes** list blade, and then click on an individual volume tooview or modify its properties.</span></span>
    
    ![Cliquer sur la vignette Volumes](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    <span data-ttu-id="57238-131">Pour plus d’informations, consultez Comment trop[gérer les volumes](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="57238-131">For more information, see how too[manage volumes](storsimple-8000-manage-volumes-u2.md).</span></span>

* <span data-ttu-id="57238-132">Bonjour **utilisation** graphique, vous pouvez afficher les stockage principal hello utilisée sur votre appareil et le stockage en cloud hello consommées sur hello des 7 derniers jours, la valeur par défaut de hello laps de temps.</span><span class="sxs-lookup"><span data-stu-id="57238-132">In hello **Usage** chart, you can view hello primary storage used across your device, and hello cloud storage consumed over hello past 7 days, hello default time period.</span></span>

     ![Mosaïque Utilisation](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     <span data-ttu-id="57238-134">toochoose une échelle de temps différente, utilisez hello **modifier** option dans l’angle supérieur droit de hello du graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="57238-134">toochoose a different time scale, use hello **Edit** option in hello top-right corner of hello chart.</span></span>

     ![Modifier le graphique Utilisation](./media/storsimple-8000-device-dashboard/device-summary12.png)

     <span data-ttu-id="57238-136">Dans ce graphique, vous pouvez afficher les métriques de stockage principal total hello (montant hello des données écrites par l’appareil de tooyour hôtes) et hello totale consommé par votre appareil sur une période de temps de stockage cloud.</span><span class="sxs-lookup"><span data-stu-id="57238-136">In this chart, you can view metrics for hello total primary storage (hello amount of data written by hosts tooyour device) and hello total cloud storage consumed by your device over a period of time.</span></span>
  
     <span data-ttu-id="57238-137">Dans ce contexte, *stockage principal* fait référence toohello la quantité totale de données écrites par hello hôte et peut être décomposée en type de volume : *principal de stockage hiérarchisé* inclut les deux stockés localement les données et les données cloud toohello à plusieurs niveaux.</span><span class="sxs-lookup"><span data-stu-id="57238-137">In this context, *primary storage* refers toohello total amount of data written by hello host, and can be broken down by volume type: *primary tiered storage* includes both locally stored data and data tiered toohello cloud.</span></span> <span data-ttu-id="57238-138">Le *stockage principal attaché localement* inclut uniquement les données stockées localement.</span><span class="sxs-lookup"><span data-stu-id="57238-138">*Primary locally pinned storage* includes just data stored locally.</span></span> <span data-ttu-id="57238-139">*Stockage cloud*, on hello d’autre part, est une mesure de la quantité totale de hello des données stockées dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="57238-139">*Cloud storage*, on hello other hand, is a measurement of hello total amount of data stored in hello cloud.</span></span> <span data-ttu-id="57238-140">Ce stockage inclut les données hiérarchisées et les sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="57238-140">This storage includes tiered data and backups.</span></span> <span data-ttu-id="57238-141">les données Hello stockées dans le cloud de hello sont dédupliquées et compressées, alors que le stockage principal indique la quantité hello de stockage utilisé avant hello sont dédupliquées et des données compressées.</span><span class="sxs-lookup"><span data-stu-id="57238-141">hello data stored in hello cloud is deduplicated and compressed, whereas primary storage indicates hello amount of storage used before hello data is deduplicated and compressed.</span></span> <span data-ttu-id="57238-142">(Vous pouvez comparer ces tooget de deux nombres une idée du taux de compression hello). Pour les deux types et stockage hello les montants indiqués sont basées sur hello suivi fréquence que vous configurez en nuage.</span><span class="sxs-lookup"><span data-stu-id="57238-142">(You can compare these two numbers tooget an idea of hello compression rate.) For both primary and cloud storage, hello amounts shown are based on hello tracking frequency you configure.</span></span> <span data-ttu-id="57238-143">Par exemple, si vous choisissez une fréquence hebdomadaire, puis graphique de hello affiche les données pour chaque jour Bonjour semaine précédente.</span><span class="sxs-lookup"><span data-stu-id="57238-143">For example, if you choose a one week frequency, then hello chart shows data for each day in hello previous week.</span></span>

     <span data-ttu-id="57238-144">quantité de hello toosee de stockage cloud consommé sur le temps, sélectionnez hello **stockage CLOUD utilisé** option.</span><span class="sxs-lookup"><span data-stu-id="57238-144">toosee hello amount of cloud storage consumed over time, select hello **CLOUD STORAGE USED** option.</span></span> <span data-ttu-id="57238-145">stockage total toosee hello qui a été écrit par hôte hello, sélectionnez hello **hiérarchisé stockage utilisé principal** et **localement ÉPINGLÉ stockage principal utilisé** options.</span><span class="sxs-lookup"><span data-stu-id="57238-145">toosee hello total storage that has been written by hello host, select hello **PRIMARY TIERED STORAGE USED** and **PRIMARY LOCALLY PINNED STORAGE USED** options.</span></span> 
     <span data-ttu-id="57238-146">Pour plus d’informations, consultez [utilisez hello toomonitor du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-monitor-device.md).</span><span class="sxs-lookup"><span data-stu-id="57238-146">For more information, see [Use hello StorSimple Device Manager service toomonitor your StorSimple device](storsimple-monitor-device.md).</span></span>


* <span data-ttu-id="57238-147">Hello **capacité** vignette affiche hello stockage principal qui est configuré et restants dans hello appareil relatif toohello stockage total disponible pour hello identiques.</span><span class="sxs-lookup"><span data-stu-id="57238-147">hello **Capacity** tile displays hello primary storage that is provisioned and remaining across hello device relative toohello total storage available for hello same.</span></span> <span data-ttu-id="57238-148">**Configuré** fait référence toohello quantité de stockage qui est préparée et allouée à l’utilisation, **restant** fait référence toohello restant de capacité qui peut être configurée sur ce périphérique.</span><span class="sxs-lookup"><span data-stu-id="57238-148">**Provisioned** refers toohello amount of storage that is prepared and allocated for use, **Remaining** refers toohello remaining capacity that can be provisioned across this device.</span></span> 

    ![Mosaïque Utilisation](./media/storsimple-8000-device-dashboard/device-summary8.png)

    <span data-ttu-id="57238-150">Cliquez sur cette tooview vignette la capacité de hello est configurée sur les volumes attachés localement et hiérarchisés.</span><span class="sxs-lookup"><span data-stu-id="57238-150">Click this tile tooview how hello capacity is provisioned across tiered and locally pinned volumes.</span></span> <span data-ttu-id="57238-151">Hello **hiérarchisé restantes** capacité est la capacité disponible hello qui peut être configurée, y compris le nuage, tout en hello **restant Local** est la capacité hello restant sur des disques hello toothis de périphérique.</span><span class="sxs-lookup"><span data-stu-id="57238-151">hello **Remaining Tiered** capacity is hello available capacity that can be provisioned including cloud, while hello **Remaining Local** is hello capacity remaining on hello disks attached toothis device.</span></span>

    ![Cliquer sur le graphique Utilisation](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a><span data-ttu-id="57238-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57238-153">Next steps</span></span>
* <span data-ttu-id="57238-154">En savoir plus sur hello [panneau Résumé du service StorSimple](storsimple-8000-service-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="57238-154">Learn more about hello [StorSimple service summary blade](storsimple-8000-service-dashboard.md).</span></span>
* <span data-ttu-id="57238-155">En savoir plus sur [à l’aide de hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="57238-155">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

