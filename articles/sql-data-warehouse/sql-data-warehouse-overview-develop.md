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
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="b91ee-103">Choix de conception et techniques de codage pour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b91ee-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="b91ee-104">Examinez ces articles développement toobetter comprendre principales décisions de conception, des recommandations et des techniques de codage pour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b91ee-104">Take a look through these development articles toobetter understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="b91ee-105">Choix de conception clés</span><span class="sxs-lookup"><span data-stu-id="b91ee-105">Key design decisions</span></span>
<span data-ttu-id="b91ee-106">Hello articles suivants de la mettre en évidence certains des concepts clés de hello et les décisions de conception que vous devez toounderstand pour le développement hello de votre entrepôt de données distribuées à l’aide de l’entrepôt de données SQL :</span><span class="sxs-lookup"><span data-stu-id="b91ee-106">hello following articles highlight some of hello key concepts and design decisions you will need toounderstand for hello development of your distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="b91ee-107">[Connexions][connections]</span><span class="sxs-lookup"><span data-stu-id="b91ee-107">[connections][connections]</span></span>
* <span data-ttu-id="b91ee-108">[Accès concurrentiel][concurrency]</span><span class="sxs-lookup"><span data-stu-id="b91ee-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="b91ee-109">[Transactions][transactions]</span><span class="sxs-lookup"><span data-stu-id="b91ee-109">[transactions][transactions]</span></span>
* <span data-ttu-id="b91ee-110">[Schémas définis par l’utilisateur][user-defined schemas]</span><span class="sxs-lookup"><span data-stu-id="b91ee-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="b91ee-111">[Distribution de tables][table distribution]</span><span class="sxs-lookup"><span data-stu-id="b91ee-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="b91ee-112">[Index de table][table indexes]</span><span class="sxs-lookup"><span data-stu-id="b91ee-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="b91ee-113">[Partitions de table][table partitions]</span><span class="sxs-lookup"><span data-stu-id="b91ee-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="b91ee-114">[CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="b91ee-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="b91ee-115">[Statistiques][statistics]</span><span class="sxs-lookup"><span data-stu-id="b91ee-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="b91ee-116">Recommandations pour le développement et techniques de codage</span><span class="sxs-lookup"><span data-stu-id="b91ee-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="b91ee-117">Ces articles mettent l’accent sur des techniques de codage spécifiques, des conseils et des recommandations pour le développement de votre SQL Data Warehouse :</span><span class="sxs-lookup"><span data-stu-id="b91ee-117">These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="b91ee-118">[Procédures stockées][stored procedures]</span><span class="sxs-lookup"><span data-stu-id="b91ee-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="b91ee-119">[Étiquettes][labels]</span><span class="sxs-lookup"><span data-stu-id="b91ee-119">[labels][labels]</span></span>
* <span data-ttu-id="b91ee-120">[Vues][views]</span><span class="sxs-lookup"><span data-stu-id="b91ee-120">[views][views]</span></span>
* <span data-ttu-id="b91ee-121">[Tables temporaires][temporary tables]</span><span class="sxs-lookup"><span data-stu-id="b91ee-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="b91ee-122">[SQL dynamique][dynamic SQL]</span><span class="sxs-lookup"><span data-stu-id="b91ee-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="b91ee-123">[Bouclage][looping]</span><span class="sxs-lookup"><span data-stu-id="b91ee-123">[looping][looping]</span></span>
* <span data-ttu-id="b91ee-124">[Options de regroupement][group by options]</span><span class="sxs-lookup"><span data-stu-id="b91ee-124">[group by options][group by options]</span></span>
* <span data-ttu-id="b91ee-125">[Attribution de variables][variable assignment]</span><span class="sxs-lookup"><span data-stu-id="b91ee-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="b91ee-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b91ee-126">Next steps</span></span>
<span data-ttu-id="b91ee-127">Une fois que vous avez été articles de développement hello jetez un œil à hello [référence Transact-SQL] [ Transact-SQL reference] pour plus d’informations sur la syntaxe hello pris en charge pour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b91ee-127">Once you have been through hello development articles take a look through hello [Transact-SQL reference][Transact-SQL reference] page for more details on hello supported syntax for SQL Data Warehouse.</span></span>

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
