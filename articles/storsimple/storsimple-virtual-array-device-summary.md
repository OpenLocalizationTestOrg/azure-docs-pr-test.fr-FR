---
title: "Panneau de synthèse de l’appareil StorSimple Virtual Array | Microsoft Docs"
description: "Décrit le panneau de synthèse des appareils pour StorSimple Device Manager et explique comment l’utiliser pour surveiller l’intégrité de votre instance StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 35413d597c3b6b1c7600241a78572b63f982d175
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-blade-for-storsimple-device-manager-connected-to-storsimple-virtual-array"></a><span data-ttu-id="911c1-103">Utiliser le panneau de synthèse des appareils pour StorSimple Device Manager connecté à StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="911c1-103">Use the device summary blade for StorSimple Device Manager connected to StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="911c1-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="911c1-104">Overview</span></span>

<span data-ttu-id="911c1-105">Le panneau de synthèse des appareils StorSimple Device Manager procure un résumé d’une instance StorSimple Virtual Array enregistrée auprès d’un service StorSimple Device Manager, en mettant en évidence les problèmes qui nécessitent l’intervention d’un administrateur système.</span><span class="sxs-lookup"><span data-stu-id="911c1-105">The StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="911c1-106">Ce didacticiel présente le panneau de synthèse des appareils, explique le contenu et la fonctionnalité et décrit les travaux que vous pouvez effectuer à partir de ce panneau.</span><span class="sxs-lookup"><span data-stu-id="911c1-106">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="911c1-107">Le panneau de synthèse des appareils affiche les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="911c1-107">The device summary blade displays the following information:</span></span>

![Page du tableau de bord d’un appareil](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a><span data-ttu-id="911c1-109">Gestion</span><span class="sxs-lookup"><span data-stu-id="911c1-109">Management</span></span>

<span data-ttu-id="911c1-110">Dans le panneau des appareils StorSimple, vous avez accès aux options de gestion de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="911c1-110">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="911c1-111">Les commandes de gestion se trouvent dans la partie supérieure et sur le côté gauche du panneau.</span><span class="sxs-lookup"><span data-stu-id="911c1-111">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="911c1-112">Utilisez ces options pour ajouter des partages ou des volumes, ou pour mettre à jour ou basculer votre tableau virtuel.</span><span class="sxs-lookup"><span data-stu-id="911c1-112">Use these options to add shares or volumes, or update or fail over your virtual array.</span></span>

<span data-ttu-id="911c1-113">La zone des éléments principaux comporte quelques-unes des propriétés importantes, telles que le statut, le modèle, la version logicielle, ainsi qu’un lien vers l’**IU web** du tableau.</span><span class="sxs-lookup"><span data-stu-id="911c1-113">The essentials area captures some of the important properties such as, the status, model, software version as well as a link to the **Web UI** of the array.</span></span> <span data-ttu-id="911c1-114">Si vous vous trouvez sur un réseau interne, vous pouvez directement lancer [l’interface utilisateur web locale](storsimple-ova-web-ui-admin.md) pour administrer votre tableau virtuel.</span><span class="sxs-lookup"><span data-stu-id="911c1-114">If you are on an internal network, you can directly launch the [local web UI](storsimple-ova-web-ui-admin.md) to administer your virtual array.</span></span>

![Éléments principaux des appareils](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a><span data-ttu-id="911c1-116">Synthèse des appareils StorSimple</span><span class="sxs-lookup"><span data-stu-id="911c1-116">StorSimple device summary</span></span>

* <span data-ttu-id="911c1-117">La vignette **Alertes** fournit un instantané de l’ensemble des alertes actives associées à votre tableau virtuel, et groupées par gravité.</span><span class="sxs-lookup"><span data-stu-id="911c1-117">The **Alerts** tile provides a snapshot of all the active alerts for your virtual array, grouped by alert severity.</span></span> <span data-ttu-id="911c1-118">Cliquez sur la vignette pour ouvrir le panneau **Alertes**, puis cliquez sur une alerte pour afficher des détails supplémentaires sur cette alerte, y compris les actions recommandées.</span><span class="sxs-lookup"><span data-stu-id="911c1-118">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="911c1-119">Vous pouvez également effacer l'alerte si le problème a été résolu.</span><span class="sxs-lookup"><span data-stu-id="911c1-119">You can also clear the alert if the issue has been resolved.</span></span>

* <span data-ttu-id="911c1-120">La vignette **Capacité** affiche le stockage primaire configuré et demeurant sur l’appareil virtuel, relativement au stockage total disponible pour cet élément.</span><span class="sxs-lookup"><span data-stu-id="911c1-120">The **Capacity** tile displays the primary storage that is provisioned and remaining across the virtual device relative to the total storage available for the same.</span></span> <span data-ttu-id="911c1-121">**Configuré** fait référence au volume de stockage préparé et alloué pour l’utilisation, **Restant** fait référence à la capacité restante pouvant être configurée sur cet appareil.</span><span class="sxs-lookup"><span data-stu-id="911c1-121">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> <span data-ttu-id="911c1-122">La capacité **Hiérarchisée restante** est la capacité disponible pouvant être configurée, notamment le cloud, tandis que la capacité **Locale restante** est la capacité restant sur les disques associés à ce tableau virtuel.</span><span class="sxs-lookup"><span data-stu-id="911c1-122">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this virtual array.</span></span>

* <span data-ttu-id="911c1-123">Dans le tableau **Utilisation**, vous pouvez consulter le stockage primaire utilisé au sein de votre tableau virtuel, ainsi que le stockage cloud consommé ces 7 derniers jours, la période par défaut.</span><span class="sxs-lookup"><span data-stu-id="911c1-123">In the **Usage** chart, you can view the primary storage used across your virtual array, as well as the cloud storage consumed  over the past 7 days, the default time period.</span></span> <span data-ttu-id="911c1-124">Utilisez l’option **Modifier** du coin supérieur droit du tableau pour définir une période différente.</span><span class="sxs-lookup"><span data-stu-id="911c1-124">Use the **Edit** option in the top-right corner of the chart to choose a different time scale.</span></span>

* <span data-ttu-id="911c1-125">La vignette **Partages** ou **Volumes** fournit une synthèse des nombres de partages ou de volumes de votre appareil, groupés par état.</span><span class="sxs-lookup"><span data-stu-id="911c1-125">The **Shares** or **Volumes** tile provides a summary of the number of shares or volumes in your device grouped by status.</span></span> <span data-ttu-id="911c1-126">Cliquez sur la vignette pour ouvrir le panneau de la liste **Partages** ou **Volumes**, puis cliquez sur un partage ou un volume individuel pour afficher ou modifier ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="911c1-126">Click the tile to open the **Shares**  or **Volumes** list blade, and then click on an individual share or volume to view or modify its properties.</span></span> <span data-ttu-id="911c1-127">Pour plus d’informations, découvrez comment [gérer des partages](storsimple-virtual-array-manage-shares.md) ou [gérer des volumes](storsimple-virtual-array-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="911c1-127">For more information, see how to [manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="911c1-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="911c1-128">Next steps</span></span>
<span data-ttu-id="911c1-129">Découvrez comment :</span><span class="sxs-lookup"><span data-stu-id="911c1-129">Learn how to:</span></span>
- [<span data-ttu-id="911c1-130">Gérer des partages sur une instance StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="911c1-130">Manage shares on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-shares.md)
    
- [<span data-ttu-id="911c1-131">Gérer des volumes sur une instance StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="911c1-131">Manage volumes on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-volumes.md)

