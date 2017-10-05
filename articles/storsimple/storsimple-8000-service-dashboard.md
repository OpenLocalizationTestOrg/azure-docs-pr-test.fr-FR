---
title: "Utiliser les infos relatives à un appareil de la gamme StorSimple 8000 | Microsoft Docs"
description: "Décrit le panneau de synthèse du service StorSimple Manager, et explique comment l’utiliser pour surveiller l’intégrité de votre solution StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: d987a4ae170f21532a886552cbe1eb5a0d25fc3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-service-summary-blade-for-storsimple-8000-series-device"></a><span data-ttu-id="e20bd-103">Utiliser le panneau de synthèse du service pour un appareil de la gamme StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="e20bd-103">Use the service summary blade for StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="e20bd-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e20bd-104">Overview</span></span>

<span data-ttu-id="e20bd-105">Le panneau de synthèse du service de StorSimple Device Manager fournit un aperçu de tous les appareils connectés au service StorSimple Device Manager, en mettant en surbrillance ceux qui requièrent une attention particulière d’un administrateur système.</span><span class="sxs-lookup"><span data-stu-id="e20bd-105">The StorSimple Device Manager service summary blade provides a summary view of all the devices that are connected to the StorSimple Device Manager service, highlighting those devices that need a system administrator's attention.</span></span> <span data-ttu-id="e20bd-106">Ce didacticiel présente le panneau de synthèse du service, explique le contenu et la fonction du tableau de bord, et décrit les tâches que vous pouvez effectuer à partir de cette page.</span><span class="sxs-lookup"><span data-stu-id="e20bd-106">This tutorial introduces the service summary blade, explains the dashboard content and function, and describes the tasks that you can perform from this page.</span></span>

![Récapitulatif du service](./media/storsimple-8000-service-dashboard/service-summary1.png)


## <a name="management-commands"></a><span data-ttu-id="e20bd-108">Commandes de gestion</span><span class="sxs-lookup"><span data-stu-id="e20bd-108">Management commands</span></span>

<span data-ttu-id="e20bd-109">Le panneau de synthèse du service StorSimple présente les options de gestion de votre service StorSimple Device Manager, ainsi que les appareils de la gamme StorSimple 8000 inscrits auprès de ce service.</span><span class="sxs-lookup"><span data-stu-id="e20bd-109">In the StorSimple service summary blade, you see the options for managing your StorSimple Device Manager service and the StorSimple 8000 series devices registered to this service.</span></span> <span data-ttu-id="e20bd-110">Les commandes de gestion se trouvent dans la partie supérieure et sur le côté gauche du panneau.</span><span class="sxs-lookup"><span data-stu-id="e20bd-110">You see the management commands across the top of the blade and on the left side.</span></span>

![Barre de commandes](./media/storsimple-8000-service-dashboard/service-summary2.png)

<span data-ttu-id="e20bd-112">Utilisez ces options pour effectuer diverses opérations, telles qu’ajouter des partages ou des volumes, ou surveiller les différents travaux en cours d’exécution sur les appareils StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e20bd-112">Use these options to perform various operations such as add shares or volumes, or monitor the various jobs running on the StorSimple devices.</span></span>


## <a name="essentials"></a><span data-ttu-id="e20bd-113">Essentials</span><span class="sxs-lookup"><span data-stu-id="e20bd-113">Essentials</span></span>

<span data-ttu-id="e20bd-114">La zone des éléments principaux comporte quelques-unes des propriétés importantes comme le groupe de ressources, l’emplacement et l’abonnement dans lequel a été créée votre instance StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="e20bd-114">The essentials area captures some of the important properties such as, the resource group, location, and subscription in which your StorSimple Device Manager was created.</span></span>

![Essentials](./media/storsimple-8000-service-dashboard/service-summary3.png)

## <a name="storsimple-device-manager-service-summary"></a><span data-ttu-id="e20bd-116">Synthèse des services StorSimple Device Manager</span><span class="sxs-lookup"><span data-stu-id="e20bd-116">StorSimple Device Manager service summary</span></span>

* <span data-ttu-id="e20bd-117">La vignette **Alertes** fournit un instantané de toutes les alertes actives sur tous les appareils, groupées par gravité.</span><span class="sxs-lookup"><span data-stu-id="e20bd-117">The **Alerts** tile provides a snapshot of all the active alerts across all devices, grouped by alert severity.</span></span>

    ![Vignette alertes](./media/storsimple-8000-service-dashboard/service-summary4.png)

    <span data-ttu-id="e20bd-119">Cliquez sur la vignette pour ouvrir le panneau **Alertes**, où vous pouvez cliquer sur une alerte individuelle pour afficher des détails supplémentaires, y compris les actions recommandées.</span><span class="sxs-lookup"><span data-stu-id="e20bd-119">Clicking the tile opens the **Alerts** blade, where you can click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="e20bd-120">Vous pouvez également effacer l'alerte si le problème a été résolu.</span><span class="sxs-lookup"><span data-stu-id="e20bd-120">You can also clear the alert if the issue has been resolved.</span></span>

    ![Cliquer sur la vignette Alertes](./media/storsimple-8000-service-dashboard/service-summary8.png)

* <span data-ttu-id="e20bd-122">La vignette **Capacité** affiche le stockage primaire approvisionné et restant sur tous les appareils, par rapport au stockage total disponible sur ceux-ci.</span><span class="sxs-lookup"><span data-stu-id="e20bd-122">The **Capacity** tile displays shows the primary storage that is provisioned and remaining across all devices relative to the total storage available across all devices.</span></span> <span data-ttu-id="e20bd-123">**Approvisionné** fait référence au volume de stockage préparé et alloué pour l’utilisation, **Restant** fait référence à la capacité restante pouvant être approvisionnée sur tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="e20bd-123">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across all devices.</span></span>

    ![Vignette Capacité](./media/storsimple-8000-service-dashboard/service-summary6.png)

    <span data-ttu-id="e20bd-125">La capacité **Hiérarchisée restante** est la capacité disponible pouvant être approvisionnée, notamment le cloud, tandis que la capacité **Locale restante** est la capacité encore disponible sur les disques associés aux appareils de la gamme StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="e20bd-125">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to the StorSimple 8000 series devices.</span></span>


* <span data-ttu-id="e20bd-126">Le graphique **Utilisation** présente les mesures appropriées pour vos appareils.</span><span class="sxs-lookup"><span data-stu-id="e20bd-126">In the **Usage** chart, you can see the relevant metrics for your devices.</span></span> <span data-ttu-id="e20bd-127">Vous pouvez voir le stockage principal utilisé sur tous les appareils, ainsi que le stockage cloud utilisé par les appareils au cours des 7 derniers jours, soit la période par défaut.</span><span class="sxs-lookup"><span data-stu-id="e20bd-127">You can view the primary storage used across all devices, and the cloud storage consumed by devices over the past 7 days, the default time period.</span></span> 

    ![Mosaïque Utilisation](./media/storsimple-8000-service-dashboard/service-summary7.png) 

    <span data-ttu-id="e20bd-129">Pour choisir une autre échelle de temps, utilisez l’option **Modifier** accessible dans l’angle supérieur droit du graphique.</span><span class="sxs-lookup"><span data-stu-id="e20bd-129">To choose a different time scale, use the **Edit** option in the top-right corner of the chart.</span></span>

     ![Cliquer sur la Utilisation](./media/storsimple-8000-service-dashboard/service-summary10.png)

     ![Exporter les données du graphique](./media/storsimple-8000-service-dashboard/service-summary11.png)

* <span data-ttu-id="e20bd-132">La vignette **Appareils** fournit une synthèse du nombre d’appareils de la gamme StorSimple 8000 présents dans votre StorSimple Device Manager, regroupés par état d’appareil.</span><span class="sxs-lookup"><span data-stu-id="e20bd-132">The **Devices** tile provides a summary of the number of StorSimple 8000 series devices in your StorSimple Device Manager grouped by device status.</span></span> 

    ![Vignette Appareils](./media/storsimple-8000-service-dashboard/service-summary5.png)

    <span data-ttu-id="e20bd-134">Cliquez sur cette vignette pour ouvrir le panneau de la liste des **Appareils**, puis cliquez sur un appareil spécifique afin d’accéder aux données le concernant.</span><span class="sxs-lookup"><span data-stu-id="e20bd-134">Click this tile to open the **Devices** list blade and then click an individual device to drill into the device summary specific to the device.</span></span> <span data-ttu-id="e20bd-135">Vous pouvez également exécuter des actions spécifiques d’un appareil à partir d’un panneau de synthèse d’appareil donné.</span><span class="sxs-lookup"><span data-stu-id="e20bd-135">You can also perform device-specific actions from a given device summary blade.</span></span> <span data-ttu-id="e20bd-136">Pour plus d’informations sur le panneau de synthèse des appareils, accédez à [Panneau de synthèse des appareils](storsimple-8000-device-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="e20bd-136">For more information about the device summary blade, go to [Device summary blade](storsimple-8000-device-dashboard.md).</span></span>

    ![Cliquer sur la vignette Appareils](./media/storsimple-8000-service-dashboard/service-summary9.png)

## <a name="view-the-activity-logs"></a><span data-ttu-id="e20bd-138">Afficher les journaux d’activité</span><span class="sxs-lookup"><span data-stu-id="e20bd-138">View the activity logs</span></span>

<span data-ttu-id="e20bd-139">Pour afficher les opérations effectuées au sein de votre instance StorSimple Device Manager, cliquez sur le lien **Journaux d’activité** situé sur le côté gauche du panneau de synthèse des services StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e20bd-139">To view the various operations carried out within your StorSimple Device Manager, click the **Activity logs** link on the left side of your StorSimple service summary blade.</span></span> <span data-ttu-id="e20bd-140">Vous accédez au panneau **Journaux d’activité**, où vous avez accès à une synthèse des opérations récentes effectuées.</span><span class="sxs-lookup"><span data-stu-id="e20bd-140">This takes you to the **Activity logs** blade, where you can see a summary of the recent operations carried out.</span></span>

![Journaux d’activité](./media/storsimple-8000-service-dashboard/activity-logs1.png)
## <a name="next-steps"></a><span data-ttu-id="e20bd-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e20bd-142">Next steps</span></span>

* <span data-ttu-id="e20bd-143">En savoir plus sur [l’utilisation du service StorSimple Device Manager pour gérer votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e20bd-143">Learn more about how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

