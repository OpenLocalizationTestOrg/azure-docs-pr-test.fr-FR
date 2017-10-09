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
# <a name="monitor-your-workload-using-dmvs"></a>Surveiller votre charge de travail à l'aide de vues de gestion dynamique
Cet article décrit comment toomonitor de vues de gestion dynamique (DMV) toouse votre charge de travail et examiner l’exécution de requête dans l’entrepôt de données SQL Azure.

## <a name="permissions"></a>Autorisations
tooquery hello DMV dans cet article, vous devez avoir l’autorisation VIEW DATABASE STATE ou de contrôle. Octroi à l’état de base de données d’affichage est généralement des autorisations de hello préféré car il est beaucoup plus restrictive.

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a>Suivi des connexions
Toutes les connexions tooSQL l’entrepôt de données sont enregistrés trop[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].  Cette DMV contient hello 10 000 connexions de la dernière.  Hello session_id est la clé primaire de hello et assignés de façon séquentielle pour chaque ouverture de session.

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a>Surveillance de l’exécution des rêquetes
Toutes les requêtes exécutées sur l’entrepôt de données SQL sont enregistrés trop[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].  Cette DMV contient hello dernière 10 000 requêtes exécutées.  Hello request_id identifie chaque requête de manière unique et est hello de clé primaire pour cette vue de gestion dynamique.  Hello request_id est attribué de manière séquentielle pour chaque nouvelle requête et est préfixé avec QID, ce qui correspond à l’ID de requête.  En interrogeant cette DMV pour un ID de session (session_id) donné, vous obtenez toutes les requêtes pour une connexion donnée.

> [!NOTE]
> Les procédures stockées utilisent plusieurs ID de requête.  Les ID de requête sont affectés dans un ordre séquentiel. 
> 
> 

Vous trouverez ici les plans d’exécution étapes toofollow tooinvestigate et les heures pour une requête particulière.

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a>ÉTAPE 1 : Identifier la requête hello que vous souhaitez tooinvestigate
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

À partir de hello précédant les résultats de la requête, **hello de note ID de demande** de requête hello que vous aimeriez tooinvestigate.

Requêtes Bonjour **Suspended** état sont en file d’attente en raison des limites de tooconcurrency. Ces requêtes apparaissent également dans hello sys.dm_pdw_waits attentes de requête avec un type de UserConcurrencyResourceType. Pour plus d’informations sur les limites de concurrence, consultez [Gestion de la concurrence et des charges de travail][Concurrency and workload management]. Les requêtes peuvent également attendre d’autres raisons, par exemple des verrouillages d’objets.  Si votre requête est en attente d’une ressource, consultez [Examen des requêtes en attente de ressources][Investigating queries waiting for resources] plus loin dans cet article.

recherche de hello toosimplify d’une requête dans la table de sys.dm_pdw_exec_requests hello, utilisez [étiquette] [ LABEL] tooassign une requête tooyour commentaire qui peut être recherchée dans la vue de sys.dm_pdw_exec_requests hello.

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a>ÉTAPE 2 : Examiner le plan de requête hello
Utilisez hello ID de demande tooretrieve hello plan de la requête distribuée SQL (DSQL) à partir de [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

Lorsqu’un plan DSQL est plu longue que prévu, cause de hello peut être un plan complex avec nombreuses étapes DSQL ou qu’une seule étape prend beaucoup de temps.  Si le plan de hello est de nombreuses étapes avec plusieurs opérations de déplacement, envisagez d’optimiser votre le déplacement des données de table distributions tooreduce. Hello [Table distribution] [ Table distribution] article explique pourquoi les données doivent être déplacée toosolve une requête et explique certains le déplacement des données de distribution stratégies toominimize.

tooinvestigate plus d’informations sur une seule étape, hello *type_opération* colonne Hello d’étape et prendre note de la requête longue à exécuter hello **Index d’étape**:

* Passez à l’étape 3a pour les **opérations SQL**: OnOperation, RemoteOperation, ReturnOperation.
* Passez à l’étape 3b pour **les opérations de déplacement des données**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a>ÉTAPE 3 a : examiner SQL sur les bases de données hello distribué
Utilisez hello ID de la demande et hello Index d’étape tooretrieve détails [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], qui contient des informations de l’exécution de l’étape de requête hello sur tous les hello distribuées de bases de données.

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

Lors de l’étape de requête hello est en cours d’exécution, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] peut être utilisé tooretrieve hello SQL Server le plan estimé de hello du cache de plan SQL Server de l’étape hello en cours d’exécution sur un particulier distribution.

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a>ÉTAPE 3 b : examiner le déplacement des données sur les bases de données hello distribué
Utilisez hello ID de la demande et hello étape tooretrieve informations d’Index une étape de déplacement des données en cours d’exécution sur chaque point de distribution à partir de [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* Vérifiez hello *total_elapsed_time* toosee colonne si une distribution particulière prend beaucoup plus de temps que d’autres pour le déplacement des données.
* Pour la distribution de longs hello, vérifiez hello *rows_processed* toosee colonne si le nombre de hello de lignes en cours de déplacement à partir de cette distribution est beaucoup plus important que d’autres. Dans ce cas, cela peut indiquer un décalage des données sous-jacentes.

Si la requête de hello est en cours d’exécution, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] peut être utilisé tooretrieve hello SQL Server le plan estimé de hello cache du plan de SQL Server pour hello étape SQL en cours d’exécution au sein d’un particulier distribution.

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a>Surveillance des requêtes en attente
Si vous découvrez que votre requête ne progresse pas, car elle est en attente d’une ressource, voici une requête qui affiche toutes les ressources hello qu'attend une requête.

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

Si la requête de hello est activement en attente de ressources à partir d’une autre requête, puis hello état ne sera pas **AcquireResources**.  Si la requête de hello possède toutes les ressources hello requis, puis hello état ne sera pas **Granted**.

## <a name="monitor-tempdb"></a>Surveiller tempdb
Utilisation de tempdb élevée peut être hello cause de ralentissement des performances et les problèmes de mémoire insuffisante. Vérifiez tout d’abord si vous avez rowgroups de décalage ou de mauvaise qualité de données et prenez les mesures appropriées de hello. Envisagez la mise à l’échelle de votre entrepôt de données si tempdb atteint ses limites lors de l’exécution de requêtes. Hello suivante décrit comment l’utilisation de tempdb tooidentify par requête sur chaque nœud. 

Créer hello id de nœud approprié vue tooassociate hello pour sys.dm_pdw_sql_requests suivant. Cela active vous tooleverage autres DMV directs et joignez ces tables à sys.dm_pdw_sql_requests.

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
Exécutez hello suivant requête toomonitor tempdb :

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
## <a name="monitor-memory"></a>Surveiller la mémoire

Mémoire peut être la cause première hello de ralentissement des performances et les problèmes de mémoire insuffisante. Vérifiez tout d’abord si vous avez rowgroups de décalage ou de mauvaise qualité de données et prenez les mesures appropriées de hello. Envisagez la mise à l’échelle de votre entrepôt de données si l’utilisation de la mémoire SQL Server atteint ses limites lors de l’exécution de requêtes.

Hello suivant la requête retourne à SQL Server d’utilisation et de la mémoire sollicitation de la mémoire par nœud : 
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
## <a name="monitor-transaction-log-size"></a>Surveiller la taille du journal des transactions
Hello requête suivante retourne taille de journal des transactions hello sur chaque point de distribution. Vérifiez si vous avez rowgroups de décalage ou de mauvaise qualité de données et prenez les mesures appropriées de hello. Si un des fichiers de journal hello atteint 160 Go, vous devez envisager la mise à l’échelle votre instance ou en limitant la taille de votre transaction. 
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
## <a name="monitor-transaction-log-rollback"></a>Surveiller la restauration du journal des transactions
Si vos requêtes échouent ou prenant un tooproceed beaucoup de temps, vous pouvez contrôler et surveiller si vous disposez de toutes les transactions d’annulation.
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

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les vues de gestion dynamique, consultez [Vues système][System views].
Pour plus d’informations sur les bonnes pratiques, consultez [Bonnes pratiques pour SQL Data Warehouse][SQL Data Warehouse best practices].

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
