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
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="1699c-103">Options de regroupement dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1699c-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="1699c-104">Hello [GROUP BY] [ GROUP BY] clause est utilisée tooaggregate tooa résumé série de données en lignes.</span><span class="sxs-lookup"><span data-stu-id="1699c-104">hello [GROUP BY][GROUP BY] clause is used tooaggregate data tooa summary set of rows.</span></span> <span data-ttu-id="1699c-105">Il a également quelques options qui étendent ses fonctionnalités que toobe besoin contourné car ils ne sont pas directement pris en charge par Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1699c-105">It also has a few options that extend it's functionality that need toobe worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="1699c-106">Ces options sont :</span><span class="sxs-lookup"><span data-stu-id="1699c-106">These options are</span></span>

* <span data-ttu-id="1699c-107">GROUP BY avec ROLLUP</span><span class="sxs-lookup"><span data-stu-id="1699c-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="1699c-108">GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="1699c-108">GROUPING SETS</span></span>
* <span data-ttu-id="1699c-109">GROUP BY avec CUBE</span><span class="sxs-lookup"><span data-stu-id="1699c-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="1699c-110">Options ROLLUP et GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="1699c-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="1699c-111">option la plus simple ici Hello est toouse `UNION ALL` à la place tooperform hello cumul plutôt que de compter sur hello syntaxe explicite.</span><span class="sxs-lookup"><span data-stu-id="1699c-111">hello simplest option here is toouse `UNION ALL` instead tooperform hello rollup rather than relying on hello explicit syntax.</span></span> <span data-ttu-id="1699c-112">résultat de Hello est exactement hello même</span><span class="sxs-lookup"><span data-stu-id="1699c-112">hello result is exactly hello same</span></span>

<span data-ttu-id="1699c-113">Voici un exemple d’un groupe par l’instruction à l’aide de hello `ROLLUP` option :</span><span class="sxs-lookup"><span data-stu-id="1699c-113">Below is an example of a group by statement using hello `ROLLUP` option:</span></span>

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

<span data-ttu-id="1699c-114">À l’aide du correctif cumulatif, nous avons demandé hello suivant des agrégations :</span><span class="sxs-lookup"><span data-stu-id="1699c-114">By using ROLLUP we have requested hello following aggregations:</span></span>

* <span data-ttu-id="1699c-115">Pays et région</span><span class="sxs-lookup"><span data-stu-id="1699c-115">Country and Region</span></span>
* <span data-ttu-id="1699c-116">Pays</span><span class="sxs-lookup"><span data-stu-id="1699c-116">Country</span></span>
* <span data-ttu-id="1699c-117">Total général</span><span class="sxs-lookup"><span data-stu-id="1699c-117">Grand Total</span></span>

<span data-ttu-id="1699c-118">tooreplace vous devez toouse `UNION ALL`; spécifiant les agrégations de hello requises explicitement tooreturn hello les mêmes résultats :</span><span class="sxs-lookup"><span data-stu-id="1699c-118">tooreplace this you will need toouse `UNION ALL`; specifying hello aggregations required explicitly tooreturn hello same results:</span></span>

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

<span data-ttu-id="1699c-119">Pour tout ce que nous devons toodo est adopter les jeux de regroupement hello même entité mais uniquement créer des sections UNION ALL pour hello niveaux d’agrégation, nous souhaitons toosee</span><span class="sxs-lookup"><span data-stu-id="1699c-119">For GROUPING SETS all we need toodo is adopt hello same principal but only create UNION ALL sections for hello aggregation levels we want toosee</span></span>

## <a name="cube-options"></a><span data-ttu-id="1699c-120">Options CUBE</span><span class="sxs-lookup"><span data-stu-id="1699c-120">Cube options</span></span>
<span data-ttu-id="1699c-121">Il est possible de toocreate un GROUP BY WITH CUBE à l’aide de la méthode UNION ALL de hello.</span><span class="sxs-lookup"><span data-stu-id="1699c-121">It is possible toocreate a GROUP BY WITH CUBE using hello UNION ALL approach.</span></span> <span data-ttu-id="1699c-122">problème de Hello est que les code hello peut rapidement s’avérer fastidieuse et complexe.</span><span class="sxs-lookup"><span data-stu-id="1699c-122">hello problem is that hello code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="1699c-123">toomitigate ce vous pouvez l’utiliser plus avancé approche.</span><span class="sxs-lookup"><span data-stu-id="1699c-123">toomitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="1699c-124">Nous allons utiliser exemple hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="1699c-124">Let's use hello example above.</span></span>

<span data-ttu-id="1699c-125">première étape de Hello est toodefine hello « cube » qui définit tous les niveaux de hello d’agrégation que nous souhaitons toocreate.</span><span class="sxs-lookup"><span data-stu-id="1699c-125">hello first step is toodefine hello 'cube' that defines all hello levels of aggregation that we want toocreate.</span></span> <span data-ttu-id="1699c-126">Il est important tootake Hello CROSS JOIN de deux tables de dérivée hello.</span><span class="sxs-lookup"><span data-stu-id="1699c-126">It is important tootake note of hello CROSS JOIN of hello two derived tables.</span></span> <span data-ttu-id="1699c-127">Cette opération génère tous les niveaux de hello pour nous.</span><span class="sxs-lookup"><span data-stu-id="1699c-127">This generates all hello levels for us.</span></span> <span data-ttu-id="1699c-128">Hello reste du code de hello est vraiment il pour mettre en forme.</span><span class="sxs-lookup"><span data-stu-id="1699c-128">hello rest of hello code is really there for formatting.</span></span>

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

<span data-ttu-id="1699c-129">Hello Hello SACT pouvez consulter les résultats ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1699c-129">hello results of hello CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="1699c-130">deuxième étape de Hello est toospecify qu'un intérimaire toostore du tableau cible des résultats :</span><span class="sxs-lookup"><span data-stu-id="1699c-130">hello second step is toospecify a target table toostore interim results:</span></span>

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

<span data-ttu-id="1699c-131">troisième étape de Hello est tooloop sur notre cube des colonnes d’agrégation de hello.</span><span class="sxs-lookup"><span data-stu-id="1699c-131">hello third step is tooloop over our cube of columns performing hello aggregation.</span></span> <span data-ttu-id="1699c-132">Hello requête exécutée une fois pour chaque ligne dans la table temporaire de hello #Cube et stocker les résultats de hello dans la table temporaire de hello #Results</span><span class="sxs-lookup"><span data-stu-id="1699c-132">hello query will run once for every row in hello #Cube temporary table and store hello results in hello #Results temp table</span></span>

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

<span data-ttu-id="1699c-133">Enfin, nous pouvons retourner les résultats de hello en lisant simplement à partir de la table temporaire de hello #Results</span><span class="sxs-lookup"><span data-stu-id="1699c-133">Lastly we can return hello results by simply reading from hello #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="1699c-134">En rupture du code de hello sections et en générant un bouclage Bonjour de construction de code devient plus gérable et plus facile à gérer.</span><span class="sxs-lookup"><span data-stu-id="1699c-134">By breaking hello code up into sections and generating a looping construct hello code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1699c-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1699c-135">Next steps</span></span>
<span data-ttu-id="1699c-136">Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="1699c-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
