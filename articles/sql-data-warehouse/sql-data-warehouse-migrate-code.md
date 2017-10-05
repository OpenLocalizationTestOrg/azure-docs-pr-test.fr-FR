---
title: "Migration de votre code SQL vers SQL Data Warehouse | Microsoft Docs"
description: "Conseils relatifs à la migration de votre code SQL vers Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 19c252a3-0e41-4eec-9d3e-09a68c7e7add
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/23/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: c6e6b890f5e2d0e31b10bbb6803adad02bf60248
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-sql-code-to-sql-data-warehouse"></a><span data-ttu-id="99182-103">Migration de votre code SQL vers SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="99182-103">Migrate your SQL code to SQL Data Warehouse</span></span>
<span data-ttu-id="99182-104">Cet article vous explique les éventuelles modifications de code que vous aurez à réaliser lors de la migration de votre code depuis une autre base de données vers SQL DATA Warehouse.</span><span class="sxs-lookup"><span data-stu-id="99182-104">This article explains code changes you will probably need to make when migrating your code from another database to SQL Data Warehouse.</span></span> <span data-ttu-id="99182-105">Certaines fonctionnalités de SQL Data Warehouse peuvent améliorer considérablement les performances, dans la mesure où elles sont conçues pour fonctionner selon un modèle distribué.</span><span class="sxs-lookup"><span data-stu-id="99182-105">Some SQL Data Warehouse features can significantly improve performance as they are designed to work in a distributed fashion.</span></span> <span data-ttu-id="99182-106">Toutefois, pour maintenir des niveaux appropriés de performance et d’évolutivité, certaines fonctions ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="99182-106">However, to maintain performance and scale, some features are also not available.</span></span>

## <a name="common-t-sql-limitations"></a><span data-ttu-id="99182-107">Limites courantes de T-SQL</span><span class="sxs-lookup"><span data-stu-id="99182-107">Common T-SQL Limitations</span></span>
<span data-ttu-id="99182-108">La liste suivante répertorie les fonctionnalités les plus courantes que SQL Data Warehouse ne prend pas en charge.</span><span class="sxs-lookup"><span data-stu-id="99182-108">The following list summarizes the most common features that SQL Data Warehouse does not support.</span></span> <span data-ttu-id="99182-109">Les liens vous présentent des solutions de contournement pour les fonctionnalités non prises en charge :</span><span class="sxs-lookup"><span data-stu-id="99182-109">The links take you to workarounds for the unsupported features:</span></span>

* <span data-ttu-id="99182-110">[Jointures ANSI sur les opérations UPDATE][ANSI joins on updates]</span><span class="sxs-lookup"><span data-stu-id="99182-110">[ANSI joins on updates][ANSI joins on updates]</span></span>
* <span data-ttu-id="99182-111">[Jointures ANSI sur les opérations DELETE][ANSI joins on deletes]</span><span class="sxs-lookup"><span data-stu-id="99182-111">[ANSI joins on deletes][ANSI joins on deletes]</span></span>
* <span data-ttu-id="99182-112">[Instruction MERGE][merge statement]</span><span class="sxs-lookup"><span data-stu-id="99182-112">[merge statement][merge statement]</span></span>
* <span data-ttu-id="99182-113">Jonctions entre plusieurs bases de données</span><span class="sxs-lookup"><span data-stu-id="99182-113">cross-database joins</span></span>
* <span data-ttu-id="99182-114">[Curseurs][cursors]</span><span class="sxs-lookup"><span data-stu-id="99182-114">[cursors][cursors]</span></span>
* <span data-ttu-id="99182-115"><seg>
  [INSERT..EXEC][INSERT..EXEC]</seg></span><span class="sxs-lookup"><span data-stu-id="99182-115">[INSERT..EXEC][INSERT..EXEC]</span></span>
* <span data-ttu-id="99182-116">Clause OUTPUT</span><span class="sxs-lookup"><span data-stu-id="99182-116">output clause</span></span>
* <span data-ttu-id="99182-117">Fonctions en ligne définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="99182-117">inline user-defined functions</span></span>
* <span data-ttu-id="99182-118">Fonctions à instructions multiples</span><span class="sxs-lookup"><span data-stu-id="99182-118">multi-statement functions</span></span>
* [<span data-ttu-id="99182-119">Expressions de table commune</span><span class="sxs-lookup"><span data-stu-id="99182-119">common table expressions</span></span>](#Common-table-expressions)
* <span data-ttu-id="99182-120">[Expressions récursives de table commune (CTE)](#Expressions-récursives-de-table-commune-(CTE)</span><span class="sxs-lookup"><span data-stu-id="99182-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span></span>
* <span data-ttu-id="99182-121">Fonctions et procédures CLR</span><span class="sxs-lookup"><span data-stu-id="99182-121">CLR functions and procedures</span></span>
* <span data-ttu-id="99182-122">Fonction $partition</span><span class="sxs-lookup"><span data-stu-id="99182-122">$partition function</span></span>
* <span data-ttu-id="99182-123">Variables de table</span><span class="sxs-lookup"><span data-stu-id="99182-123">table variables</span></span>
* <span data-ttu-id="99182-124">Paramètres de valeurs de table</span><span class="sxs-lookup"><span data-stu-id="99182-124">table value parameters</span></span>
* <span data-ttu-id="99182-125">Transactions distribuées</span><span class="sxs-lookup"><span data-stu-id="99182-125">distributed transactions</span></span>
* <span data-ttu-id="99182-126">Tâche de validation/restauration</span><span class="sxs-lookup"><span data-stu-id="99182-126">commit / rollback work</span></span>
* <span data-ttu-id="99182-127">Transaction d’enregistrement</span><span class="sxs-lookup"><span data-stu-id="99182-127">save transaction</span></span>
* <span data-ttu-id="99182-128">Contextes d’exécution (EXECUTE AS)</span><span class="sxs-lookup"><span data-stu-id="99182-128">execution contexts (EXECUTE AS)</span></span>
* <span data-ttu-id="99182-129">[Regroupement par clause à l’aide des options rollup/cube/grouping sets][group by clause with rollup / cube / grouping sets options]</span><span class="sxs-lookup"><span data-stu-id="99182-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span></span>
* <span data-ttu-id="99182-130">[Imbrication des niveaux au-delà de 8][nesting levels beyond 8]</span><span class="sxs-lookup"><span data-stu-id="99182-130">[nesting levels beyond 8][nesting levels beyond 8]</span></span>
* <span data-ttu-id="99182-131">[Mise à jour par le biais de vues][updating through views]</span><span class="sxs-lookup"><span data-stu-id="99182-131">[updating through views][updating through views]</span></span>
* <span data-ttu-id="99182-132">[Utilisation de Select pour l’attribution des variables][use of select for variable assignment]</span><span class="sxs-lookup"><span data-stu-id="99182-132">[use of select for variable assignment][use of select for variable assignment]</span></span>
* <span data-ttu-id="99182-133">[Pas de type de données MAX pour les chaînes SQL dynamiques][no MAX data type for dynamic SQL strings]</span><span class="sxs-lookup"><span data-stu-id="99182-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span></span>

<span data-ttu-id="99182-134">Fort heureusement, la plupart de ces restrictions peuvent être contournées.</span><span class="sxs-lookup"><span data-stu-id="99182-134">Fortunately most of these limitations can be worked around.</span></span> <span data-ttu-id="99182-135">Des explications sont fournies dans les articles de développement référencés ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="99182-135">Explanations are provided in the relevant development articles referenced above.</span></span>

## <a name="supported-cte-features"></a><span data-ttu-id="99182-136">Fonctionnalités CTE prises en charge</span><span class="sxs-lookup"><span data-stu-id="99182-136">Supported CTE features</span></span>
<span data-ttu-id="99182-137">Les expressions de table communes (CTE) sont partiellement prises en charge dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="99182-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="99182-138">Les fonctionnalités CTE actuellement prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="99182-138">The following CTE features are currently supported:</span></span>

* <span data-ttu-id="99182-139">Une CTE peut être spécifiée dans une instruction SELECT.</span><span class="sxs-lookup"><span data-stu-id="99182-139">A CTE can be specified in a SELECT statement.</span></span>
* <span data-ttu-id="99182-140">Une CTE peut être spécifiée dans une instruction CREATE VIEW.</span><span class="sxs-lookup"><span data-stu-id="99182-140">A CTE can be specified in a CREATE VIEW statement.</span></span>
* <span data-ttu-id="99182-141">Une CTE peut être spécifiée dans une instruction CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="99182-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span></span>
* <span data-ttu-id="99182-142">Une CTE peut être spécifiée dans une instruction CREATE REMOTE TABLE AS SELECT (CRTAS).</span><span class="sxs-lookup"><span data-stu-id="99182-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span></span>
* <span data-ttu-id="99182-143">Une CTE peut être spécifiée dans une instruction CREATE EXTERNAL TABLE AS SELECT (CETAS).</span><span class="sxs-lookup"><span data-stu-id="99182-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span></span>
* <span data-ttu-id="99182-144">Une table distante peut être référencée à partir d’une expression de table commune.</span><span class="sxs-lookup"><span data-stu-id="99182-144">A remote table can be referenced from a CTE.</span></span>
* <span data-ttu-id="99182-145">Une table externe peut être référencée à partir d’une expression de table commune.</span><span class="sxs-lookup"><span data-stu-id="99182-145">An external table can be referenced from a CTE.</span></span>
* <span data-ttu-id="99182-146">Plusieurs définitions de requête CTE peuvent être définies dans une expression de table commune.</span><span class="sxs-lookup"><span data-stu-id="99182-146">Multiple CTE query definitions can be defined in a CTE.</span></span>

## <a name="cte-limitations"></a><span data-ttu-id="99182-147">Limitations d’une CTE</span><span class="sxs-lookup"><span data-stu-id="99182-147">CTE Limitations</span></span>
<span data-ttu-id="99182-148">Les expressions de table communes présentent certaines restrictions dans SQL Data Warehouse, notamment :</span><span class="sxs-lookup"><span data-stu-id="99182-148">Common table expressions have some limitations in SQL Data Warehouse including:</span></span>

* <span data-ttu-id="99182-149">Une CTE doit être suivie d’une instruction SELECT unique.</span><span class="sxs-lookup"><span data-stu-id="99182-149">A CTE must be followed by a single SELECT statement.</span></span> <span data-ttu-id="99182-150">Les instructions INSERT, UPDATE, DELETE et MERGE ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="99182-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span></span>
* <span data-ttu-id="99182-151">Une expression de table commune qui inclut des références à elle-même (expression de table commune récursive) n’est pas prise en charge (voir la section ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="99182-151">A common table expression that includes references to itself (a recursive common table expression) is not supported (see below section).</span></span>
* <span data-ttu-id="99182-152">La spécification de plusieurs clauses WITH dans une CTE n’est pas autorisée.</span><span class="sxs-lookup"><span data-stu-id="99182-152">Specifying more than one WITH clause in a CTE is not allowed.</span></span> <span data-ttu-id="99182-153">Par exemple, si une définition CTE_query_definition contient une sous-requête, celle-ci ne peut pas contenir de clause WITH imbriquée définissant une autre CTE.</span><span class="sxs-lookup"><span data-stu-id="99182-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span></span>
* <span data-ttu-id="99182-154">Une clause ORDER BY ne peut pas être utilisée dans une définition CTE_query_definition, sauf lorsqu’une clause TOP est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="99182-154">An ORDER BY clause cannot be used in the CTE_query_definition, except when a TOP clause is specified.</span></span>
* <span data-ttu-id="99182-155">Lorsqu’une CTE est utilisée dans une instruction qui fait partie d’un lot, l’instruction qui la précède doit être suivie d’un point-virgule.</span><span class="sxs-lookup"><span data-stu-id="99182-155">When a CTE is used in a statement that is part of a batch, the statement before it must be followed by a semicolon.</span></span>
* <span data-ttu-id="99182-156">Lorsqu’une CTE est utilisée dans des instructions préparées par sp_prepare, celle-ci se comporte de la même façon que les autres instructions SELECT dans PDW.</span><span class="sxs-lookup"><span data-stu-id="99182-156">When used in statements prepared by sp_prepare, CTEs will behave the same way as other SELECT statements in PDW.</span></span> <span data-ttu-id="99182-157">Toutefois, si les expressions de table communes sont utilisées dans le cadre de CETAS préparées par sp_prepare, le comportement peut différer selon qu’il s’agit d’instructions SQL Server ou PDW en raison de la façon dont la liaison est mise en œuvre pour sp_prepare.</span><span class="sxs-lookup"><span data-stu-id="99182-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, the behavior can defer from SQL Server and other PDW statements because of the way binding is implemented for sp_prepare.</span></span> <span data-ttu-id="99182-158">Si l’instruction SELECT qui référence CTE utilise une colonne erronée, qui n’existe pas dans CTE, sp_prepare transmet sans détecter l’erreur, mais l’erreur est levée pendant l’instruction sp_execute.</span><span class="sxs-lookup"><span data-stu-id="99182-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, the sp_prepare will pass without detecting the error, but the error will be thrown during sp_execute instead.</span></span>

## <a name="recursive-ctes"></a><span data-ttu-id="99182-159">CTE récursives</span><span class="sxs-lookup"><span data-stu-id="99182-159">Recursive CTEs</span></span>
<span data-ttu-id="99182-160">Les expressions de table communes récursives ne sont pas prises en charge dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="99182-160">Recursive CTEs are not supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="99182-161">La migration de CTE récursives peut être relativement complexe et la meilleure solution reste de décomposer le processus en plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="99182-161">The migration of recursive CTE can be somewhat complex and the best process is to break it into multiple steps.</span></span> <span data-ttu-id="99182-162">Vous pouvez généralement utiliser une boucle pour une table temporaire pendant que vous parcourez les requêtes intermédiaires récursives.</span><span class="sxs-lookup"><span data-stu-id="99182-162">You can typically use a loop and populate a temporary table as you iterate over the recursive interim queries.</span></span> <span data-ttu-id="99182-163">Une fois la table temporaire remplie, vous pouvez renvoyer les données sous forme d’un seul jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="99182-163">Once the temporary table is populated you can then return the data as a single result set.</span></span> <span data-ttu-id="99182-164">Une approche similaire a été utilisée pour résoudre `GROUP BY WITH CUBE` dans l’article [Regroupement par clause à l’aide des options rollup/cube/grouping sets][group by clause with rollup / cube / grouping sets options].</span><span class="sxs-lookup"><span data-stu-id="99182-164">A similar approach has been used to solve `GROUP BY WITH CUBE` in the [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span></span>

## <a name="unsupported-system-functions"></a><span data-ttu-id="99182-165">Fonctions système non prises en charge</span><span class="sxs-lookup"><span data-stu-id="99182-165">Unsupported system functions</span></span>
<span data-ttu-id="99182-166">Certaines fonctions système ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="99182-166">There are also some system functions that are not supported.</span></span> <span data-ttu-id="99182-167">Voici les principales fonctions habituellement associées aux entrepôts de données :</span><span class="sxs-lookup"><span data-stu-id="99182-167">Some of the main ones you might typically find used in data warehousing are:</span></span>

* <span data-ttu-id="99182-168">NEWSEQUENTIALID()</span><span class="sxs-lookup"><span data-stu-id="99182-168">NEWSEQUENTIALID()</span></span>
* <span data-ttu-id="99182-169">@@NESTLEVEL()</span><span class="sxs-lookup"><span data-stu-id="99182-169">@@NESTLEVEL()</span></span>
* <span data-ttu-id="99182-170">@@IDENTITY()</span><span class="sxs-lookup"><span data-stu-id="99182-170">@@IDENTITY()</span></span>
* <span data-ttu-id="99182-171">@@ROWCOUNT()</span><span class="sxs-lookup"><span data-stu-id="99182-171">@@ROWCOUNT()</span></span>
* <span data-ttu-id="99182-172">ROWCOUNT_BIG</span><span class="sxs-lookup"><span data-stu-id="99182-172">ROWCOUNT_BIG</span></span>
* <span data-ttu-id="99182-173">ERROR_LINE()</span><span class="sxs-lookup"><span data-stu-id="99182-173">ERROR_LINE()</span></span>

<span data-ttu-id="99182-174">Certains de ces problèmes peuvent être contournés.</span><span class="sxs-lookup"><span data-stu-id="99182-174">Some of these issues can be worked around.</span></span>

## <a name="rowcount-workaround"></a><span data-ttu-id="99182-175">Solution de contournement pour @@ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="99182-175">@@ROWCOUNT workaround</span></span>
<span data-ttu-id="99182-176">Pour contourner l’absence de prise en charge de @@ROWCOUNT, créez une procédure stockée qui récupère le dernier nombre de lignes de sys.dm_pdw_request_steps puis exécute `EXEC LastRowCount` après une instruction DML.</span><span class="sxs-lookup"><span data-stu-id="99182-176">To work around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve the last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span></span>

```sql
CREATE PROCEDURE LastRowCount AS
WITH LastRequest as 
(   SELECT TOP 1    request_id
    FROM            sys.dm_pdw_exec_requests
    WHERE           session_id = SESSION_ID()
    AND             resource_class IS NOT NULL
    ORDER BY end_time DESC
),
LastRequestRowCounts as
(
    SELECT  step_index, row_count
    FROM    sys.dm_pdw_request_steps
    WHERE   row_count >= 0
    AND     request_id IN (SELECT request_id from LastRequest)
)
SELECT TOP 1 row_count FROM LastRequestRowCounts ORDER BY step_index DESC
;
```

## <a name="next-steps"></a><span data-ttu-id="99182-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="99182-177">Next steps</span></span>
<span data-ttu-id="99182-178">Pour obtenir la liste complète de toutes les instructions T-SQL prises en charge, consultez les [rubriques Transact-SQL][Transact-SQL topics].</span><span class="sxs-lookup"><span data-stu-id="99182-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span></span>

<!--Image references-->

<!--Article references-->
[ANSI joins on updates]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[ANSI joins on deletes]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[merge statement]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[INSERT..EXEC]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[Transact-SQL topics]: ./sql-data-warehouse-reference-tsql-statements.md

[cursors]: ./sql-data-warehouse-develop-loops.md
[group by clause with rollup / cube / grouping sets options]: ./sql-data-warehouse-develop-group-by-options.md
[nesting levels beyond 8]: ./sql-data-warehouse-develop-transactions.md
[updating through views]: ./sql-data-warehouse-develop-views.md
[use of select for variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[no MAX data type for dynamic SQL strings]: ./sql-data-warehouse-develop-dynamic-sql.md

<!--MSDN references-->

<!--Other Web references-->
