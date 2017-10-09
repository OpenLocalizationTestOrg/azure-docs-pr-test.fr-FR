---
title: "aaaMonitor votre charge de travail à l’aide des DMV | Documents Microsoft"
description: "Découvrez comment toomonitor votre charge de travail à l’aide de vues de gestion dynamique."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 69ecd479-0941-48df-b3d0-cf54c79e6549
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: acccf952d165ccec3de3b4b1c633b18bbbf78077
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="a2982-103">Surveiller votre charge de travail à l'aide de vues de gestion dynamique</span><span class="sxs-lookup"><span data-stu-id="a2982-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="a2982-104">Cet article décrit comment toomonitor de vues de gestion dynamique (DMV) toouse votre charge de travail et examiner l’exécution de requête dans l’entrepôt de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a2982-104">This article describes how toouse Dynamic Management Views (DMVs) toomonitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="a2982-105">Autorisations</span><span class="sxs-lookup"><span data-stu-id="a2982-105">Permissions</span></span>
<span data-ttu-id="a2982-106">tooquery hello DMV dans cet article, vous devez avoir l’autorisation VIEW DATABASE STATE ou de contrôle.</span><span class="sxs-lookup"><span data-stu-id="a2982-106">tooquery hello DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="a2982-107">Octroi à l’état de base de données d’affichage est généralement des autorisations de hello préféré car il est beaucoup plus restrictive.</span><span class="sxs-lookup"><span data-stu-id="a2982-107">Usually granting VIEW DATABASE STATE is hello preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="a2982-108">Suivi des connexions</span><span class="sxs-lookup"><span data-stu-id="a2982-108">Monitor connections</span></span>
<span data-ttu-id="a2982-109">Toutes les connexions tooSQL l’entrepôt de données sont enregistrés trop[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="a2982-109">All logins tooSQL Data Warehouse are logged too[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="a2982-110">Cette DMV contient hello 10 000 connexions de la dernière.</span><span class="sxs-lookup"><span data-stu-id="a2982-110">This DMV contains hello last 10,000 logins.</span></span>  <span data-ttu-id="a2982-111">Hello session_id est la clé primaire de hello et assignés de façon séquentielle pour chaque ouverture de session.</span><span class="sxs-lookup"><span data-stu-id="a2982-111">hello session_id is hello primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="a2982-112">Surveillance de l’exécution des rêquetes</span><span class="sxs-lookup"><span data-stu-id="a2982-112">Monitor query execution</span></span>
<span data-ttu-id="a2982-113">Toutes les requêtes exécutées sur l’entrepôt de données SQL sont enregistrés trop[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="a2982-113">All queries executed on SQL Data Warehouse are logged too[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="a2982-114">Cette DMV contient hello dernière 10 000 requêtes exécutées.</span><span class="sxs-lookup"><span data-stu-id="a2982-114">This DMV contains hello last 10,000 queries executed.</span></span>  <span data-ttu-id="a2982-115">Hello request_id identifie chaque requête de manière unique et est hello de clé primaire pour cette vue de gestion dynamique.</span><span class="sxs-lookup"><span data-stu-id="a2982-115">hello request_id uniquely identifies each query and is hello primary key for this DMV.</span></span>  <span data-ttu-id="a2982-116">Hello request_id est attribué de manière séquentielle pour chaque nouvelle requête et est préfixé avec QID, ce qui correspond à l’ID de requête.</span><span class="sxs-lookup"><span data-stu-id="a2982-116">hello request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="a2982-117">En interrogeant cette DMV pour un ID de session (session_id) donné, vous obtenez toutes les requêtes pour une connexion donnée.</span><span class="sxs-lookup"><span data-stu-id="a2982-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="a2982-118">Les procédures stockées utilisent plusieurs ID de requête.</span><span class="sxs-lookup"><span data-stu-id="a2982-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="a2982-119">Les ID de requête sont affectés dans un ordre séquentiel.</span><span class="sxs-lookup"><span data-stu-id="a2982-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="a2982-120">Vous trouverez ici les plans d’exécution étapes toofollow tooinvestigate et les heures pour une requête particulière.</span><span class="sxs-lookup"><span data-stu-id="a2982-120">Here are steps toofollow tooinvestigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a><span data-ttu-id="a2982-121">ÉTAPE 1 : Identifier la requête hello que vous souhaitez tooinvestigate</span><span class="sxs-lookup"><span data-stu-id="a2982-121">STEP 1: Identify hello query you wish tooinvestigate</span></span>
```sql
-- Monitor active queries
SELECT * 
FROM sys.dm_pdw_exec_requests 
WHERE status not in ('Completed','Failed','Cancelled')
  AND session_id <> session_id()
ORDER BY submit_time DESC;

-- Find top 10 queries longest running queries
SELECT TOP 10 * 
FROM sys.dm_pdw_exec_requests 
ORDER BY total_elapsed_time DESC;

-- Find a query with hello Label 'My Query'
-- Use brackets when querying hello label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="a2982-122">À partir de hello précédant les résultats de la requête, **hello de note ID de demande** de requête hello que vous aimeriez tooinvestigate.</span><span class="sxs-lookup"><span data-stu-id="a2982-122">From hello preceding query results, **note hello Request ID** of hello query that you would like tooinvestigate.</span></span>

<span data-ttu-id="a2982-123">Requêtes Bonjour **Suspended** état sont en file d’attente en raison des limites de tooconcurrency.</span><span class="sxs-lookup"><span data-stu-id="a2982-123">Queries in hello **Suspended** state are being queued due tooconcurrency limits.</span></span> <span data-ttu-id="a2982-124">Ces requêtes apparaissent également dans hello sys.dm_pdw_waits attentes de requête avec un type de UserConcurrencyResourceType.</span><span class="sxs-lookup"><span data-stu-id="a2982-124">These queries also appear in hello sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="a2982-125">Pour plus d’informations sur les limites de concurrence, consultez [Gestion de la concurrence et des charges de travail][Concurrency and workload management].</span><span class="sxs-lookup"><span data-stu-id="a2982-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="a2982-126">Les requêtes peuvent également attendre d’autres raisons, par exemple des verrouillages d’objets.</span><span class="sxs-lookup"><span data-stu-id="a2982-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="a2982-127">Si votre requête est en attente d’une ressource, consultez [Examen des requêtes en attente de ressources][Investigating queries waiting for resources] plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="a2982-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="a2982-128">recherche de hello toosimplify d’une requête dans la table de sys.dm_pdw_exec_requests hello, utilisez [étiquette] [ LABEL] tooassign une requête tooyour commentaire qui peut être recherchée dans la vue de sys.dm_pdw_exec_requests hello.</span><span class="sxs-lookup"><span data-stu-id="a2982-128">toosimplify hello lookup of a query in hello sys.dm_pdw_exec_requests table, use [LABEL][LABEL] tooassign a comment tooyour query that can be looked up in hello sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a><span data-ttu-id="a2982-129">ÉTAPE 2 : Examiner le plan de requête hello</span><span class="sxs-lookup"><span data-stu-id="a2982-129">STEP 2: Investigate hello query plan</span></span>
<span data-ttu-id="a2982-130">Utilisez hello ID de demande tooretrieve hello plan de la requête distribuée SQL (DSQL) à partir de [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="a2982-130">Use hello Request ID tooretrieve hello query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="a2982-131">Lorsqu’un plan DSQL est plu longue que prévu, cause de hello peut être un plan complex avec nombreuses étapes DSQL ou qu’une seule étape prend beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="a2982-131">When a DSQL plan is taking longer than expected, hello cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="a2982-132">Si le plan de hello est de nombreuses étapes avec plusieurs opérations de déplacement, envisagez d’optimiser votre le déplacement des données de table distributions tooreduce.</span><span class="sxs-lookup"><span data-stu-id="a2982-132">If hello plan is many steps with several move operations, consider optimizing your table distributions tooreduce data movement.</span></span> <span data-ttu-id="a2982-133">Hello [Table distribution] [ Table distribution] article explique pourquoi les données doivent être déplacée toosolve une requête et explique certains le déplacement des données de distribution stratégies toominimize.</span><span class="sxs-lookup"><span data-stu-id="a2982-133">hello [Table distribution][Table distribution] article explains why data must be moved toosolve a query and explains some distribution strategies toominimize data movement.</span></span>

<span data-ttu-id="a2982-134">tooinvestigate plus d’informations sur une seule étape, hello *type_opération* colonne Hello d’étape et prendre note de la requête longue à exécuter hello **Index d’étape**:</span><span class="sxs-lookup"><span data-stu-id="a2982-134">tooinvestigate further details about a single step, hello *operation_type* column of hello long-running query step and note hello **Step Index**:</span></span>

* <span data-ttu-id="a2982-135">Passez à l’étape 3a pour les **opérations SQL**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="a2982-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="a2982-136">Passez à l’étape 3b pour **les opérations de déplacement des données**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="a2982-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a><span data-ttu-id="a2982-137">ÉTAPE 3 a : examiner SQL sur les bases de données hello distribué</span><span class="sxs-lookup"><span data-stu-id="a2982-137">STEP 3a: Investigate SQL on hello distributed databases</span></span>
<span data-ttu-id="a2982-138">Utilisez hello ID de la demande et hello Index d’étape tooretrieve détails [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], qui contient des informations de l’exécution de l’étape de requête hello sur tous les hello distribuées de bases de données.</span><span class="sxs-lookup"><span data-stu-id="a2982-138">Use hello Request ID and hello Step Index tooretrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of hello query step on all of hello distributed databases.</span></span>

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="a2982-139">Lors de l’étape de requête hello est en cours d’exécution, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] peut être utilisé tooretrieve hello SQL Server le plan estimé de hello du cache de plan SQL Server de l’étape hello en cours d’exécution sur un particulier distribution.</span><span class="sxs-lookup"><span data-stu-id="a2982-139">When hello query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello step running on a particular distribution.</span></span>

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a><span data-ttu-id="a2982-140">ÉTAPE 3 b : examiner le déplacement des données sur les bases de données hello distribué</span><span class="sxs-lookup"><span data-stu-id="a2982-140">STEP 3b: Investigate data movement on hello distributed databases</span></span>
<span data-ttu-id="a2982-141">Utilisez hello ID de la demande et hello étape tooretrieve informations d’Index une étape de déplacement des données en cours d’exécution sur chaque point de distribution à partir de [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="a2982-141">Use hello Request ID and hello Step Index tooretrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="a2982-142">Vérifiez hello *total_elapsed_time* toosee colonne si une distribution particulière prend beaucoup plus de temps que d’autres pour le déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="a2982-142">Check hello *total_elapsed_time* column toosee if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="a2982-143">Pour la distribution de longs hello, vérifiez hello *rows_processed* toosee colonne si le nombre de hello de lignes en cours de déplacement à partir de cette distribution est beaucoup plus important que d’autres.</span><span class="sxs-lookup"><span data-stu-id="a2982-143">For hello long-running distribution, check hello *rows_processed* column toosee if hello number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="a2982-144">Dans ce cas, cela peut indiquer un décalage des données sous-jacentes.</span><span class="sxs-lookup"><span data-stu-id="a2982-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="a2982-145">Si la requête de hello est en cours d’exécution, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] peut être utilisé tooretrieve hello SQL Server le plan estimé de hello cache du plan de SQL Server pour hello étape SQL en cours d’exécution au sein d’un particulier distribution.</span><span class="sxs-lookup"><span data-stu-id="a2982-145">If hello query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="a2982-146">Surveillance des requêtes en attente</span><span class="sxs-lookup"><span data-stu-id="a2982-146">Monitor waiting queries</span></span>
<span data-ttu-id="a2982-147">Si vous découvrez que votre requête ne progresse pas, car elle est en attente d’une ressource, voici une requête qui affiche toutes les ressources hello qu'attend une requête.</span><span class="sxs-lookup"><span data-stu-id="a2982-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all hello resources a query is waiting for.</span></span>

```sql
-- Find queries 
-- Replace request_id with value from Step 1.

SELECT waits.session_id,
      waits.request_id,  
      requests.command,
      requests.status,
      requests.start_time,  
      waits.type,
      waits.state,
      waits.object_type,
      waits.object_name
FROM   sys.dm_pdw_waits waits
   JOIN  sys.dm_pdw_exec_requests requests
   ON waits.request_id=requests.request_id
WHERE waits.request_id = 'QID####'
ORDER BY waits.object_name, waits.object_type, waits.state;
```

<span data-ttu-id="a2982-148">Si la requête de hello est activement en attente de ressources à partir d’une autre requête, puis hello état ne sera pas **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="a2982-148">If hello query is actively waiting on resources from another query, then hello state will be **AcquireResources**.</span></span>  <span data-ttu-id="a2982-149">Si la requête de hello possède toutes les ressources hello requis, puis hello état ne sera pas **Granted**.</span><span class="sxs-lookup"><span data-stu-id="a2982-149">If hello query has all hello required resources, then hello state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="a2982-150">Surveiller tempdb</span><span class="sxs-lookup"><span data-stu-id="a2982-150">Monitor tempdb</span></span>
<span data-ttu-id="a2982-151">Utilisation de tempdb élevée peut être hello cause de ralentissement des performances et les problèmes de mémoire insuffisante.</span><span class="sxs-lookup"><span data-stu-id="a2982-151">High tempdb utilization can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="a2982-152">Vérifiez tout d’abord si vous avez rowgroups de décalage ou de mauvaise qualité de données et prenez les mesures appropriées de hello.</span><span class="sxs-lookup"><span data-stu-id="a2982-152">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="a2982-153">Envisagez la mise à l’échelle de votre entrepôt de données si tempdb atteint ses limites lors de l’exécution de requêtes.</span><span class="sxs-lookup"><span data-stu-id="a2982-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="a2982-154">Hello suivante décrit comment l’utilisation de tempdb tooidentify par requête sur chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="a2982-154">hello following describes how tooidentify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="a2982-155">Créer hello id de nœud approprié vue tooassociate hello pour sys.dm_pdw_sql_requests suivant.</span><span class="sxs-lookup"><span data-stu-id="a2982-155">Create hello following view tooassociate hello appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="a2982-156">Cela active vous tooleverage autres DMV directs et joignez ces tables à sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="a2982-156">This will enable you tooleverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with hello correct node id
CREATE VIEW sql_requests AS
(SELECT
       sr.request_id,
       sr.step_index,
       (CASE 
              WHEN (sr.distribution_id = -1 ) THEN 
              (SELECT pdw_node_id FROM sys.dm_pdw_nodes WHERE type = 'CONTROL') 
              ELSE d.pdw_node_id END) AS pdw_node_id,
       sr.distribution_id,
       sr.status,
       sr.error_id,
       sr.start_time,
       sr.end_time,
       sr.total_elapsed_time,
       sr.row_count,
       sr.spid,
       sr.command
FROM sys.pdw_distributions AS d
RIGHT JOIN sys.dm_pdw_sql_requests AS sr ON d.distribution_id = sr.distribution_id)
```
<span data-ttu-id="a2982-157">Exécutez hello suivant requête toomonitor tempdb :</span><span class="sxs-lookup"><span data-stu-id="a2982-157">Run hello following query toomonitor tempdb:</span></span>

```sql
-- Monitor tempdb
SELECT
    sr.request_id,
    ssu.session_id,
    ssu.pdw_node_id,
    sr.command,
    sr.total_elapsed_time,
    es.login_name AS 'LoginName',
    DB_NAME(ssu.database_id) AS 'DatabaseName',
    (es.memory_usage * 8) AS 'MemoryUsage (in KB)',
    (ssu.user_objects_alloc_page_count * 8) AS 'Space Allocated For User Objects (in KB)',
    (ssu.user_objects_dealloc_page_count * 8) AS 'Space Deallocated For User Objects (in KB)',
    (ssu.internal_objects_alloc_page_count * 8) AS 'Space Allocated For Internal Objects (in KB)',
    (ssu.internal_objects_dealloc_page_count * 8) AS 'Space Deallocated For Internal Objects (in KB)',
    CASE es.is_user_process
    WHEN 1 THEN 'User Session'
    WHEN 0 THEN 'System Session'
    END AS 'SessionType',
    es.row_count AS 'RowCount'
FROM sys.dm_pdw_nodes_db_session_space_usage AS ssu
    INNER JOIN sys.dm_pdw_nodes_exec_sessions AS es ON ssu.session_id = es.session_id AND ssu.pdw_node_id = es.pdw_node_id
    INNER JOIN sys.dm_pdw_nodes_exec_connections AS er ON ssu.session_id = er.session_id AND ssu.pdw_node_id = er.pdw_node_id
    INNER JOIN sql_requests AS sr ON ssu.session_id = sr.spid AND ssu.pdw_node_id = sr.pdw_node_id
WHERE DB_NAME(ssu.database_id) = 'tempdb'
    AND es.session_id <> @@SPID
    AND es.login_name <> 'sa' 
ORDER BY sr.request_id;
```
## <a name="monitor-memory"></a><span data-ttu-id="a2982-158">Surveiller la mémoire</span><span class="sxs-lookup"><span data-stu-id="a2982-158">Monitor memory</span></span>

<span data-ttu-id="a2982-159">Mémoire peut être la cause première hello de ralentissement des performances et les problèmes de mémoire insuffisante.</span><span class="sxs-lookup"><span data-stu-id="a2982-159">Memory can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="a2982-160">Vérifiez tout d’abord si vous avez rowgroups de décalage ou de mauvaise qualité de données et prenez les mesures appropriées de hello.</span><span class="sxs-lookup"><span data-stu-id="a2982-160">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="a2982-161">Envisagez la mise à l’échelle de votre entrepôt de données si l’utilisation de la mémoire SQL Server atteint ses limites lors de l’exécution de requêtes.</span><span class="sxs-lookup"><span data-stu-id="a2982-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="a2982-162">Hello suivant la requête retourne à SQL Server d’utilisation et de la mémoire sollicitation de la mémoire par nœud :</span><span class="sxs-lookup"><span data-stu-id="a2982-162">hello following query returns SQL Server memory usage and memory pressure per node:</span></span> 
```sql
-- Memory consumption
SELECT
  pc1.cntr_value as Curr_Mem_KB, 
  pc1.cntr_value/1024.0 as Curr_Mem_MB,
  (pc1.cntr_value/1048576.0) as Curr_Mem_GB,
  pc2.cntr_value as Max_Mem_KB,
  pc2.cntr_value/1024.0 as Max_Mem_MB,
  (pc2.cntr_value/1048576.0) as Max_Mem_GB,
  pc1.cntr_value * 100.0/pc2.cntr_value AS Memory_Utilization_Percentage,
  pc1.pdw_node_id
FROM
-- pc1: current memory
sys.dm_pdw_nodes_os_performance_counters AS pc1
-- pc2: total memory allowed for this SQL instance
JOIN sys.dm_pdw_nodes_os_performance_counters AS pc2 
ON pc1.object_name = pc2.object_name AND pc1.pdw_node_id = pc2.pdw_node_id
WHERE
pc1.counter_name = 'Total Server Memory (KB)'
AND pc2.counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="a2982-163">Surveiller la taille du journal des transactions</span><span class="sxs-lookup"><span data-stu-id="a2982-163">Monitor transaction log size</span></span>
<span data-ttu-id="a2982-164">Hello requête suivante retourne taille de journal des transactions hello sur chaque point de distribution.</span><span class="sxs-lookup"><span data-stu-id="a2982-164">hello following query returns hello transaction log size on each distribution.</span></span> <span data-ttu-id="a2982-165">Vérifiez si vous avez rowgroups de décalage ou de mauvaise qualité de données et prenez les mesures appropriées de hello.</span><span class="sxs-lookup"><span data-stu-id="a2982-165">Please check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="a2982-166">Si un des fichiers de journal hello atteint 160 Go, vous devez envisager la mise à l’échelle votre instance ou en limitant la taille de votre transaction.</span><span class="sxs-lookup"><span data-stu-id="a2982-166">If one of hello log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
```sql
-- Transaction log size
SELECT
  instance_name as distribution_db,
  cntr_value*1.0/1048576 as log_file_size_used_GB,
  pdw_node_id 
FROM sys.dm_pdw_nodes_os_performance_counters 
WHERE 
instance_name like 'Distribution_%' 
AND counter_name = 'Log File(s) Used Size (KB)'
AND counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="a2982-167">Surveiller la restauration du journal des transactions</span><span class="sxs-lookup"><span data-stu-id="a2982-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="a2982-168">Si vos requêtes échouent ou prenant un tooproceed beaucoup de temps, vous pouvez contrôler et surveiller si vous disposez de toutes les transactions d’annulation.</span><span class="sxs-lookup"><span data-stu-id="a2982-168">If your queries are failing or taking a long time tooproceed, you can check and monitor if you have any transactions rolling back.</span></span>
```sql
-- Monitor rollback
SELECT 
    SUM(CASE WHEN t.database_transaction_next_undo_lsn IS NOT NULL THEN 1 ELSE 0 END),
    t.pdw_node_id,
    nod.[type]
FROM sys.dm_pdw_nodes_tran_database_transactions t
JOIN sys.dm_pdw_nodes nod ON t.pdw_node_id = nod.pdw_node_id
GROUP BY t.pdw_node_id, nod.[type]
```

## <a name="next-steps"></a><span data-ttu-id="a2982-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a2982-169">Next steps</span></span>
<span data-ttu-id="a2982-170">Pour plus d’informations sur les vues de gestion dynamique, consultez [Vues système][System views].</span><span class="sxs-lookup"><span data-stu-id="a2982-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="a2982-171">Pour plus d’informations sur les bonnes pratiques, consultez [Bonnes pratiques pour SQL Data Warehouse][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="a2982-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

<!--Image references-->

<!--Article references-->
[Manage overview]: ./sql-data-warehouse-overview-manage.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[System views]: ./sql-data-warehouse-reference-tsql-system-views.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Investigating queries waiting for resources]: ./sql-data-warehouse-manage-monitor.md#waiting

<!--MSDN references-->
[sys.dm_pdw_dms_workers]: http://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_exec_requests]: http://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_exec_sessions]: http://msdn.microsoft.com/library/mt203883.aspx
[sys.dm_pdw_request_steps]: http://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: http://msdn.microsoft.com/library/mt203889.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: http://msdn.microsoft.com/library/mt204017.aspx
[DBCC PDW_SHOWSPACEUSED]: http://msdn.microsoft.com/library/mt204028.aspx
[LABEL]: https://msdn.microsoft.com/library/ms190322.aspx
