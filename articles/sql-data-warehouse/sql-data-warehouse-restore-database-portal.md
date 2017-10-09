---
title: aaaRestore Azure SQL Data Warehouse (portail Azure) | Documents Microsoft
description: "Tâches du portail Azure permettant de restaurer Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="b1898-103">Restauration d’Azure SQL Data Warehouse (portail)</span><span class="sxs-lookup"><span data-stu-id="b1898-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="b1898-104">[Vue d’ensemble][Overview]</span><span class="sxs-lookup"><span data-stu-id="b1898-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="b1898-105">[Portail][Portal]</span><span class="sxs-lookup"><span data-stu-id="b1898-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="b1898-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="b1898-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="b1898-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="b1898-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="b1898-108">Dans cet article, vous allez apprendre comment toorestore Azure SQL Data Warehouse à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b1898-108">In this article, you will learn how toorestore Azure SQL Data Warehouse by using hello Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b1898-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="b1898-109">Before you begin</span></span>
<span data-ttu-id="b1898-110">**Vérifiez votre capacité de DTU.**</span><span class="sxs-lookup"><span data-stu-id="b1898-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="b1898-111">Chaque instance de SQL Data Warehouse est hébergée par un serveur SQL (par exemple, myserver.database.windows.net) qui dispose d’un quota d’unité de débit de données (DTU) par défaut.</span><span class="sxs-lookup"><span data-stu-id="b1898-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="b1898-112">Avant de pouvoir restaurer SQL Data Warehouse, vérifiez que votre serveur SQL server dispose de suffisamment restantes du quota UDBD pour la base de données hello que vous restaurez.</span><span class="sxs-lookup"><span data-stu-id="b1898-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for hello database that you're restoring.</span></span> <span data-ttu-id="b1898-113">toolearn du quota UDBD toocalculate ou toorequest Udbd plus, voir [demander une modification du quota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="b1898-113">toolearn how toocalculate DTU quota or toorequest more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="b1898-114">Restauration d’une base de données active ou en pause</span><span class="sxs-lookup"><span data-stu-id="b1898-114">Restore an active or paused database</span></span>
<span data-ttu-id="b1898-115">toorestore une base de données :</span><span class="sxs-lookup"><span data-stu-id="b1898-115">toorestore a database:</span></span>

1. <span data-ttu-id="b1898-116">Connectez-vous à toohello [portail Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="b1898-116">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="b1898-117">Dans le volet gauche de hello, sélectionnez **Parcourir**, puis sélectionnez **serveurs SQL**.</span><span class="sxs-lookup"><span data-stu-id="b1898-117">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Sélectionnez Parcourir > Serveurs SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="b1898-119">Recherchez votre serveur et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="b1898-119">Find your server, and then select it.</span></span>

    ![Sélectionnez votre serveur](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="b1898-121">Occurrence hello de l’entrepôt de données SQL que vous souhaitez toorestore à partir d’et sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="b1898-121">Find hello instance of SQL Data Warehouse that you want toorestore from, and then select it.</span></span>

    ![Sélectionnez l’instance hello de SQL Data Warehouse toorestore](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="b1898-123">Haut hello du Panneau de l’entrepôt de données hello, sélectionnez **restaurer**.</span><span class="sxs-lookup"><span data-stu-id="b1898-123">At hello top of hello Data Warehouse blade, select **Restore**.</span></span>

    ![Sélectionnez Restaurer](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="b1898-125">Spécifiez un nouveau **nom pour la base de données**.</span><span class="sxs-lookup"><span data-stu-id="b1898-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="b1898-126">Sélectionnez hello dernières **point de restauration**.</span><span class="sxs-lookup"><span data-stu-id="b1898-126">Select hello latest **Restore point**.</span></span>

   <span data-ttu-id="b1898-127">Assurez-vous que vous choisissez le dernier point de restauration hello.</span><span class="sxs-lookup"><span data-stu-id="b1898-127">Make sure you choose hello latest restore point.</span></span> <span data-ttu-id="b1898-128">Étant donné que les points de restauration sont affichés dans le temps universel coordonné (UTC), option par défaut de hello peut-être pas le dernier point de restauration hello.</span><span class="sxs-lookup"><span data-stu-id="b1898-128">Because restore points are shown in Coordinated Universal Time (UTC), hello default option might not be hello latest restore point.</span></span>

      ![Sélectionner un point de restauration](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="b1898-130">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1898-130">Select **OK**.</span></span>
9. <span data-ttu-id="b1898-131">processus de restauration de base de données Hello commence, et vous pouvez utiliser **NOTIFICATIONS** processus de hello toomonitor.</span><span class="sxs-lookup"><span data-stu-id="b1898-131">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="b1898-132">Après la restauration de hello terminée, vous pouvez configurer votre base de données récupérée en suivant [configurer votre base de données après récupération][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="b1898-132">After hello restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="b1898-133">restauration d’une base de données supprimée.</span><span class="sxs-lookup"><span data-stu-id="b1898-133">Restore a deleted database</span></span>
<span data-ttu-id="b1898-134">toorestore une base de données supprimée :</span><span class="sxs-lookup"><span data-stu-id="b1898-134">toorestore a deleted database:</span></span>

1. <span data-ttu-id="b1898-135">Connectez-vous à toohello [portail Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="b1898-135">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="b1898-136">Dans le volet gauche de hello, sélectionnez **Parcourir**, puis sélectionnez **serveurs SQL**.</span><span class="sxs-lookup"><span data-stu-id="b1898-136">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Sélectionnez Parcourir > Serveurs SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="b1898-138">Recherchez votre serveur et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="b1898-138">Find your server, and then select it.</span></span>

    ![Sélectionnez votre serveur](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="b1898-140">Faites défiler vers le bas toohello **Operations** section sur le panneau de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="b1898-140">Scroll down toohello **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="b1898-141">Sélectionnez hello **bases de données supprimées** vignette.</span><span class="sxs-lookup"><span data-stu-id="b1898-141">Select hello **Deleted databases** tile.</span></span>

    ![Sélectionnez la vignette de bases de données supprimées hello](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="b1898-143">Sélectionnez hello supprimé de la base de données que vous souhaitez toorestore.</span><span class="sxs-lookup"><span data-stu-id="b1898-143">Select hello deleted database that you want toorestore.</span></span>

    ![Sélectionnez un toorestore de la base de données](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="b1898-145">Spécifiez un nouveau **nom pour la base de données**.</span><span class="sxs-lookup"><span data-stu-id="b1898-145">Specify a new **Database name**.</span></span>

    ![Ajouter un nom pour la base de données hello](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="b1898-147">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1898-147">Select **OK**.</span></span>
9. <span data-ttu-id="b1898-148">processus de restauration de base de données Hello commence, et vous pouvez utiliser **NOTIFICATIONS** processus de hello toomonitor.</span><span class="sxs-lookup"><span data-stu-id="b1898-148">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="b1898-149">reportez-vous à votre base de données après restauration de hello, tooconfigure [configurer votre base de données après récupération][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="b1898-149">tooconfigure your database after hello restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="b1898-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b1898-150">Next steps</span></span>
<span data-ttu-id="b1898-151">toolearn sur les fonctionnalités de continuité d’activité d’entreprise hello des éditions de base de données SQL Azure, lisez hello [vue d’ensemble de base de données SQL Azure business la continuité des activités][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="b1898-151">toolearn about hello business continuity features of Azure SQL Database editions, read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
