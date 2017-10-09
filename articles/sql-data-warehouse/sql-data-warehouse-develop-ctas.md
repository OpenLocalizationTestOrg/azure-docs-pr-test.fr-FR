---
title: "table aaaCreate que vous sélectionnez (SACT) dans l’entrepôt de données SQL | Documents Microsoft"
description: "Conseils pour le codage par hello créer la table que vous sélectionnez l’instruction de (SACT) dans l’entrepôt de données SQL Azure pour développer des solutions."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 68ac9a94-09f9-424b-b536-06a125a653bd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 01/30/2017
ms.author: shigu;barbkess
ms.openlocfilehash: e381601a0a4d94e189d8f9115bf2e7593025410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a>Instruction Create Table As Select (CTAS) dans SQL Data Warehouse
Créer la table en tant que select ou `CTAS` est un de hello plus importantes fonctionnalités T-SQL disponibles. Il s’agit d’une opération entièrement parallélisée qui crée une table basée sur sortie hello d’une instruction SELECT. `CTAS`toocreate de la façon la plus simple et plus rapide de hello n’est une copie d’une table. Ce document fournit des exemples et les meilleures pratiques pour `CTAS`.

## <a name="selectinto-vs-ctas"></a>SELECT..INTO et CTAS
`CTAS` est en quelque sorte une version améliorée de `SELECT..INTO`.

Vous trouverez ci-dessous un exemple simple d’une instruction `SELECT..INTO` :

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

Dans l’exemple hello ci-dessus `[dbo].[FactInternetSales_new]` seront créées en tant que table de distribuées ROUND_ROBIN avec un INDEX COLUMNSTORE en cluster sur ce dernier, car il s’agit des valeurs par défaut de la table hello dans Azure SQL Data Warehouse.

`SELECT..INTO`toutefois vous interdit toochange soit hello distribution méthode ou hello l’index de type dans le cadre de l’opération de hello. C’est là où `CTAS` entre en jeu.

tooconvert hello ci-dessus trop`CTAS` est très simple :

```sql
CREATE TABLE [dbo].[FactInternetSales_new]
WITH
(
    DISTRIBUTION = ROUND_ROBIN
,   CLUSTERED COLUMNSTORE INDEX
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

Avec `CTAS` vous êtes en mesure de toochange à la fois hello distribution des données de table hello comme type de table hello. 

> [!NOTE]
> Si vous essayez uniquement les index de hello toochange dans votre `CTAS` opération et hello la table source est distribué de hachage votre `CTAS` opération effectue mieux si vous conservez hello même type de colonne et les données de distribution. Cela permet d’éviter entre le déplacement des données de distribution au cours de l’opération hello qui est plus efficace.
> 
> 

## <a name="using-ctas-toocopy-a-table"></a>À l’aide de SACT toocopy une table
Peut-être un des plus courants de hello utilise de `CTAS` crée une copie d’une table afin que vous puissiez modifier hello DDL. Si par exemple vous avez créé votre table en tant que `ROUND_ROBIN` et maintenant que vous souhaitez modifier tooa table distribuée sur une colonne, `CTAS` est la façon dont vous pouvez modifier la colonne de distribution hello. `CTAS`peut également être utilisé toochange types de partitionnement, l’indexation ou de colonne.

Supposons que vous avez créé ce tableau à l’aide du type de distribution par défaut hello `ROUND_ROBIN` distribuées car aucune colonne de distribution a été spécifié dans hello `CREATE TABLE`.

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

Maintenant, vous souhaitez toocreate une nouvelle copie de cette table avec un Index cluster Columnstore afin que vous pouvez tirer parti des performances de hello de tables de Columnstore cluster. Vous souhaitez également toodistribute cette table sur ProductKey dans la mesure où vous comptez les jointures sur cette colonne et que vous souhaitez le déplacement des données de tooavoid pendant les jointures sur ProductKey. Enfin vous également tooadd partitionnement sur OrderDateKey afin que vous pouvez rapidement supprimer les anciennes données en supprimant les anciennes partitions. Voici l’instruction SACT hello copiez votre ancienne table dans une nouvelle table.

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

Enfin, vous pouvez renommer votre tooswap de tables dans votre nouvelle table et puis supprimez votre ancienne table.

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> Azure SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique.  Dans l’ordre tooget hello optimiser les performances de vos requêtes, il est important que créer des statistiques sur toutes les colonnes de toutes les tables après le premier chargement de hello ou toutes les modifications importantes se produisent dans les données de salutation.  Pour obtenir une explication détaillée des statistiques, consultez hello [statistiques] [ Statistics] rubrique dans le groupe de développement hello de rubriques.
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a>À l’aide de toowork SACT sur les fonctionnalités non prises en charge
`CTAS`peut également être utilisé toowork autour d’un nombre de fonctionnalités hello non pris en charge répertoriées ci-dessous. Ceci peut souvent s’avérer toobe une situation gagnant/gagnant comme non seulement votre code sera conforme, mais il s’exécute souvent plus rapidement sur SQL Data Warehouse. Ces deux avantages découlent de sa conception entièrement parallélisée. Les scénarios qui peuvent être contournés avec CTAS comprennent notamment :

* Jointures ANSI sur les opérations UPDATE
* Jointures ANSI sur les opérations DELETE
* Instruction MERGE

> [!NOTE]
> Essayez toothink « SACT premier ». Si vous pensez que vous pouvez résoudre un problème à l’aide de `CTAS` , qui est généralement hello meilleure manière tooapproach il - même si vous écrivez des données en conséquence.
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a>Remplacement de jointures ANSI pour les instructions de mise à jour
Vous pouvez trouver qu'une mise à jour complexe qui joint plus de deux tables à l’aide de ANSI hello tooperform de syntaxe de jointure UPDATE ou DELETE.

Imaginez que vous aviez tooupdate cette table :

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(    [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,    [CalendarYear]                    SMALLINT        NOT NULL
,    [TotalSalesAmount]                MONEY            NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

requête d’origine de Hello peut avoir recherché quelque chose comme ceci :

```sql
UPDATE    acs
SET        [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT    [EnglishProductCategoryName]
        ,        [CalendarYear]
        ,        SUM([SalesAmount])                AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]        AS s
        JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
        JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
        WHERE     [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,        [CalendarYear]
        ) AS fis
ON    [acs].[EnglishProductCategoryName]    = [fis].[EnglishProductCategoryName]
AND    [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

Étant donné que l’entrepôt de données SQL ne prend pas en charge ANSI joint Bonjour `FROM` clause d’une `UPDATE` instruction, vous ne pouvez pas copier ce code sur sans quelques modifications apportées.

Vous pouvez utiliser une combinaison d’un `CTAS` et implicite joindre tooreplace ce code :

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT    ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,        ISNULL(CAST([CalendarYear] AS SMALLINT),0)                         AS [CalendarYear]
,        ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                        AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]        AS s
JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
WHERE     [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,        [CalendarYear]
;

-- Use an implicit join tooperform hello update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop hello interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a>Remplacement de jointures ANSI pour les instructions de suppression
Hello meilleure approche pour la suppression des données est parfois toouse `CTAS`. Plutôt que la suppression des données hello sélectionnez simplement les données hello tookeep. Cette particulièrement vrai pour `DELETE` instructions qui utilisent ansi rejoindre la syntaxe SQL Data Warehouse ne prenant pas en charge les jointures ANSI Bonjour `FROM` clause d’un `DELETE` instruction.

Voici un exemple d’instruction DELETE convertie :

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish tookeep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        tooDimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert tooDimProduct;
```

## <a name="replace-merge-statements"></a>Remplacement d’instructions MERGE
Vous pouvez remplacer les instructions MERGE, du moins partiellement, à l’aide de `CTAS`. Vous pouvez consolider hello `INSERT` et hello `UPDATE` dans une instruction unique. Tous les enregistrements supprimés faudrait toobe clôturé dans une deuxième instruction.

Voici un exemple d’utilisation d’une instruction consolidée `UPSERT` :

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          too[DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  too[DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a>Recommandation CTAS : déclarer explicitement le type de données et la possibilité de valeur NULL de la sortie
Lorsque vous procédez à la migration de votre code, vous pouvez constater que vous exécutez le type de modèle de codage suivant :

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

Instinctivement, vous pouvez considérer ce tooa code SACT, vous devez migrer et vous serait correcte. Toutefois, un problème se dissimule derrière ce scénario.

Hello de code suivant ne génère pas hello même résultat :

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

Notez que hello colonne « result » comporte des valeurs de type et la possibilité de valeur null de données d’expression de hello hello vers l’avant. Cela peut entraîner des écarts de toosubtle dans les valeurs si vous ne faites pas attention.

Essayez les opérations suivantes de hello par exemple :

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

valeur Hello stocké pour le résultat est différent. Comme une valeur persistante dans la colonne de résultats hello hello est utilisée dans d’autres erreurs de hello expressions devient encore plus important.

![][1]

Ceci se révèle particulièrement important dans le cas des migrations de données. Même si la requête de deuxième hello est sans doute plus précis, il existe un problème. les données de salutation serait système de source toohello comparés différentes et qui conduit tooquestions d’intégrité dans la migration hello. Il s’agit d’une des ces rares cas où une réponse « incorrecte » hello est réellement hello droite !

Hello raison pour laquelle nous voir cette disparité entre les résultats de deux de hello est arrêté tooimplicit cast de type. Bonjour premier exemple de table hello définit la définition de colonne hello. Lors de la ligne de hello est insérée une conversion de type implicite se produit. Dans le deuxième exemple de hello n’existe aucune conversion de type implicite comme expression de hello définit le type de données de colonne de hello. Notez que également que la colonne hello hello deuxième exemple a été définie comme une colonne acceptant les valeurs NULL alors que dans le premier exemple de hello il n’a pas. Lors de la création de table de hello dans hello premier exemple colonne possibilité de valeur null a été définie explicitement. Dans le deuxième exemple de hello, il était juste toohello expression et par défaut, cela se traduirait dans une définition de valeur NULL.  

tooresolve ces problèmes qui vous devez définir explicitement de conversion de type hello et la possibilité de valeur NULL dans hello `SELECT` partie Hello `CTAS` instruction. Vous ne pouvez pas définir ces propriétés dans hello créent la partie de la table.

exemple Hello ci-dessous montre comment toofix hello code :

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

Notez hello suivantes :

* Nous aurions pu utiliser CAST ou CONVERT.
* ISNULL est utilisé tooforce COALESCE pas de valeurs null
* ISNULL est fonction extérieur hello
* Hello deuxième partie de hello ISNULL est une constante c'est-à-dire 0

> [!NOTE]
> Pour toobe de possibilité de valeur null hello correctement défini est vital toouse `ISNULL` et non `COALESCE`. `COALESCE`n’est pas une fonction déterministe et donc hello résultat d’expression de hello sera toujours NULLable. `ISNULL` est différent. Cette fonction est déterministe. Par conséquent, lorsque hello deuxième partie de hello `ISNULL` fonction est une constante ou un littéral, valeur obtenue de hello est non NULL.
> 
> 

Ce Conseil n’est pas seulement utile pour garantir l’intégrité de hello de vos calculs. Il est également important dans le cadre du basculement de partition de table. Imaginons que vous ayez défini la table suivante :

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

Toutefois, le champ de valeur hello est une expression calculée, il n’est pas partie de la source de données hello.

toocreate votre jeu de données partitionnée que vous pourriez toodo cela :

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

requête de Hello s’exécute parfaitement. problème de Hello est fourni lorsque vous essayez de basculement de partition tooperform hello. les définitions de table Hello ne correspondent pas. définitions de table toomake hello correspond à hello que SACT doit toobe modifié.

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

Vous pouvez alors constater que la cohérence des types et le maintien des propriétés de possibilité de valeur Null sur une instruction CTAS constituent des approches d’ingénierie judicieuses. Il permet l’intégrité des toomaintain dans vos calculs et garantit également que le basculement de partition est possible.

Pour plus d’informations sur l’utilisation, consultez tooMSDN [SACT][CTAS]. Il est une des instructions plus importantes de hello dans Azure SQL Data Warehouse. Vous devez donc faire en sorte d’en comprendre les moindres aspects.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
