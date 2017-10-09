---
title: "Azure SQL de base de données à l’aide de vues de gestion dynamique d’aaaMonitoring | Documents Microsoft"
description: "Découvrez comment toodetect et diagnostiquer les problèmes de performances courants à l’aide de vues de gestion dynamique toomonitor base de données SQL Microsoft Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: d08f505f-3c62-47d4-bab7-35c9a834b79b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 43d5fe2dd9a38d031e9334f6ad49fce5866e3bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="5262f-103">Analyse d’une base de données SQL Azure à l’aide de vues de gestion dynamique</span><span class="sxs-lookup"><span data-stu-id="5262f-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="5262f-104">Base de données SQL Microsoft Azure permet un sous-ensemble de gestion dynamique affiche toodiagnose des problèmes de performances, ce qui peuvent être dû à des requêtes longues ou bloquées, des goulots d’étranglement, plans de requête médiocres et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="5262f-104">Microsoft Azure SQL Database enables a subset of dynamic management views toodiagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="5262f-105">Cette rubrique fournit des informations sur la façon de toodetect les problèmes de performances courants à l’aide de vues de gestion dynamique.</span><span class="sxs-lookup"><span data-stu-id="5262f-105">This topic provides information on how toodetect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="5262f-106">La base de données SQL prend partiellement en charge trois catégories de vues de gestion dynamique :</span><span class="sxs-lookup"><span data-stu-id="5262f-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="5262f-107">vues de gestion dynamique liées à la base de données ;</span><span class="sxs-lookup"><span data-stu-id="5262f-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="5262f-108">vues de gestion dynamique liées à l’exécution ;</span><span class="sxs-lookup"><span data-stu-id="5262f-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="5262f-109">vues de gestion dynamique liées à la transaction.</span><span class="sxs-lookup"><span data-stu-id="5262f-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="5262f-110">Pour plus d’informations sur les vues de gestion dynamique, voir [Fonctions et vues de gestion dynamique (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) dans la documentation en ligne de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5262f-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="5262f-111">Autorisations</span><span class="sxs-lookup"><span data-stu-id="5262f-111">Permissions</span></span>
<span data-ttu-id="5262f-112">Dans la base de données SQL, l’interrogation d’une vue de gestion dynamique nécessite des autorisations **AFFICHER L'ÉTAT DE LA BASE DE DONNÉES** .</span><span class="sxs-lookup"><span data-stu-id="5262f-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="5262f-113">Hello **VIEW DATABASE STATE** autorisation retourne des informations sur tous les objets de base de données actuelle hello.</span><span class="sxs-lookup"><span data-stu-id="5262f-113">hello **VIEW DATABASE STATE** permission returns information about all objects within hello current database.</span></span>
<span data-ttu-id="5262f-114">toogrant hello **VIEW DATABASE STATE** autorisation tooa utilisateur spécifique, exécutez hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="5262f-114">toogrant hello **VIEW DATABASE STATE** permission tooa specific database user, run hello following query:</span></span>

```GRANT VIEW DATABASE STATE toodatabase_user; ```

<span data-ttu-id="5262f-115">Dans une instance de SQL Server local, des vues de gestion dynamiques renvoient des informations sur l’état du serveur.</span><span class="sxs-lookup"><span data-stu-id="5262f-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="5262f-116">Dans Base de données SQL, elles renvoient des informations relatives à votre base de données logique actuelle.</span><span class="sxs-lookup"><span data-stu-id="5262f-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="5262f-117">Calcul de la taille de la base de données</span><span class="sxs-lookup"><span data-stu-id="5262f-117">Calculating database size</span></span>
<span data-ttu-id="5262f-118">Hello requête suivante renvoie taille hello de votre base de données (en mégaoctets) :</span><span class="sxs-lookup"><span data-stu-id="5262f-118">hello following query returns hello size of your database (in megabytes):</span></span>

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="5262f-119">Hello requête suivante renvoie hello taille des objets individuels (en mégaoctets) dans votre base de données :</span><span class="sxs-lookup"><span data-stu-id="5262f-119">hello following query returns hello size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="5262f-120">Analyse des connexions</span><span class="sxs-lookup"><span data-stu-id="5262f-120">Monitoring connections</span></span>
<span data-ttu-id="5262f-121">Vous pouvez utiliser hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) tooretrieve des informations sur le serveur de base de données SQL Azure spécifique hello connexions établies tooa et les détails de hello de chaque connexion.</span><span class="sxs-lookup"><span data-stu-id="5262f-121">You can use hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view tooretrieve information about hello connections established tooa specific Azure SQL Database server and hello details of each connection.</span></span> <span data-ttu-id="5262f-122">En outre, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) vue est utile lors de la récupération des informations sur toutes les connexions utilisateur actives et les tâches internes.</span><span class="sxs-lookup"><span data-stu-id="5262f-122">In addition, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="5262f-123">Hello requête suivante récupère des informations sur la connexion en cours de hello :</span><span class="sxs-lookup"><span data-stu-id="5262f-123">hello following query retrieves information on hello current connection:</span></span>

```
SELECT
    c.session_id, c.net_transport, c.encrypt_option,
    c.auth_scheme, s.host_name, s.program_name,
    s.client_interface_name, s.login_name, s.nt_domain,
    s.nt_user_name, s.original_login_name, c.connect_time,
    s.login_time
FROM sys.dm_exec_connections AS c
JOIN sys.dm_exec_sessions AS s
    ON c.session_id = s.session_id
WHERE c.session_id = @@SPID;
```

> [!NOTE]
> <span data-ttu-id="5262f-124">Lors de l’exécution hello **sys.dm_exec_requests** et **des vues sys.dm_exec_sessions**, si vous avez **VIEW DATABASE STATE** autorisation sur la base de données hello, reportez-vous à l’exécution de toutes les sessions de base de données hello ; Sinon, vous verrez uniquement hello session active.</span><span class="sxs-lookup"><span data-stu-id="5262f-124">When executing hello **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on hello database, you see all executing sessions on hello database; otherwise, you see only hello current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="5262f-125">Analyse des performances des requêtes</span><span class="sxs-lookup"><span data-stu-id="5262f-125">Monitoring query performance</span></span>
<span data-ttu-id="5262f-126">Des requêtes lentes ou longues peuvent consommer des ressources système significatives.</span><span class="sxs-lookup"><span data-stu-id="5262f-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="5262f-127">Cette section montre comment toouse vues de gestion dynamiques toodetect quelques problèmes de performances de requête courants.</span><span class="sxs-lookup"><span data-stu-id="5262f-127">This section demonstrates how toouse dynamic management views toodetect a few common query performance problems.</span></span> <span data-ttu-id="5262f-128">Une référence plus anciens, mais toujours utile pour le dépannage, est hello [résolution des problèmes de performances dans SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article sur Microsoft TechNet.</span><span class="sxs-lookup"><span data-stu-id="5262f-128">An older but still helpful reference for troubleshooting, is hello [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="5262f-129">Recherche des N premières requêtes</span><span class="sxs-lookup"><span data-stu-id="5262f-129">Finding top N queries</span></span>
<span data-ttu-id="5262f-130">Hello exemple suivant retourne des informations sur hello cinq premières requêtes classées d’après le temps processeur moyen.</span><span class="sxs-lookup"><span data-stu-id="5262f-130">hello following example returns information about hello top five queries ranked by average CPU time.</span></span> <span data-ttu-id="5262f-131">Cet exemple regroupe les requêtes hello en tootheir en fonction de hachage de requête, afin que les requêtes logiquement équivalentes soient groupées par leur consommation de ressources cumulative.</span><span class="sxs-lookup"><span data-stu-id="5262f-131">This example aggregates hello queries according tootheir query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

```
SELECT TOP 5 query_stats.query_hash AS "Query Hash",
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",
    MIN(query_stats.statement_text) AS "Statement Text"
FROM
    (SELECT QS.*,
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,
    ((CASE statement_end_offset
        WHEN -1 THEN DATALENGTH(ST.text)
        ELSE QS.statement_end_offset END
            - QS.statement_start_offset)/2) + 1) AS statement_text
     FROM sys.dm_exec_query_stats AS QS
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats
GROUP BY query_stats.query_hash
ORDER BY 2 DESC;
```

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="5262f-132">Surveillance des requêtes bloquées</span><span class="sxs-lookup"><span data-stu-id="5262f-132">Monitoring blocked queries</span></span>
<span data-ttu-id="5262f-133">Les requêtes lentes ou longues peuvent contribuer tooexcessive la consommation des ressources et être la conséquence de hello de requêtes bloquées.</span><span class="sxs-lookup"><span data-stu-id="5262f-133">Slow or long-running queries can contribute tooexcessive resource consumption and be hello consequence of blocked queries.</span></span> <span data-ttu-id="5262f-134">cause Hello hello blocage peut être une mauvaise conception de l’application, mauvais plans de requête, hello manque d’index utiles et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="5262f-134">hello cause of hello blocking can be poor application design, bad query plans, hello lack of useful indexes, and so on.</span></span> <span data-ttu-id="5262f-135">Vous pouvez utiliser hello sys.dm_tran_locks afficher tooget des informations sur l’activité hello de verrouillage actuelle dans votre base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5262f-135">You can use hello sys.dm_tran_locks view tooget information about hello current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="5262f-136">Pour un exemple de code, voir [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) dans la documentation en ligne de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5262f-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="5262f-137">Analyse des plans de requête</span><span class="sxs-lookup"><span data-stu-id="5262f-137">Monitoring query plans</span></span>
<span data-ttu-id="5262f-138">Un plan de requête inefficace peut également augmenter la consommation du processeur.</span><span class="sxs-lookup"><span data-stu-id="5262f-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="5262f-139">exemple Hello utilise hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) afficher toodetermine requête qui utilise les UC plus cumulative hello.</span><span class="sxs-lookup"><span data-stu-id="5262f-139">hello following example uses hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view toodetermine which query uses hello most cumulative CPU.</span></span>

```
SELECT
    highest_cpu_queries.plan_handle,
    highest_cpu_queries.total_worker_time,
    q.dbid,
    q.objectid,
    q.number,
    q.encrypted,
    q.[text]
FROM
    (SELECT TOP 50
        qs.plan_handle,
        qs.total_worker_time
    FROM
        sys.dm_exec_query_stats qs
    ORDER BY qs.total_worker_time desc) AS highest_cpu_queries
    CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS q
ORDER BY highest_cpu_queries.total_worker_time DESC;
```

## <a name="see-also"></a><span data-ttu-id="5262f-140">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5262f-140">See also</span></span>
[<span data-ttu-id="5262f-141">Introduction tooSQL de base de données</span><span class="sxs-lookup"><span data-stu-id="5262f-141">Introduction tooSQL Database</span></span>](sql-database-technical-overview.md)

