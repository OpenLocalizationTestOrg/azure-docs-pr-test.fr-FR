---
title: "aaaManage de calcul power dans l’entrepôt de données SQL Azure (portail Azure) | Documents Microsoft"
description: "Tâches du portail Azure toomanage une puissance de calcul. Mettez à l’échelle les ressources de calcul en ajustant les unités DWU. Ou bien, suspendre et reprendre des coûts toosave des ressources de calcul."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="dfb37-105">Gestion de la puissance de calcul dans Azure SQL Data Warehouse (portail Azure)</span><span class="sxs-lookup"><span data-stu-id="dfb37-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dfb37-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="dfb37-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="dfb37-107">Portail</span><span class="sxs-lookup"><span data-stu-id="dfb37-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="dfb37-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfb37-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="dfb37-109">REST</span><span class="sxs-lookup"><span data-stu-id="dfb37-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="dfb37-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="dfb37-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="dfb37-111">Mise à l’échelle de la puissance de calcul</span><span class="sxs-lookup"><span data-stu-id="dfb37-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="dfb37-112">toochange des ressources de calcul :</span><span class="sxs-lookup"><span data-stu-id="dfb37-112">toochange compute resources:</span></span>

1. <span data-ttu-id="dfb37-113">Ouvrez hello [portail Azure][Azure portal], ouvrez votre base de données, puis cliquez sur **échelle**.</span><span class="sxs-lookup"><span data-stu-id="dfb37-113">Open hello [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Cliquez sur Mettre à l’échelle.][1]
2. <span data-ttu-id="dfb37-115">Dans le panneau de mise à l’échelle de hello, déplacez le curseur de hello gauche ou vers la droite toochange valeur dwu hello.</span><span class="sxs-lookup"><span data-stu-id="dfb37-115">In hello Scale blade, move hello slider left or right toochange hello DWU setting.</span></span>

    ![Déplacez le curseur][2]
3. <span data-ttu-id="dfb37-117">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="dfb37-117">Click **Save**.</span></span> <span data-ttu-id="dfb37-118">Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="dfb37-118">A confirmation message appears.</span></span> <span data-ttu-id="dfb37-119">Cliquez sur **Oui** tooconfirm ou **aucun** toocancel.</span><span class="sxs-lookup"><span data-stu-id="dfb37-119">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Cliquez sur Enregistrer.][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="dfb37-121">Suspension du calcul</span><span class="sxs-lookup"><span data-stu-id="dfb37-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="dfb37-122">toopause une base de données :</span><span class="sxs-lookup"><span data-stu-id="dfb37-122">toopause a database:</span></span>

1. <span data-ttu-id="dfb37-123">Ouvrez hello [portail Azure] [ Azure portal] et ouvrez votre base de données.</span><span class="sxs-lookup"><span data-stu-id="dfb37-123">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="dfb37-124">Notez que hello état est **Online**.</span><span class="sxs-lookup"><span data-stu-id="dfb37-124">Notice that hello Status is **Online**.</span></span>

    ![État En ligne][6]
2. <span data-ttu-id="dfb37-126">Cliquez sur les ressources de calcul et de mémoire toosuspend, **Pause**, puis un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="dfb37-126">toosuspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="dfb37-127">Cliquez sur **Oui** tooconfirm ou **aucun** toocancel.</span><span class="sxs-lookup"><span data-stu-id="dfb37-127">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Confirmer la pause][7]
3. <span data-ttu-id="dfb37-129">Pendant le démarrage de l’entrepôt de données SQL de la base de données hello, état de hello est **interruption**.</span><span class="sxs-lookup"><span data-stu-id="dfb37-129">While SQL Data Warehouse is starting hello database, hello status is **Pausing**.</span></span>
4. <span data-ttu-id="dfb37-130">Lorsque le statut de hello est **suspendu**, opération de suspension hello est effectuée et que vous êtes en cours n’est plus facturé pour Dwu.</span><span class="sxs-lookup"><span data-stu-id="dfb37-130">When hello status is **Paused**, hello pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![État Pause][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="dfb37-132">Reprise du calcul</span><span class="sxs-lookup"><span data-stu-id="dfb37-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="dfb37-133">tooresume une base de données :</span><span class="sxs-lookup"><span data-stu-id="dfb37-133">tooresume a database:</span></span>

1. <span data-ttu-id="dfb37-134">Ouvrez hello [portail Azure] [ Azure portal] et ouvrez votre base de données.</span><span class="sxs-lookup"><span data-stu-id="dfb37-134">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="dfb37-135">Notez que hello état est **suspendu**.</span><span class="sxs-lookup"><span data-stu-id="dfb37-135">Notice that hello Status is **Paused**.</span></span>

    ![Suspendre la base de données][4]
2. <span data-ttu-id="dfb37-137">Cliquez sur base de données de hello tooresume **Démarrer**, puis un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="dfb37-137">tooresume hello database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="dfb37-138">Cliquez sur **Oui** tooconfirm ou **aucun** toocancel.</span><span class="sxs-lookup"><span data-stu-id="dfb37-138">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Confirmer la reprise][5]
3. <span data-ttu-id="dfb37-140">Pendant le démarrage de l’entrepôt de données SQL de la base de données hello, statut de hello est « Reprise ».</span><span class="sxs-lookup"><span data-stu-id="dfb37-140">While SQL Data Warehouse is starting hello database, hello status is "Resuming".</span></span>
4. <span data-ttu-id="dfb37-141">Lorsque le statut de hello est **online**, base de données hello est prêt.</span><span class="sxs-lookup"><span data-stu-id="dfb37-141">When hello status is **online**, hello database is ready.</span></span>

    ![État En ligne][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="dfb37-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dfb37-143">Next steps</span></span>
<span data-ttu-id="dfb37-144">Pour plus d’informations, consultez la [vue d’ensemble de la gestion][Management overview].</span><span class="sxs-lookup"><span data-stu-id="dfb37-144">For more information, see [Management overview][Management overview].</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
