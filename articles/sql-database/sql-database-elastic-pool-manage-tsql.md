---
title: "T-SQL : Gérer un pool élastique Azure SQL Database | Microsoft Docs"
description: "Utilisez T-SQL toomanage un pool élastique de base de données SQL Azure."
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
ms.openlocfilehash: 666f131b2c88849a1a9ea83381bbc27548e93599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="a2f24-103">Surveiller et gérer un pool élastique avec Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="a2f24-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="a2f24-104">Cette rubrique vous montre comment toomanage évolutive [pools élastiques](sql-database-elastic-pool.md) avec Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="a2f24-104">This topic shows you how toomanage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="a2f24-105">Vous pouvez également créer et gérer un hello Azure pool élastique [portail Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello API REST, ou [c#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="a2f24-105">You can also create and manage an Azure elastic pool hello [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="a2f24-106">Vous pouvez également créer et déplacer des bases de données vers et depuis des pools élastiques à l’aide de [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="a2f24-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="a2f24-107">Hello d’utilisation [Create Database (base de données de SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) et [Alter de Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commandes toocreate et déplacement des bases de données vers et depuis les pools élastiques.</span><span class="sxs-lookup"><span data-stu-id="a2f24-107">Use hello [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands toocreate and move databases into and out of elastic pools.</span></span> <span data-ttu-id="a2f24-108">pool élastique de Hello doit exister avant de pouvoir utiliser ces commandes.</span><span class="sxs-lookup"><span data-stu-id="a2f24-108">hello elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="a2f24-109">Ces commandes affectent uniquement les bases de données.</span><span class="sxs-lookup"><span data-stu-id="a2f24-109">These commands affect only databases.</span></span> <span data-ttu-id="a2f24-110">La création de nouveaux pools hello paramètre et des propriétés du pool (par exemple, Edtu min et max) ne peut pas être modifié avec les commandes T-SQL.</span><span class="sxs-lookup"><span data-stu-id="a2f24-110">Creation of new pools and hello setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="a2f24-111">Créer une base de données regroupée dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="a2f24-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="a2f24-112">Utilisez la commande de créer la base de données de hello avec l’option de SERVICE_OBJECTIVE de hello.</span><span class="sxs-lookup"><span data-stu-id="a2f24-112">Use hello CREATE DATABASE command with hello SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="a2f24-113">Toutes les bases de données dans un pool élastique héritent de niveau de service hello du pool élastique de hello (Basic, Standard, Premium).</span><span class="sxs-lookup"><span data-stu-id="a2f24-113">All databases in an elastic pool inherit hello service tier of hello elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="a2f24-114">Déplacer une base de données entre les pools élastiques</span><span class="sxs-lookup"><span data-stu-id="a2f24-114">Move a database between elastic pools</span></span>
<span data-ttu-id="a2f24-115">Utilisez la commande ALTER DATABASE hello avec hello modifier et configurer SERVICE\_option OBJECTIVE élastique\_POOL.</span><span class="sxs-lookup"><span data-stu-id="a2f24-115">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="a2f24-116">Définir le hello nom toohello nom de pool de cible hello.</span><span class="sxs-lookup"><span data-stu-id="a2f24-116">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="a2f24-117">Déplacer une base de données dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="a2f24-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="a2f24-118">Utilisez la commande ALTER DATABASE hello avec hello modifier et configurer SERVICE\_option OBJECTIVE comme ELASTIC_POOL.</span><span class="sxs-lookup"><span data-stu-id="a2f24-118">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="a2f24-119">Définir le hello nom toohello nom de pool de cible hello.</span><span class="sxs-lookup"><span data-stu-id="a2f24-119">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="a2f24-120">Déplacer une base de données hors d’un pool élastique</span><span class="sxs-lookup"><span data-stu-id="a2f24-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="a2f24-121">Utilisez la commande ALTER DATABASE hello et tooone SERVICE_OBJECTIVE hello hello des niveaux de performances (par exemple, S0 ou S1).</span><span class="sxs-lookup"><span data-stu-id="a2f24-121">Use hello ALTER DATABASE command and set hello SERVICE_OBJECTIVE tooone of hello performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="a2f24-122">Répertorier les bases de données dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="a2f24-122">List databases in an elastic pool</span></span>
<span data-ttu-id="a2f24-123">Hello d’utilisation [sys.database\_service \_objectifs vue](https://msdn.microsoft.com/library/mt712619) toolist tous hello des bases de données dans un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="a2f24-123">Use hello [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) toolist all hello databases in an elastic pool.</span></span> <span data-ttu-id="a2f24-124">Ouvrez une session dans toohello master vue de base de données tooquery hello.</span><span class="sxs-lookup"><span data-stu-id="a2f24-124">Log in toohello master database tooquery hello view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="a2f24-125">Obtenir les données d’utilisation des ressources d’un pool élastique</span><span class="sxs-lookup"><span data-stu-id="a2f24-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="a2f24-126">Hello d’utilisation [sys.elastic\_pool \_ressource \_affichage de statistiques](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello ressource les statistiques d’un pool élastique sur un serveur logique.</span><span class="sxs-lookup"><span data-stu-id="a2f24-126">Use hello [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="a2f24-127">Ouvrez une session dans toohello master vue de base de données tooquery hello.</span><span class="sxs-lookup"><span data-stu-id="a2f24-127">Log in toohello master database tooquery hello view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="a2f24-128">Obtenir les données d’utilisation des ressources d’une base de données mise en pool</span><span class="sxs-lookup"><span data-stu-id="a2f24-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="a2f24-129">Hello d’utilisation [sys.dm\_ db\_ ressource\_affichage de statistiques](https://msdn.microsoft.com/library/dn800981.aspx) ou [sys.resource \_affichage de statistiques](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine hello ressource les statistiques d’une base de données dans un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="a2f24-129">Use hello [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine hello resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="a2f24-130">Ce processus est l’utilisation des ressources tooquerying similaires pour une base de données.</span><span class="sxs-lookup"><span data-stu-id="a2f24-130">This process is similar tooquerying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2f24-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a2f24-131">Next steps</span></span>
<span data-ttu-id="a2f24-132">Après avoir créé un pool élastique, vous pouvez gérer des bases de données élastiques dans le pool de hello en créant des travaux élastique.</span><span class="sxs-lookup"><span data-stu-id="a2f24-132">After creating an elastic pool, you can manage elastic databases in hello pool by creating elastic jobs.</span></span> <span data-ttu-id="a2f24-133">Travaux élastique facilite les scripts T-SQL en cours d’exécution par rapport à n’importe quel nombre de bases de données dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="a2f24-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in hello pool.</span></span> <span data-ttu-id="a2f24-134">Pour en savoir plus, consultez [Vue d'ensemble des tâches de base de données élastiques](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2f24-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="a2f24-135">Consultez [montée en puissance parallèle avec la base de données SQL Azure](sql-database-elastic-scale-introduction.md): utiliser tooscale d’outils de base de données élastique out, de déplacer des données, la requête ou la création des transactions.</span><span class="sxs-lookup"><span data-stu-id="a2f24-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools tooscale out, move data, query, or create transactions.</span></span>

