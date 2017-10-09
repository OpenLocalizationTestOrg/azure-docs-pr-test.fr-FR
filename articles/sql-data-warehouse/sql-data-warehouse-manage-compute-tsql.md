---
title: "aaaPause, reprendre, mettre à l’échelle avec T-SQL dans Azure SQL Data Warehouse | Documents Microsoft"
description: "Transact-SQL (T-SQL) tâches tooscale performances en ajustant les Dwu. Réalisez des économies en réduisant vos ressources pendant les heures creuses."
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
ms.openlocfilehash: 84c6868acb673221d8853319ac9a05bb98b2b7c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="3c274-104">Gestion de la puissance de calcul dans Azure SQL Data Warehouse (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="3c274-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c274-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3c274-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="3c274-106">Portail</span><span class="sxs-lookup"><span data-stu-id="3c274-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="3c274-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c274-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="3c274-108">REST</span><span class="sxs-lookup"><span data-stu-id="3c274-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="3c274-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="3c274-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="3c274-110">Afficher les paramètres d’unités DWU actuels</span><span class="sxs-lookup"><span data-stu-id="3c274-110">View current DWU settings</span></span>
<span data-ttu-id="3c274-111">tooview hello DWU paramètres actuels de vos bases de données :</span><span class="sxs-lookup"><span data-stu-id="3c274-111">tooview hello current DWU settings for your databases:</span></span>

1. <span data-ttu-id="3c274-112">Ouvrez l’Explorateur d’objets SQL Server dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c274-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="3c274-113">Connecter la base de données master toohello associé avec le serveur de base de données SQL logique hello.</span><span class="sxs-lookup"><span data-stu-id="3c274-113">Connect toohello master database associated with hello logical SQL Database server.</span></span>
3. <span data-ttu-id="3c274-114">Sélectionnez dans la vue de gestion dynamique sys.database_service_objectives hello.</span><span class="sxs-lookup"><span data-stu-id="3c274-114">Select from hello sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="3c274-115">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="3c274-115">Here is an example:</span></span> 

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

## <a name="scale-compute"></a><span data-ttu-id="3c274-116">Mise à l’échelle des ressources de calcul</span><span class="sxs-lookup"><span data-stu-id="3c274-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="3c274-117">hello toochange Dwu :</span><span class="sxs-lookup"><span data-stu-id="3c274-117">toochange hello DWUs:</span></span>

1. <span data-ttu-id="3c274-118">Connecter la base de données master toohello associé à votre serveur logique de la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="3c274-118">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="3c274-119">Hello d’utilisation [ALTER DATABASE] [ ALTER DATABASE] l’instruction TSQL.</span><span class="sxs-lookup"><span data-stu-id="3c274-119">Use hello [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="3c274-120">Hello exemple suivant définit hello service niveau objectif tooDW1000 pour la base de données de hello MySQLDW.</span><span class="sxs-lookup"><span data-stu-id="3c274-120">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="3c274-121">Vérification de l’état de la base de données et de la progression de l’opération</span><span class="sxs-lookup"><span data-stu-id="3c274-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="3c274-122">Connecter la base de données master toohello associé à votre serveur logique de la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="3c274-122">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="3c274-123">Envoyer l’état de base de données de requête toocheck</span><span class="sxs-lookup"><span data-stu-id="3c274-123">Submit query toocheck database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="3c274-124">Soumettre l’état de toocheck de requête d’opération</span><span class="sxs-lookup"><span data-stu-id="3c274-124">Submit query toocheck status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="3c274-125">Cette DMV retourne des informations sur les diverses opérations de gestion sur votre entrepôt de données SQL telles que l’état de fonctionnement et hello hello d’opération de hello, qui sera IN_PROGRESS ou s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="3c274-125">This DMV will return information about various management operations on your SQL Data Warehouse such as hello operation and hello state of hello operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="3c274-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3c274-126">Next steps</span></span>
<span data-ttu-id="3c274-127">Pour d’autres tâches de gestion, consultez la rubrique [Vue d’ensemble du système de gestion][Management overview].</span><span class="sxs-lookup"><span data-stu-id="3c274-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
