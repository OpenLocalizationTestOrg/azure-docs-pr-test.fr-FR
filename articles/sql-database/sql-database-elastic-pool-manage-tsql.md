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
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a>Surveiller et gérer un pool élastique avec Transact-SQL
Cette rubrique vous montre comment toomanage évolutive [pools élastiques](sql-database-elastic-pool.md) avec Transact-SQL.  Vous pouvez également créer et gérer un hello Azure pool élastique [portail Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello API REST, ou [c#](sql-database-elastic-pool-manage-csharp.md). Vous pouvez également créer et déplacer des bases de données vers et depuis des pools élastiques à l’aide de [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).


Hello d’utilisation [Create Database (base de données de SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) et [Alter de Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commandes toocreate et déplacement des bases de données vers et depuis les pools élastiques. pool élastique de Hello doit exister avant de pouvoir utiliser ces commandes. Ces commandes affectent uniquement les bases de données. La création de nouveaux pools hello paramètre et des propriétés du pool (par exemple, Edtu min et max) ne peut pas être modifié avec les commandes T-SQL.

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Créer une base de données regroupée dans un pool élastique
Utilisez la commande de créer la base de données de hello avec l’option de SERVICE_OBJECTIVE de hello.   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

Toutes les bases de données dans un pool élastique héritent de niveau de service hello du pool élastique de hello (Basic, Standard, Premium). 

## <a name="move-a-database-between-elastic-pools"></a>Déplacer une base de données entre les pools élastiques
Utilisez la commande ALTER DATABASE hello avec hello modifier et configurer SERVICE\_option OBJECTIVE élastique\_POOL. Définir le hello nom toohello nom de pool de cible hello.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a>Déplacer une base de données dans un pool élastique
Utilisez la commande ALTER DATABASE hello avec hello modifier et configurer SERVICE\_option OBJECTIVE comme ELASTIC_POOL. Définir le hello nom toohello nom de pool de cible hello.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a>Déplacer une base de données hors d’un pool élastique
Utilisez la commande ALTER DATABASE hello et tooone SERVICE_OBJECTIVE hello hello des niveaux de performances (par exemple, S0 ou S1).

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a>Répertorier les bases de données dans un pool élastique
Hello d’utilisation [sys.database\_service \_objectifs vue](https://msdn.microsoft.com/library/mt712619) toolist tous hello des bases de données dans un pool élastique. Ouvrez une session dans toohello master vue de base de données tooquery hello.

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Obtenir les données d’utilisation des ressources d’un pool élastique
Hello d’utilisation [sys.elastic\_pool \_ressource \_affichage de statistiques](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello ressource les statistiques d’un pool élastique sur un serveur logique. Ouvrez une session dans toohello master vue de base de données tooquery hello.

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a>Obtenir les données d’utilisation des ressources d’une base de données mise en pool
Hello d’utilisation [sys.dm\_ db\_ ressource\_affichage de statistiques](https://msdn.microsoft.com/library/dn800981.aspx) ou [sys.resource \_affichage de statistiques](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine hello ressource les statistiques d’une base de données dans un pool élastique. Ce processus est l’utilisation des ressources tooquerying similaires pour une base de données.

## <a name="next-steps"></a>Étapes suivantes
Après avoir créé un pool élastique, vous pouvez gérer des bases de données élastiques dans le pool de hello en créant des travaux élastique. Travaux élastique facilite les scripts T-SQL en cours d’exécution par rapport à n’importe quel nombre de bases de données dans le pool de hello. Pour en savoir plus, consultez [Vue d'ensemble des tâches de base de données élastiques](sql-database-elastic-jobs-overview.md). 

Consultez [montée en puissance parallèle avec la base de données SQL Azure](sql-database-elastic-scale-introduction.md): utiliser tooscale d’outils de base de données élastique out, de déplacer des données, la requête ou la création des transactions.

