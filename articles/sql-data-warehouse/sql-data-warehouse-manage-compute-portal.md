---
title: "Gestion de la puissance de calcul dans Azure SQL Data Warehouse (portail Azure) | Microsoft Docs"
description: "Tâches du portail Azure permettant de gérer la puissance de calcul. Mettez à l’échelle les ressources de calcul en ajustant les unités DWU. Ou suspendez et reprenez des ressources de calcul pour réduire les coûts."
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
ms.openlocfilehash: 63888d5dd103b585cf18e4787d3e779810163e3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="fd742-105">Gestion de la puissance de calcul dans Azure SQL Data Warehouse (portail Azure)</span><span class="sxs-lookup"><span data-stu-id="fd742-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd742-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="fd742-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="fd742-107">Portail</span><span class="sxs-lookup"><span data-stu-id="fd742-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="fd742-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd742-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="fd742-109">REST</span><span class="sxs-lookup"><span data-stu-id="fd742-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="fd742-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="fd742-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="fd742-111">Mise à l’échelle de la puissance de calcul</span><span class="sxs-lookup"><span data-stu-id="fd742-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="fd742-112">Pour modifier les ressources de calcul :</span><span class="sxs-lookup"><span data-stu-id="fd742-112">To change compute resources:</span></span>

1. <span data-ttu-id="fd742-113">Ouvrez le [portail Azure][Azure portal], ouvrez votre base de données, puis cliquez sur **Mettre à l’échelle**.</span><span class="sxs-lookup"><span data-stu-id="fd742-113">Open the [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Cliquez sur Mettre à l’échelle.][1]
2. <span data-ttu-id="fd742-115">Dans le panneau de mise à l’échelle, déplacez le curseur vers la gauche ou vers la droite pour modifier le paramètre DWU.</span><span class="sxs-lookup"><span data-stu-id="fd742-115">In the Scale blade, move the slider left or right to change the DWU setting.</span></span>

    ![Déplacez le curseur][2]
3. <span data-ttu-id="fd742-117">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="fd742-117">Click **Save**.</span></span> <span data-ttu-id="fd742-118">Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fd742-118">A confirmation message appears.</span></span> <span data-ttu-id="fd742-119">Cliquez sur **Oui** pour confirmer ou sur **Non** pour annuler.</span><span class="sxs-lookup"><span data-stu-id="fd742-119">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Cliquez sur Enregistrer.][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="fd742-121">Suspension du calcul</span><span class="sxs-lookup"><span data-stu-id="fd742-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="fd742-122">Pour suspendre une base de données :</span><span class="sxs-lookup"><span data-stu-id="fd742-122">To pause a database:</span></span>

1. <span data-ttu-id="fd742-123">Ouvrez le [portail Azure][Azure portal], puis votre base de données.</span><span class="sxs-lookup"><span data-stu-id="fd742-123">Open the [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="fd742-124">Notez que l’état est **En ligne**.</span><span class="sxs-lookup"><span data-stu-id="fd742-124">Notice that the Status is **Online**.</span></span>

    ![État En ligne][6]
2. <span data-ttu-id="fd742-126">Pour interrompre les ressources de calcul et de mémoire, cliquez sur **Pause**. Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fd742-126">To suspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="fd742-127">Cliquez sur **Oui** pour confirmer ou sur **Non** pour annuler.</span><span class="sxs-lookup"><span data-stu-id="fd742-127">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Confirmer la pause][7]
3. <span data-ttu-id="fd742-129">Lorsque SQL Data Warehouse démarre la base de données, l’état est **Interruption**.</span><span class="sxs-lookup"><span data-stu-id="fd742-129">While SQL Data Warehouse is starting the database, the status is **Pausing**.</span></span>
4. <span data-ttu-id="fd742-130">Lorsque l’état est **Interrompu**, l’opération d’interruption est effectuée et aucune DWU ne vous est plus facturée.</span><span class="sxs-lookup"><span data-stu-id="fd742-130">When the status is **Paused**, the pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![État Pause][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="fd742-132">Reprise du calcul</span><span class="sxs-lookup"><span data-stu-id="fd742-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="fd742-133">Pour reprendre une base de données :</span><span class="sxs-lookup"><span data-stu-id="fd742-133">To resume a database:</span></span>

1. <span data-ttu-id="fd742-134">Ouvrez le [portail Azure][Azure portal], puis votre base de données.</span><span class="sxs-lookup"><span data-stu-id="fd742-134">Open the [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="fd742-135">Notez que l’état est **Suspendu**.</span><span class="sxs-lookup"><span data-stu-id="fd742-135">Notice that the Status is **Paused**.</span></span>

    ![Suspendre la base de données][4]
2. <span data-ttu-id="fd742-137">Pour relancer la base de données, cliquez sur **Démarrer**. Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fd742-137">To resume the database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="fd742-138">Cliquez sur **Oui** pour confirmer ou sur **Non** pour annuler.</span><span class="sxs-lookup"><span data-stu-id="fd742-138">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Confirmer la reprise][5]
3. <span data-ttu-id="fd742-140">Lorsque SQL Data Warehouse démarre la base de données, l’état est « Reprise ».</span><span class="sxs-lookup"><span data-stu-id="fd742-140">While SQL Data Warehouse is starting the database, the status is "Resuming".</span></span>
4. <span data-ttu-id="fd742-141">Lorsque l’état est **En ligne**, la base de données est prête.</span><span class="sxs-lookup"><span data-stu-id="fd742-141">When the status is **online**, the database is ready.</span></span>

    ![État En ligne][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="fd742-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fd742-143">Next steps</span></span>
<span data-ttu-id="fd742-144">Pour plus d’informations, consultez la [vue d’ensemble de la gestion][Management overview].</span><span class="sxs-lookup"><span data-stu-id="fd742-144">For more information, see [Management overview][Management overview].</span></span>

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
