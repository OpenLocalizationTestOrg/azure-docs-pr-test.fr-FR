---
title: aaaMigrate votre tooSQL de code SQL Data Warehouse | Documents Microsoft
description: "Conseils pour migrer votre tooAzure de code SQL SQL Data Warehouse pour développer des solutions."
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
ms.openlocfilehash: 7a16d579d068e9df9aba3dc61e4a09bcaa551588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a>Migrer votre tooSQL de code SQL Data Warehouse
Cet article explique les modifications de code que vous aurez probablement besoin toomake lors de la migration de votre code à partir d’une autre base de données tooSQL l’entrepôt de données. Certaines fonctionnalités de SQL Data Warehouse peuvent améliorer considérablement les performances car ils sont conçu toowork en mode distribué. Toutefois, les performances de toomaintain et d’échelle, certaines fonctionnalités sont également pas disponibles.

## <a name="common-t-sql-limitations"></a>Limites courantes de T-SQL
Hello suivant liste récapitule les fonctionnalités courantes hello SQL Data Warehouse ne prend pas en charge. les liens Hello prennent tooworkarounds pour les fonctionnalités de hello non pris en charge :

* [Jointures ANSI sur les opérations UPDATE][ANSI joins on updates]
* [Jointures ANSI sur les opérations DELETE][ANSI joins on deletes]
* [Instruction MERGE][merge statement]
* Jonctions entre plusieurs bases de données
* [Curseurs][cursors]
* <seg>
  [INSERT..EXEC][INSERT..EXEC]</seg>
* Clause OUTPUT
* Fonctions en ligne définies par l’utilisateur
* Fonctions à instructions multiples
* [Expressions de table commune](#Common-table-expressions)
* [Expressions récursives de table commune (CTE)](#Expressions-récursives-de-table-commune-(CTE)
* Fonctions et procédures CLR
* Fonction $partition
* Variables de table
* Paramètres de valeurs de table
* Transactions distribuées
* Tâche de validation/restauration
* Transaction d’enregistrement
* Contextes d’exécution (EXECUTE AS)
* [Regroupement par clause à l’aide des options rollup/cube/grouping sets][group by clause with rollup / cube / grouping sets options]
* [Imbrication des niveaux au-delà de 8][nesting levels beyond 8]
* [Mise à jour par le biais de vues][updating through views]
* [Utilisation de Select pour l’attribution des variables][use of select for variable assignment]
* [Pas de type de données MAX pour les chaînes SQL dynamiques][no MAX data type for dynamic SQL strings]

Fort heureusement, la plupart de ces restrictions peuvent être contournées. Explications sont fournies dans les articles de développement pertinentes hello mentionnés ci-dessus.

## <a name="supported-cte-features"></a>Fonctionnalités CTE prises en charge
Les expressions de table communes (CTE) sont partiellement prises en charge dans SQL Data Warehouse.  Hello suivant les fonctionnalités de l’expression de table commune est actuellement prises en charge :

* Une CTE peut être spécifiée dans une instruction SELECT.
* Une CTE peut être spécifiée dans une instruction CREATE VIEW.
* Une CTE peut être spécifiée dans une instruction CREATE TABLE AS SELECT (CTAS).
* Une CTE peut être spécifiée dans une instruction CREATE REMOTE TABLE AS SELECT (CRTAS).
* Une CTE peut être spécifiée dans une instruction CREATE EXTERNAL TABLE AS SELECT (CETAS).
* Une table distante peut être référencée à partir d’une expression de table commune.
* Une table externe peut être référencée à partir d’une expression de table commune.
* Plusieurs définitions de requête CTE peuvent être définies dans une expression de table commune.

## <a name="cte-limitations"></a>Limitations d’une CTE
Les expressions de table communes présentent certaines restrictions dans SQL Data Warehouse, notamment :

* Une CTE doit être suivie d’une instruction SELECT unique. Les instructions INSERT, UPDATE, DELETE et MERGE ne sont pas prises en charge.
* Une expression de table commune qui inclut des références tooitself (expression de table commune récursive) n’est pas pris en charge (voir ci-dessous la section).
* La spécification de plusieurs clauses WITH dans une CTE n’est pas autorisée. Par exemple, si une définition CTE_query_definition contient une sous-requête, celle-ci ne peut pas contenir de clause WITH imbriquée définissant une autre CTE.
* Une clause ORDER BY ne peut pas servir Bonjour définitions de requêtes, cet, sauf lorsqu’une clause TOP est spécifiée.
* Lorsqu’une expression CTE est utilisée dans une instruction qui fait partie d’un lot, l’instruction hello avant qu’il doit être suivie par un point-virgule.
* Lorsqu’il est utilisé dans les instructions préparées par sp_prepare, CTE comporteront hello même façon que les autres instructions SELECT dans PDW. Toutefois, si les expressions de table communes sont utilisées dans le cadre de CETAS préparée par sp_prepare, comportement de hello peut différer de SQL Server et les autres instructions PDW en raison de façon hello est implémentée pour sp_prepare. Si l’option références que CTE utilise une mauvaise colonne qui n’existe pas dans l’expression de table commune, hello sp_prepare transmettra sans détection d’erreur de hello que hello une erreur est générée pendant sp_execute à la place.

## <a name="recursive-ctes"></a>CTE récursives
Les expressions de table communes récursives ne sont pas prises en charge dans SQL Data Warehouse.  migration Hello d’expression CTE récursive peut être relativement complexe et processus de meilleures hello est toobreak en plusieurs étapes. Vous pouvez généralement utiliser une boucle et remplir une table temporaire que vous parcourez les requêtes intermédiaires hello récursives. Une fois que la table temporaire de hello est remplie, vous pouvez ensuite revenir les données hello en tant qu’un seul jeu de résultats. Une approche similaire a été utilisé toosolve `GROUP BY WITH CUBE` Bonjour [regrouper par clause avec rollup, cube, définit les options de regroupement] [ group by clause with rollup / cube / grouping sets options] l’article.

## <a name="unsupported-system-functions"></a>Fonctions système non prises en charge
Certaines fonctions système ne sont pas prises en charge. Hello principales que vous constaterez généralement utilisé dans l’entrepôt de données sont notamment :

* NEWSEQUENTIALID()
* @@NESTLEVEL()
* @@IDENTITY()
* @@ROWCOUNT()
* ROWCOUNT_BIG
* ERROR_LINE()

Certains de ces problèmes peuvent être contournés.

## <a name="rowcount-workaround"></a>Solution de contournement pour @@ROWCOUNT
toowork autour d’un manque de prise en charge pour @@ROWCOUNT, créer une procédure stockée qui Récupère les hello dernier nombre de lignes à partir de sys.dm_pdw_request_steps et puis exécutez `EXEC LastRowCount` après une instruction DML.

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

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir la liste complète de toutes les instructions T-SQL prises en charge, consultez les [rubriques Transact-SQL][Transact-SQL topics].

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
