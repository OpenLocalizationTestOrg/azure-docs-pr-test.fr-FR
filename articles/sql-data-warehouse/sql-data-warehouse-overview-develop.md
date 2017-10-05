---
title: "Ressources pour le développement d’un entrepôt de données dans Azure | Microsoft Docs"
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
ms.openlocfilehash: b85a4f09e561e429aa5bf46ec680014487fb40c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="ad8dc-103">Choix de conception et techniques de codage pour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ad8dc-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="ad8dc-104">Consultez les articles sur le développement afin de mieux comprendre les choix de conception, les recommandations et les techniques de codage fondamentaux pour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ad8dc-104">Take a look through these development articles to better understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="ad8dc-105">Choix de conception clés</span><span class="sxs-lookup"><span data-stu-id="ad8dc-105">Key design decisions</span></span>
<span data-ttu-id="ad8dc-106">Les articles suivants offrent un aperçu de quelques-uns des concepts principaux et des décisions de conception que vous devrez maîtriser pour le développement de votre entrepôt de données distribué à l’aide de SQL Data Warehouse :</span><span class="sxs-lookup"><span data-stu-id="ad8dc-106">The following articles highlight some of the key concepts and design decisions you will need to understand for the development of your distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="ad8dc-107">[Connexions][connections]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-107">[connections][connections]</span></span>
* <span data-ttu-id="ad8dc-108">[Accès concurrentiel][concurrency]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="ad8dc-109">[Transactions][transactions]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-109">[transactions][transactions]</span></span>
* <span data-ttu-id="ad8dc-110">[Schémas définis par l’utilisateur][user-defined schemas]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="ad8dc-111">[Distribution de tables][table distribution]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="ad8dc-112">[Index de table][table indexes]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="ad8dc-113">[Partitions de table][table partitions]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="ad8dc-114">[CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="ad8dc-115">[Statistiques][statistics]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="ad8dc-116">Recommandations pour le développement et techniques de codage</span><span class="sxs-lookup"><span data-stu-id="ad8dc-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="ad8dc-117">Ces articles mettent l’accent sur des techniques de codage spécifiques, des conseils et des recommandations pour le développement de votre SQL Data Warehouse :</span><span class="sxs-lookup"><span data-stu-id="ad8dc-117">These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="ad8dc-118">[Procédures stockées][stored procedures]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="ad8dc-119">[Étiquettes][labels]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-119">[labels][labels]</span></span>
* <span data-ttu-id="ad8dc-120">[Vues][views]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-120">[views][views]</span></span>
* <span data-ttu-id="ad8dc-121">[Tables temporaires][temporary tables]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="ad8dc-122">[SQL dynamique][dynamic SQL]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="ad8dc-123">[Bouclage][looping]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-123">[looping][looping]</span></span>
* <span data-ttu-id="ad8dc-124">[Options de regroupement][group by options]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-124">[group by options][group by options]</span></span>
* <span data-ttu-id="ad8dc-125">[Attribution de variables][variable assignment]</span><span class="sxs-lookup"><span data-stu-id="ad8dc-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad8dc-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ad8dc-126">Next steps</span></span>
<span data-ttu-id="ad8dc-127">Une fois que vous avez consulté les articles sur le développement, accédez à la page des [informations de référence sur Transact-SQL][Transact-SQL reference] pour en savoir plus sur la syntaxe prise en charge pour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ad8dc-127">Once you have been through the development articles take a look through the [Transact-SQL reference][Transact-SQL reference] page for more details on the supported syntax for SQL Data Warehouse.</span></span>

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
