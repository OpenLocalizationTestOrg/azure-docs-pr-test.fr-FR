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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a>Gestion de la puissance de calcul dans Azure SQL Data Warehouse (T-SQL)
> [!div class="op_single_selector"]
> * [Vue d'ensemble](sql-data-warehouse-manage-compute-overview.md)
> * [Portail](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a>Afficher les paramètres d’unités DWU actuels
tooview hello DWU paramètres actuels de vos bases de données :

1. Ouvrez l’Explorateur d’objets SQL Server dans Visual Studio.
2. Connecter la base de données master toohello associé avec le serveur de base de données SQL logique hello.
3. Sélectionnez dans la vue de gestion dynamique sys.database_service_objectives hello. Voici un exemple : 

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

## <a name="scale-compute"></a>Mise à l’échelle des ressources de calcul
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

hello toochange Dwu :

1. Connecter la base de données master toohello associé à votre serveur logique de la base de données SQL.
2. Hello d’utilisation [ALTER DATABASE] [ ALTER DATABASE] l’instruction TSQL. Hello exemple suivant définit hello service niveau objectif tooDW1000 pour la base de données de hello MySQLDW. 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a>Vérification de l’état de la base de données et de la progression de l’opération

1. Connecter la base de données master toohello associé à votre serveur logique de la base de données SQL.
2. Envoyer l’état de base de données de requête toocheck

```sql
SELECT *
FROM
sys.databases
```

3. Soumettre l’état de toocheck de requête d’opération

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

Cette DMV retourne des informations sur les diverses opérations de gestion sur votre entrepôt de données SQL telles que l’état de fonctionnement et hello hello d’opération de hello, qui sera IN_PROGRESS ou s’est terminée.



<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Étapes suivantes
Pour d’autres tâches de gestion, consultez la rubrique [Vue d’ensemble du système de gestion][Management overview].

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
