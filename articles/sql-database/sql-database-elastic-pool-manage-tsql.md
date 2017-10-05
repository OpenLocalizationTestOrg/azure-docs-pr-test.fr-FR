---
title: "T-SQL : Gérer un pool élastique Azure SQL Database | Microsoft Docs"
description: "Utilisez T-SQL pour gérer un pool élastique Azure SQL Database."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: c6b64e4a7fd91283a37a792b294965064d653003
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="1084f-103">Surveiller et gérer un pool élastique avec Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="1084f-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="1084f-104">Cette rubrique vous montre comment créer des [pools élastiques](sql-database-elastic-pool.md) évolutifs avec Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="1084f-104">This topic shows you how to manage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="1084f-105">Vous pouvez également créer et gérer un pool élastique Azure avec le [Portail Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), l’API REST ou [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="1084f-105">You can also create and manage an Azure elastic pool the [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="1084f-106">Vous pouvez également créer et déplacer des bases de données vers et depuis des pools élastiques à l’aide de [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="1084f-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="1084f-107">Utilisez les commandes [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) et [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) pour créer et déplacer les bases de données dans et en dehors des pools élastiques.</span><span class="sxs-lookup"><span data-stu-id="1084f-107">Use the [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands to create and move databases into and out of elastic pools.</span></span> <span data-ttu-id="1084f-108">Le pool élastique doit exister avant de pouvoir utiliser ces commandes.</span><span class="sxs-lookup"><span data-stu-id="1084f-108">The elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="1084f-109">Ces commandes affectent uniquement les bases de données.</span><span class="sxs-lookup"><span data-stu-id="1084f-109">These commands affect only databases.</span></span> <span data-ttu-id="1084f-110">La création de nouveaux pools et le paramétrage des propriétés du pool (telles qu’eDTU min. et max.) ne peuvent pas être modifiés avec les commandes T-SQL.</span><span class="sxs-lookup"><span data-stu-id="1084f-110">Creation of new pools and the setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="1084f-111">Créer une base de données regroupée dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="1084f-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="1084f-112">Utilisez la commande CREATE DATABASE avec l’option SERVICE_OBJECTIVE.</span><span class="sxs-lookup"><span data-stu-id="1084f-112">Use the CREATE DATABASE command with the SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="1084f-113">Toutes les bases de données d’un pool élastique héritent du niveau de service du pool élastique (De base, Standard, Premium).</span><span class="sxs-lookup"><span data-stu-id="1084f-113">All databases in an elastic pool inherit the service tier of the elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="1084f-114">Déplacer une base de données entre les pools élastiques</span><span class="sxs-lookup"><span data-stu-id="1084f-114">Move a database between elastic pools</span></span>
<span data-ttu-id="1084f-115">Utilisez la commande ALTER DATABASE avec l’option MODIFY puis définissez l’option SERVICE\_OBJECTIVE sur ELASTIC\_POOL.</span><span class="sxs-lookup"><span data-stu-id="1084f-115">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="1084f-116">Définissez le nom sur le nom du pool cible.</span><span class="sxs-lookup"><span data-stu-id="1084f-116">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move the database named db1 to an elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="1084f-117">Déplacer une base de données dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="1084f-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="1084f-118">Utilisez la commande ALTER DATABASE avec l’option MODIFY puis définissez l’option SERVICE\_OBJECTIVE sur ELASTIC_POOL.</span><span class="sxs-lookup"><span data-stu-id="1084f-118">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="1084f-119">Définissez le nom sur le nom du pool cible.</span><span class="sxs-lookup"><span data-stu-id="1084f-119">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move the database named db1 to an elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="1084f-120">Déplacer une base de données hors d’un pool élastique</span><span class="sxs-lookup"><span data-stu-id="1084f-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="1084f-121">Utilisez la commande ALTER DATABASE et définir l’option SERVICE_OBJECTIVE sur l’un des niveaux de performances (par exemple S0 ou S1).</span><span class="sxs-lookup"><span data-stu-id="1084f-121">Use the ALTER DATABASE command and set the SERVICE_OBJECTIVE to one of the performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes the database into a stand-alone database with the service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="1084f-122">Répertorier les bases de données dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="1084f-122">List databases in an elastic pool</span></span>
<span data-ttu-id="1084f-123">Utilisez la vue [sys.database\_service \_objectives](https://msdn.microsoft.com/library/mt712619) pour répertorier toutes les bases de données dans un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="1084f-123">Use the [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) to list all the databases in an elastic pool.</span></span> <span data-ttu-id="1084f-124">Connectez-vous à la base de données MASTER pour interroger la vue.</span><span class="sxs-lookup"><span data-stu-id="1084f-124">Log in to the master database to query the view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="1084f-125">Obtenir les données d’utilisation des ressources d’un pool élastique</span><span class="sxs-lookup"><span data-stu-id="1084f-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="1084f-126">Utilisez la vue [sys.elastic\_pool \_resource \_stats](https://msdn.microsoft.com/library/mt280062.aspx) pour examiner les statistiques d’utilisation des ressources d’un pool élastique sur un serveur logique.</span><span class="sxs-lookup"><span data-stu-id="1084f-126">Use the [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) to examine the resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="1084f-127">Connectez-vous à la base de données MASTER pour interroger la vue.</span><span class="sxs-lookup"><span data-stu-id="1084f-127">Log in to the master database to query the view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="1084f-128">Obtenir les données d’utilisation des ressources d’une base de données mise en pool</span><span class="sxs-lookup"><span data-stu-id="1084f-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="1084f-129">Utilisez la vue [sys.dm\_ db\_ resource\_stats](https://msdn.microsoft.com/library/dn800981.aspx) ou [sys.resource \_stats](https://msdn.microsoft.com/library/dn269979.aspx) pour examiner les statistiques d’utilisation des ressources d’une base de données dans un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="1084f-129">Use the [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) to examine the resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="1084f-130">Ce processus revient à interroger l’utilisation des ressources pour une base de données unique.</span><span class="sxs-lookup"><span data-stu-id="1084f-130">This process is similar to querying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1084f-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1084f-131">Next steps</span></span>
<span data-ttu-id="1084f-132">Après avoir créé un pool élastique, vous pouvez gérer des bases de données élastiques du pool en créant des tâches élastiques.</span><span class="sxs-lookup"><span data-stu-id="1084f-132">After creating an elastic pool, you can manage elastic databases in the pool by creating elastic jobs.</span></span> <span data-ttu-id="1084f-133">Les tâches élastiques facilitent l'exécution de scripts T-SQL, quel que soit le nombre de bases de données dans le pool.</span><span class="sxs-lookup"><span data-stu-id="1084f-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in the pool.</span></span> <span data-ttu-id="1084f-134">Pour en savoir plus, consultez [Vue d'ensemble des tâches de base de données élastiques](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1084f-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="1084f-135">Consultez [Montée en charge avec la base de données SQL Azure](sql-database-elastic-scale-introduction.md): utilisez les outils de base de données élastique pour monter en charge, déplacer des données, exécuter des requêtes ou créer des transactions.</span><span class="sxs-lookup"><span data-stu-id="1084f-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools to scale out, move data, query, or create transactions.</span></span>

