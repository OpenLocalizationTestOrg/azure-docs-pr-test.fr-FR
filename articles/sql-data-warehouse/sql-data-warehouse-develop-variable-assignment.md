---
title: "variables aaaAssign dans l’entrepôt de données SQL | Documents Microsoft"
description: "Conseils relatifs à l’affectation de variables Transact-SQL dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a>Affecter des variables dans SQL Data Warehouse
Variables dans l’entrepôt de données SQL sont définies à l’aide de hello `DECLARE` instruction ou hello `SET` instruction.

Hello qui suit sont parfaitement valides tooset une valeur de variable :

## <a name="setting-variables-with-declare"></a>Définition de variables via l’instruction DECLARE
Initialiser des variables avec DECLARE est hello plus souple façons tooset une valeur de variable dans l’entrepôt de données SQL.

```sql
DECLARE @v  int = 0
;
```

Vous pouvez également utiliser DECLARE tooset plus d’une variable à la fois. Vous ne pouvez pas utiliser `SELECT` ou `UPDATE` toodo cela :

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

Vous ne peut pas initialiser et utiliser une variable dans hello même instruction DECLARE. tooillustrate hello point hello exemple ci-dessous est **pas** autorisé en tant que @p1 est initialisé et utilisé dans hello même instruction DECLARE. Cela entraîne une erreur.

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a>Définition de valeurs avec l’instruction SET
L’instruction SET est très couramment utilisée pour définir une variable unique.

Tous les exemples hello ci-dessous sont définissant une variable avec un jeu de méthodes valides :

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

Avec l’instruction SET, vous pouvez uniquement définir une variable à la fois. Toutefois, comme indiqué ci-dessus, les opérateurs composés sont autorisés.

## <a name="limitations"></a>Limitations
Vous ne pouvez pas utiliser les instructions SELECT et UPDATE pour attribuer des variables.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
