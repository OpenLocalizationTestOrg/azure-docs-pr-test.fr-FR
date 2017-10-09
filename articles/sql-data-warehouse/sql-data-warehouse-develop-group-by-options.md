---
title: "aaaGroup par les options dans l’entrepôt de données SQL | Documents Microsoft"
description: "Conseils relatifs à l’implémentation d’options de regroupement dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f95a1e43-768f-4b7b-8a10-8a0509d0c871
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: cc443c2af4e3ef2babd74d78aa6fb57bb3c1c7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a>Options de regroupement dans SQL Data Warehouse
Hello [GROUP BY] [ GROUP BY] clause est utilisée tooaggregate tooa résumé série de données en lignes. Il a également quelques options qui étendent ses fonctionnalités que toobe besoin contourné car ils ne sont pas directement pris en charge par Azure SQL Data Warehouse.

Ces options sont :

* GROUP BY avec ROLLUP
* GROUPING SETS
* GROUP BY avec CUBE

## <a name="rollup-and-grouping-sets-options"></a>Options ROLLUP et GROUPING SETS
option la plus simple ici Hello est toouse `UNION ALL` à la place tooperform hello cumul plutôt que de compter sur hello syntaxe explicite. résultat de Hello est exactement hello même

Voici un exemple d’un groupe par l’instruction à l’aide de hello `ROLLUP` option :

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount)             AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t       ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY ROLLUP (
                        [SalesTerritoryCountry]
                ,       [SalesTerritoryRegion]
                )
;
```

À l’aide du correctif cumulatif, nous avons demandé hello suivant des agrégations :

* Pays et région
* Pays
* Total général

tooreplace vous devez toouse `UNION ALL`; spécifiant les agrégations de hello requises explicitement tooreturn hello les mêmes résultats :

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
UNION ALL
SELECT [SalesTerritoryCountry]
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
UNION ALL
SELECT NULL
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey;
```

Pour tout ce que nous devons toodo est adopter les jeux de regroupement hello même entité mais uniquement créer des sections UNION ALL pour hello niveaux d’agrégation, nous souhaitons toosee

## <a name="cube-options"></a>Options CUBE
Il est possible de toocreate un GROUP BY WITH CUBE à l’aide de la méthode UNION ALL de hello. problème de Hello est que les code hello peut rapidement s’avérer fastidieuse et complexe. toomitigate ce vous pouvez l’utiliser plus avancé approche.

Nous allons utiliser exemple hello ci-dessus.

première étape de Hello est toodefine hello « cube » qui définit tous les niveaux de hello d’agrégation que nous souhaitons toocreate. Il est important tootake Hello CROSS JOIN de deux tables de dérivée hello. Cette opération génère tous les niveaux de hello pour nous. Hello reste du code de hello est vraiment il pour mettre en forme.

```sql
CREATE TABLE #Cube
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
AS
WITH GrpCube AS
(SELECT    CAST(ISNULL(Country,'NULL')+','+ISNULL(Region,'NULL') AS NVARCHAR(50)) as 'Cols'
,          CAST(ISNULL(Country+',','')+ISNULL(Region,'') AS NVARCHAR(50))  as 'GroupBy'
,          ROW_NUMBER() OVER (ORDER BY Country) as 'Seq'
FROM       ( SELECT 'SalesTerritoryCountry' as Country
             UNION ALL
             SELECT NULL
           ) c
CROSS JOIN ( SELECT 'SalesTerritoryRegion' as Region
             UNION ALL
             SELECT NULL
           ) r
)
SELECT Cols
,      CASE WHEN SUBSTRING(GroupBy,LEN(GroupBy),1) = ','
            THEN SUBSTRING(GroupBy,1,LEN(GroupBy)-1)
            ELSE GroupBy
       END AS GroupBy  --Remove Trailing Comma
,Seq
FROM GrpCube;
```

Hello Hello SACT pouvez consulter les résultats ci-dessous :

![][1]

deuxième étape de Hello est toospecify qu'un intérimaire toostore du tableau cible des résultats :

```sql
DECLARE
 @SQL NVARCHAR(4000)
,@Columns NVARCHAR(4000)
,@GroupBy NVARCHAR(4000)
,@i INT = 1
,@nbr INT = 0
;
CREATE TABLE #Results
(
 [SalesTerritoryCountry] NVARCHAR(50)
,[SalesTerritoryRegion]  NVARCHAR(50)
,[TotalSalesAmount]      MONEY
)
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
;
```

troisième étape de Hello est tooloop sur notre cube des colonnes d’agrégation de hello. Hello requête exécutée une fois pour chaque ligne dans la table temporaire de hello #Cube et stocker les résultats de hello dans la table temporaire de hello #Results

```sql
SET @nbr =(SELECT MAX(Seq) FROM #Cube);

WHILE @i<=@nbr
BEGIN
    SET @Columns = (SELECT Cols    FROM #Cube where seq = @i);
    SET @GroupBy = (SELECT GroupBy FROM #Cube where seq = @i);

    SET @SQL ='INSERT INTO #Results
              SELECT '+@Columns+'
              ,      SUM(SalesAmount) AS TotalSalesAmount
              FROM  dbo.factInternetSales s
              JOIN  dbo.DimSalesTerritory t  
              ON s.SalesTerritoryKey = t.SalesTerritoryKey
              '+CASE WHEN @GroupBy <>''
                     THEN 'GROUP BY '+@GroupBy ELSE '' END

    EXEC sp_executesql @SQL;
    SET @i +=1;
END
```

Enfin, nous pouvons retourner les résultats de hello en lisant simplement à partir de la table temporaire de hello #Results

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

En rupture du code de hello sections et en générant un bouclage Bonjour de construction de code devient plus gérable et plus facile à gérer.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
