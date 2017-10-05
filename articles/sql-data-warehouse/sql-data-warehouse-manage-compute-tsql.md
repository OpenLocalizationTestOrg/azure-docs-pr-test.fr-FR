---
title: "Suspendre, reprendre et mettre à l’échelle avec T-SQL dans Azure SQL Data Warehouse | Microsoft Docs"
description: "Tâches Transact-SQL (T-SQL) permettant une montée en puissance des performances en ajustant les unités DWU. Réalisez des économies en réduisant vos ressources pendant les heures creuses."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: a970d939-2adf-4856-8a78-d4fe8ab2cceb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/30/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 9221d72ecf8ab2ba8b04e4bc97eeef7157817cca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="c1b38-104">Gestion de la puissance de calcul dans Azure SQL Data Warehouse (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="c1b38-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1b38-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c1b38-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="c1b38-106">Portail</span><span class="sxs-lookup"><span data-stu-id="c1b38-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="c1b38-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1b38-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="c1b38-108">REST</span><span class="sxs-lookup"><span data-stu-id="c1b38-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="c1b38-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="c1b38-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="c1b38-110">Afficher les paramètres d’unités DWU actuels</span><span class="sxs-lookup"><span data-stu-id="c1b38-110">View current DWU settings</span></span>
<span data-ttu-id="c1b38-111">Pour afficher les paramètres d’unités DWU actuels pour vos bases de données :</span><span class="sxs-lookup"><span data-stu-id="c1b38-111">To view the current DWU settings for your databases:</span></span>

1. <span data-ttu-id="c1b38-112">Ouvrez l’Explorateur d’objets SQL Server dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c1b38-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="c1b38-113">Connectez-vous à la base de données associée au serveur de base de données SQL logique.</span><span class="sxs-lookup"><span data-stu-id="c1b38-113">Connect to the master database associated with the logical SQL Database server.</span></span>
3. <span data-ttu-id="c1b38-114">Sélectionnez dans la vue de gestion dynamique sys.database_service_objectives.</span><span class="sxs-lookup"><span data-stu-id="c1b38-114">Select from the sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="c1b38-115">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="c1b38-115">Here is an example:</span></span> 

```sql
SELECT
    db.name [Database]
,   ds.edition [Edition]
,   ds.service_objective [Service Objective]
FROM
    sys.database_service_objectives ds
JOIN
    sys.databases db ON ds.database_id = db.database_id
```

<a name="scale-dwu-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="c1b38-116">Mise à l’échelle des ressources de calcul</span><span class="sxs-lookup"><span data-stu-id="c1b38-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="c1b38-117">Pour modifier les unités DWU :</span><span class="sxs-lookup"><span data-stu-id="c1b38-117">To change the DWUs:</span></span>

1. <span data-ttu-id="c1b38-118">Connectez-vous à la base de données associée à votre serveur de base de données SQL logique.</span><span class="sxs-lookup"><span data-stu-id="c1b38-118">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="c1b38-119">Utilisez l’instruction TSQL [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="c1b38-119">Use the [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="c1b38-120">L'exemple suivant définit l'objectif de niveau de service sur DW1000 pour la base de données MySQLDW.</span><span class="sxs-lookup"><span data-stu-id="c1b38-120">The following example sets the service level objective to DW1000 for the database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="c1b38-121">Vérification de l’état de la base de données et de la progression de l’opération</span><span class="sxs-lookup"><span data-stu-id="c1b38-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="c1b38-122">Connectez-vous à la base de données associée à votre serveur de base de données SQL logique.</span><span class="sxs-lookup"><span data-stu-id="c1b38-122">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="c1b38-123">Envoyer une requête pour vérifier l’état de la base de données</span><span class="sxs-lookup"><span data-stu-id="c1b38-123">Submit query to check database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="c1b38-124">Envoyer une requête pour vérifier l’état de l’opération</span><span class="sxs-lookup"><span data-stu-id="c1b38-124">Submit query to check status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="c1b38-125">Cette vue de gestion dynamique retourne des informations sur diverses opérations de gestion de votre SQL Data Warehouse, comme l’opération et l’état de l’opération, qui aura la valeur IN_PROGRESS ou COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="c1b38-125">This DMV will return information about various management operations on your SQL Data Warehouse such as the operation and the state of the operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="c1b38-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1b38-126">Next steps</span></span>
<span data-ttu-id="c1b38-127">Pour d’autres tâches de gestion, consultez la rubrique [Vue d’ensemble du système de gestion][Management overview].</span><span class="sxs-lookup"><span data-stu-id="c1b38-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
