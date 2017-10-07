---
title: "procédures d’aaaStored dans l’entrepôt de données SQL | Documents Microsoft"
description: "Conseils relatifs à l’implémentation de procédures stockées dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a>Procédures stockées dans SQL Data Warehouse
Entrepôt de données SQL prend en charge plusieurs fonctionnalités hello Transact-SQL dans SQL Server. Il n’y a plus important encore montée en charge des fonctionnalités spécifiques que nous voudrons performances de hello tooleverage toomaximize de votre solution.

Toutefois, l’échelle de toomaintain hello et il les performances de l’entrepôt de données SQL sont également certaines fonctions et fonctionnalités qui ont des différences de comportement et d’autres qui ne sont pas pris en charge.

Cet article explique comment tooimplement procédures au sein de l’entrepôt de données SQL.

## <a name="introducing-stored-procedures"></a>Présentation des procédures stockées
Les procédures stockées sont un excellent moyen d’encapsuler votre code SQL. stocker les données tooyour Fermer dans l’entrepôt de données hello. En encapsulant les code hello en unités gérables, procédures stockées aident les développeurs modulariser leurs solutions. faciliter une plus grande réutilisation du code. Chaque procédure stockée peut également accepter des paramètres toomake les encore plus flexible.

SQL Data Warehouse fournit une implémentation simplifiée et rationalisée pour les procédures stockées. Hello plus grande différence par rapport tooSQL Server est que hello la procédure stockée n’est pas code précompilé. Dans les entrepôts de données nous intéresse généralement moins avec le temps de compilation hello. Il est plus important que code de la procédure stockée hello est optimisé pour correctement lorsqu’il fonctionne sur gros volumes de données. Hello vise toosave heures, minutes et secondes pas les millisecondes. Il est donc plus utile toothink des procédures stockées en tant que conteneurs pour la logique SQL.     

Lors de l’exécution de SQL Data Warehouse votre procédure stockée hello instructions SQL sont analysées, traduites et optimisées au moment de l’exécution. Lors de ce processus, chaque instruction est convertie en différentes requêtes distribuées. Hello code SQL réellement exécuté sur les données de salutation est requête toohello différents soumise.

## <a name="nesting-stored-procedures"></a>Imbrication des procédures stockées
Lorsque des procédures stockées appellent d’autres procédures stockées ou exécuter des sql dynamique interne de hello de procédure stockée ou d’appel de code est dite toobe imbriqués.

SQL Data Warehouse prend en charge un maximum de 8 niveaux d’imbrication. Il s’agit de légèrement tooSQL Server. niveau d’imbrication Hello dans SQL Server est 32.

appel de procédure stockée de niveau supérieur Hello équivaut toonest niveau 1

```sql
EXEC prc_nesting
```
Si hello stockée procédure effectue également un autre EXEC appel puis Cela augmentera too2 au niveau de hello imbrication

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
Si la deuxième procédure de hello puis exécute des instructions sql dynamiques puis Cela augmentera too3 au niveau de hello imbrication

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

Notez que SQL Data Warehouse ne prend pas en charge @@NESTLEVEL. Vous devez vous-même tookeep un suivi de votre niveau d’imbrication. Il est improbable que vous atteignez limite de niveau d’imbrication hello 8. Toutefois, si vous vous aura besoin professionnel toore votre code et de « aplatir » afin qu’il tienne dans cette limite.

## <a name="insertexecute"></a>INSERT... EXECUTE
SQL Data Warehouse n’autorise pas jeu de résultats tooconsume hello d’une procédure stockée avec une instruction INSERT. Toutefois, vous pouvez utiliser une autre méthode.

Reportez-vous toohello l’article suivant [tables temporaires] pour obtenir un exemple sur la façon de toodo cela.

## <a name="limitations"></a>Limites
Certains aspects des procédures stockées Transact-SQL ne sont pas implémentés dans SQL Data Warehouse.

Les voici :

* Procédures stockées temporaires
* Procédures stockées numérotées
* Procédures stockées étendues
* Procédures stockées CLR
* Option de chiffrement
* Option de réplication
* Paramètres table
* Paramètres en lecture seule
* Paramètres par défaut
* Contextes d’exécution
* Instruction RETURN

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].

<!--Image references-->

<!--Article references-->
[tables temporaires]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
