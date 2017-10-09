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
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a>Analyse d’une base de données SQL Azure à l’aide de vues de gestion dynamique
Base de données SQL Microsoft Azure permet un sous-ensemble de gestion dynamique affiche toodiagnose des problèmes de performances, ce qui peuvent être dû à des requêtes longues ou bloquées, des goulots d’étranglement, plans de requête médiocres et ainsi de suite. Cette rubrique fournit des informations sur la façon de toodetect les problèmes de performances courants à l’aide de vues de gestion dynamique.

La base de données SQL prend partiellement en charge trois catégories de vues de gestion dynamique :

* vues de gestion dynamique liées à la base de données ;
* vues de gestion dynamique liées à l’exécution ;
* vues de gestion dynamique liées à la transaction.

Pour plus d’informations sur les vues de gestion dynamique, voir [Fonctions et vues de gestion dynamique (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) dans la documentation en ligne de SQL Server.

## <a name="permissions"></a>Autorisations
Dans la base de données SQL, l’interrogation d’une vue de gestion dynamique nécessite des autorisations **AFFICHER L'ÉTAT DE LA BASE DE DONNÉES** . Hello **VIEW DATABASE STATE** autorisation retourne des informations sur tous les objets de base de données actuelle hello.
toogrant hello **VIEW DATABASE STATE** autorisation tooa utilisateur spécifique, exécutez hello suivant la requête :

```GRANT VIEW DATABASE STATE toodatabase_user; ```

Dans une instance de SQL Server local, des vues de gestion dynamiques renvoient des informations sur l’état du serveur. Dans Base de données SQL, elles renvoient des informations relatives à votre base de données logique actuelle.

## <a name="calculating-database-size"></a>Calcul de la taille de la base de données
Hello requête suivante renvoie taille hello de votre base de données (en mégaoctets) :

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

Hello requête suivante renvoie hello taille des objets individuels (en mégaoctets) dans votre base de données :

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a>Analyse des connexions
Vous pouvez utiliser hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) tooretrieve des informations sur le serveur de base de données SQL Azure spécifique hello connexions établies tooa et les détails de hello de chaque connexion. En outre, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) vue est utile lors de la récupération des informations sur toutes les connexions utilisateur actives et les tâches internes.
Hello requête suivante récupère des informations sur la connexion en cours de hello :

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
> Lors de l’exécution hello **sys.dm_exec_requests** et **des vues sys.dm_exec_sessions**, si vous avez **VIEW DATABASE STATE** autorisation sur la base de données hello, reportez-vous à l’exécution de toutes les sessions de base de données hello ; Sinon, vous verrez uniquement hello session active.
> 
> 

## <a name="monitoring-query-performance"></a>Analyse des performances des requêtes
Des requêtes lentes ou longues peuvent consommer des ressources système significatives. Cette section montre comment toouse vues de gestion dynamiques toodetect quelques problèmes de performances de requête courants. Une référence plus anciens, mais toujours utile pour le dépannage, est hello [résolution des problèmes de performances dans SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article sur Microsoft TechNet.

### <a name="finding-top-n-queries"></a>Recherche des N premières requêtes
Hello exemple suivant retourne des informations sur hello cinq premières requêtes classées d’après le temps processeur moyen. Cet exemple regroupe les requêtes hello en tootheir en fonction de hachage de requête, afin que les requêtes logiquement équivalentes soient groupées par leur consommation de ressources cumulative.

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

### <a name="monitoring-blocked-queries"></a>Surveillance des requêtes bloquées
Les requêtes lentes ou longues peuvent contribuer tooexcessive la consommation des ressources et être la conséquence de hello de requêtes bloquées. cause Hello hello blocage peut être une mauvaise conception de l’application, mauvais plans de requête, hello manque d’index utiles et ainsi de suite. Vous pouvez utiliser hello sys.dm_tran_locks afficher tooget des informations sur l’activité hello de verrouillage actuelle dans votre base de données SQL Azure. Pour un exemple de code, voir [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) dans la documentation en ligne de SQL Server.

### <a name="monitoring-query-plans"></a>Analyse des plans de requête
Un plan de requête inefficace peut également augmenter la consommation du processeur. exemple Hello utilise hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) afficher toodetermine requête qui utilise les UC plus cumulative hello.

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

## <a name="see-also"></a>Voir aussi
[Introduction tooSQL de base de données](sql-database-technical-overview.md)

