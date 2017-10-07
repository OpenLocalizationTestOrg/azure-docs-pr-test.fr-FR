---
title: "aaaResources pour le développement d’un entrepôt de données dans Azure | Documents Microsoft"
description: "Concepts de développement, choix de conception, recommandations et des techniques de codage pour SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: 
ms.assetid: 996e3afc-c21c-4e21-b9df-997f953f6dfd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: develop
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 67e3a6a3e2664919c3445ea5d5eba251054de020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a>Choix de conception et techniques de codage pour SQL Data Warehouse
Examinez ces articles développement toobetter comprendre principales décisions de conception, des recommandations et des techniques de codage pour SQL Data Warehouse.

## <a name="key-design-decisions"></a>Choix de conception clés
Hello articles suivants de la mettre en évidence certains des concepts clés de hello et les décisions de conception que vous devez toounderstand pour le développement hello de votre entrepôt de données distribuées à l’aide de l’entrepôt de données SQL :

* [Connexions][connections]
* [Accès concurrentiel][concurrency]
* [Transactions][transactions]
* [Schémas définis par l’utilisateur][user-defined schemas]
* [Distribution de tables][table distribution]
* [Index de table][table indexes]
* [Partitions de table][table partitions]
* [CTAS][CTAS]
* [Statistiques][statistics]

## <a name="development-recommendations-and-coding-techniques"></a>Recommandations pour le développement et techniques de codage
Ces articles mettent l’accent sur des techniques de codage spécifiques, des conseils et des recommandations pour le développement de votre SQL Data Warehouse :

* [Procédures stockées][stored procedures]
* [Étiquettes][labels]
* [Vues][views]
* [Tables temporaires][temporary tables]
* [SQL dynamique][dynamic SQL]
* [Bouclage][looping]
* [Options de regroupement][group by options]
* [Attribution de variables][variable assignment]

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous avez été articles de développement hello jetez un œil à hello [référence Transact-SQL] [ Transact-SQL reference] pour plus d’informations sur la syntaxe hello pris en charge pour SQL Data Warehouse.

<!--Image references-->

<!--Article references-->
[concurrency]: ./sql-data-warehouse-develop-concurrency.md
[connections]: ./sql-data-warehouse-connect-overview.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[dynamic SQL]: ./sql-data-warehouse-develop-dynamic-sql.md
[group by options]: ./sql-data-warehouse-develop-group-by-options.md
[labels]: ./sql-data-warehouse-develop-label.md
[looping]: ./sql-data-warehouse-develop-loops.md
[statistics]: ./sql-data-warehouse-tables-statistics.md
[stored procedures]: ./sql-data-warehouse-develop-stored-procedures.md
[table distribution]: ./sql-data-warehouse-tables-distribute.md
[table indexes]: ./sql-data-warehouse-tables-index.md
[table partitions]: ./sql-data-warehouse-tables-partition.md
[temporary tables]: ./sql-data-warehouse-tables-temporary.md
[transactions]: ./sql-data-warehouse-develop-transactions.md
[user-defined schemas]: ./sql-data-warehouse-develop-user-defined-schemas.md
[variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[views]: ./sql-data-warehouse-develop-views.md
[Transact-SQL reference]: ./sql-data-warehouse-overview-reference.md

<!--MSDN references-->
[renaming objects]: https://msdn.microsoft.com/library/mt631611.aspx

<!--Other Web references-->
