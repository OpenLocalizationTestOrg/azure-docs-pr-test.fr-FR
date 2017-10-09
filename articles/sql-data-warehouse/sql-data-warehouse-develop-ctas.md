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
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="7dca3-103">Instruction Create Table As Select (CTAS) dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7dca3-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="7dca3-104">Créer la table en tant que select ou `CTAS` est un de hello plus importantes fonctionnalités T-SQL disponibles.</span><span class="sxs-lookup"><span data-stu-id="7dca3-104">Create table as select or `CTAS` is one of hello most important T-SQL features available.</span></span> <span data-ttu-id="7dca3-105">Il s’agit d’une opération entièrement parallélisée qui crée une table basée sur sortie hello d’une instruction SELECT.</span><span class="sxs-lookup"><span data-stu-id="7dca3-105">It is a fully parallelized operation that creates a new table based on hello output of a SELECT statement.</span></span> <span data-ttu-id="7dca3-106">`CTAS`toocreate de la façon la plus simple et plus rapide de hello n’est une copie d’une table.</span><span class="sxs-lookup"><span data-stu-id="7dca3-106">`CTAS` is hello simplest and fastest way toocreate a copy of a table.</span></span> <span data-ttu-id="7dca3-107">Ce document fournit des exemples et les meilleures pratiques pour `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="7dca3-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="7dca3-108">SELECT..INTO et CTAS</span><span class="sxs-lookup"><span data-stu-id="7dca3-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="7dca3-109">`CTAS` est en quelque sorte une version améliorée de `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="7dca3-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="7dca3-110">Vous trouverez ci-dessous un exemple simple d’une instruction `SELECT..INTO` :</span><span class="sxs-lookup"><span data-stu-id="7dca3-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="7dca3-111">Dans l’exemple hello ci-dessus `[dbo].[FactInternetSales_new]` seront créées en tant que table de distribuées ROUND_ROBIN avec un INDEX COLUMNSTORE en cluster sur ce dernier, car il s’agit des valeurs par défaut de la table hello dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7dca3-111">In hello example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are hello table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="7dca3-112">`SELECT..INTO`toutefois vous interdit toochange soit hello distribution méthode ou hello l’index de type dans le cadre de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="7dca3-112">`SELECT..INTO` however does not allow you toochange either hello distribution method or hello index type as part of hello operation.</span></span> <span data-ttu-id="7dca3-113">C’est là où `CTAS` entre en jeu.</span><span class="sxs-lookup"><span data-stu-id="7dca3-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="7dca3-114">tooconvert hello ci-dessus trop`CTAS` est très simple :</span><span class="sxs-lookup"><span data-stu-id="7dca3-114">tooconvert hello above too`CTAS` is quite straight-forward:</span></span>

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

<span data-ttu-id="7dca3-115">Avec `CTAS` vous êtes en mesure de toochange à la fois hello distribution des données de table hello comme type de table hello.</span><span class="sxs-lookup"><span data-stu-id="7dca3-115">With `CTAS` you are able toochange both hello distribution of hello table data as well as hello table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="7dca3-116">Si vous essayez uniquement les index de hello toochange dans votre `CTAS` opération et hello la table source est distribué de hachage votre `CTAS` opération effectue mieux si vous conservez hello même type de colonne et les données de distribution.</span><span class="sxs-lookup"><span data-stu-id="7dca3-116">If you are only trying toochange hello index in your `CTAS` operation and hello source table is hash distributed then your `CTAS` operation will perform best if you maintain hello same distribution column and data type.</span></span> <span data-ttu-id="7dca3-117">Cela permet d’éviter entre le déplacement des données de distribution au cours de l’opération hello qui est plus efficace.</span><span class="sxs-lookup"><span data-stu-id="7dca3-117">This will avoid cross distribution data movement during hello operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-toocopy-a-table"></a><span data-ttu-id="7dca3-118">À l’aide de SACT toocopy une table</span><span class="sxs-lookup"><span data-stu-id="7dca3-118">Using CTAS toocopy a table</span></span>
<span data-ttu-id="7dca3-119">Peut-être un des plus courants de hello utilise de `CTAS` crée une copie d’une table afin que vous puissiez modifier hello DDL.</span><span class="sxs-lookup"><span data-stu-id="7dca3-119">Perhaps one of hello most common uses of `CTAS` is creating a copy of a table so that you can change hello DDL.</span></span> <span data-ttu-id="7dca3-120">Si par exemple vous avez créé votre table en tant que `ROUND_ROBIN` et maintenant que vous souhaitez modifier tooa table distribuée sur une colonne, `CTAS` est la façon dont vous pouvez modifier la colonne de distribution hello.</span><span class="sxs-lookup"><span data-stu-id="7dca3-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it tooa table distributed on a column, `CTAS` is how you would change hello distribution column.</span></span> <span data-ttu-id="7dca3-121">`CTAS`peut également être utilisé toochange types de partitionnement, l’indexation ou de colonne.</span><span class="sxs-lookup"><span data-stu-id="7dca3-121">`CTAS` can also be used toochange partitioning, indexing, or column types.</span></span>

<span data-ttu-id="7dca3-122">Supposons que vous avez créé ce tableau à l’aide du type de distribution par défaut hello `ROUND_ROBIN` distribuées car aucune colonne de distribution a été spécifié dans hello `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="7dca3-122">Let's say you created this table using hello default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in hello `CREATE TABLE`.</span></span>

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

<span data-ttu-id="7dca3-123">Maintenant, vous souhaitez toocreate une nouvelle copie de cette table avec un Index cluster Columnstore afin que vous pouvez tirer parti des performances de hello de tables de Columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="7dca3-123">Now you want toocreate a new copy of this table with a Clustered Columnstore Index so that you can take advantage of hello performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="7dca3-124">Vous souhaitez également toodistribute cette table sur ProductKey dans la mesure où vous comptez les jointures sur cette colonne et que vous souhaitez le déplacement des données de tooavoid pendant les jointures sur ProductKey.</span><span class="sxs-lookup"><span data-stu-id="7dca3-124">You also want toodistribute this table on ProductKey since you are anticipating joins on this column and want tooavoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="7dca3-125">Enfin vous également tooadd partitionnement sur OrderDateKey afin que vous pouvez rapidement supprimer les anciennes données en supprimant les anciennes partitions.</span><span class="sxs-lookup"><span data-stu-id="7dca3-125">Lastly you also want tooadd partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="7dca3-126">Voici l’instruction SACT hello copiez votre ancienne table dans une nouvelle table.</span><span class="sxs-lookup"><span data-stu-id="7dca3-126">Here is hello CTAS statement which would copy your old table into a new table.</span></span>

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

<span data-ttu-id="7dca3-127">Enfin, vous pouvez renommer votre tooswap de tables dans votre nouvelle table et puis supprimez votre ancienne table.</span><span class="sxs-lookup"><span data-stu-id="7dca3-127">Finally you can rename your tables tooswap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="7dca3-128">Azure SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique.</span><span class="sxs-lookup"><span data-stu-id="7dca3-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="7dca3-129">Dans l’ordre tooget hello optimiser les performances de vos requêtes, il est important que créer des statistiques sur toutes les colonnes de toutes les tables après le premier chargement de hello ou toutes les modifications importantes se produisent dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="7dca3-129">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="7dca3-130">Pour obtenir une explication détaillée des statistiques, consultez hello [statistiques] [ Statistics] rubrique dans le groupe de développement hello de rubriques.</span><span class="sxs-lookup"><span data-stu-id="7dca3-130">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a><span data-ttu-id="7dca3-131">À l’aide de toowork SACT sur les fonctionnalités non prises en charge</span><span class="sxs-lookup"><span data-stu-id="7dca3-131">Using CTAS toowork around unsupported features</span></span>
<span data-ttu-id="7dca3-132">`CTAS`peut également être utilisé toowork autour d’un nombre de fonctionnalités hello non pris en charge répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7dca3-132">`CTAS` can also be used toowork around a number of hello unsupported features listed below.</span></span> <span data-ttu-id="7dca3-133">Ceci peut souvent s’avérer toobe une situation gagnant/gagnant comme non seulement votre code sera conforme, mais il s’exécute souvent plus rapidement sur SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7dca3-133">This can often prove toobe a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="7dca3-134">Ces deux avantages découlent de sa conception entièrement parallélisée.</span><span class="sxs-lookup"><span data-stu-id="7dca3-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="7dca3-135">Les scénarios qui peuvent être contournés avec CTAS comprennent notamment :</span><span class="sxs-lookup"><span data-stu-id="7dca3-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="7dca3-136">Jointures ANSI sur les opérations UPDATE</span><span class="sxs-lookup"><span data-stu-id="7dca3-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="7dca3-137">Jointures ANSI sur les opérations DELETE</span><span class="sxs-lookup"><span data-stu-id="7dca3-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="7dca3-138">Instruction MERGE</span><span class="sxs-lookup"><span data-stu-id="7dca3-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="7dca3-139">Essayez toothink « SACT premier ».</span><span class="sxs-lookup"><span data-stu-id="7dca3-139">Try toothink "CTAS first".</span></span> <span data-ttu-id="7dca3-140">Si vous pensez que vous pouvez résoudre un problème à l’aide de `CTAS` , qui est généralement hello meilleure manière tooapproach il - même si vous écrivez des données en conséquence.</span><span class="sxs-lookup"><span data-stu-id="7dca3-140">If you think you can solve a problem using `CTAS` then that is generally hello best way tooapproach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="7dca3-141">Remplacement de jointures ANSI pour les instructions de mise à jour</span><span class="sxs-lookup"><span data-stu-id="7dca3-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="7dca3-142">Vous pouvez trouver qu'une mise à jour complexe qui joint plus de deux tables à l’aide de ANSI hello tooperform de syntaxe de jointure UPDATE ou DELETE.</span><span class="sxs-lookup"><span data-stu-id="7dca3-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax tooperform hello UPDATE or DELETE.</span></span>

<span data-ttu-id="7dca3-143">Imaginez que vous aviez tooupdate cette table :</span><span class="sxs-lookup"><span data-stu-id="7dca3-143">Imagine you had tooupdate this table:</span></span>

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

<span data-ttu-id="7dca3-144">requête d’origine de Hello peut avoir recherché quelque chose comme ceci :</span><span class="sxs-lookup"><span data-stu-id="7dca3-144">hello original query might have looked something like this:</span></span>

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

<span data-ttu-id="7dca3-145">Étant donné que l’entrepôt de données SQL ne prend pas en charge ANSI joint Bonjour `FROM` clause d’une `UPDATE` instruction, vous ne pouvez pas copier ce code sur sans quelques modifications apportées.</span><span class="sxs-lookup"><span data-stu-id="7dca3-145">Since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="7dca3-146">Vous pouvez utiliser une combinaison d’un `CTAS` et implicite joindre tooreplace ce code :</span><span class="sxs-lookup"><span data-stu-id="7dca3-146">You can use a combination of a `CTAS` and an implicit join tooreplace this code:</span></span>

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

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="7dca3-147">Remplacement de jointures ANSI pour les instructions de suppression</span><span class="sxs-lookup"><span data-stu-id="7dca3-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="7dca3-148">Hello meilleure approche pour la suppression des données est parfois toouse `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="7dca3-148">Sometimes hello best approach for deleting data is toouse `CTAS`.</span></span> <span data-ttu-id="7dca3-149">Plutôt que la suppression des données hello sélectionnez simplement les données hello tookeep.</span><span class="sxs-lookup"><span data-stu-id="7dca3-149">Rather than deleting hello data simply select hello data you want tookeep.</span></span> <span data-ttu-id="7dca3-150">Cette particulièrement vrai pour `DELETE` instructions qui utilisent ansi rejoindre la syntaxe SQL Data Warehouse ne prenant pas en charge les jointures ANSI Bonjour `FROM` clause d’un `DELETE` instruction.</span><span class="sxs-lookup"><span data-stu-id="7dca3-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="7dca3-151">Voici un exemple d’instruction DELETE convertie :</span><span class="sxs-lookup"><span data-stu-id="7dca3-151">An example of a converted DELETE statement is available below:</span></span>

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

## <a name="replace-merge-statements"></a><span data-ttu-id="7dca3-152">Remplacement d’instructions MERGE</span><span class="sxs-lookup"><span data-stu-id="7dca3-152">Replace merge statements</span></span>
<span data-ttu-id="7dca3-153">Vous pouvez remplacer les instructions MERGE, du moins partiellement, à l’aide de `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="7dca3-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="7dca3-154">Vous pouvez consolider hello `INSERT` et hello `UPDATE` dans une instruction unique.</span><span class="sxs-lookup"><span data-stu-id="7dca3-154">You can consolidate hello `INSERT` and hello `UPDATE` into a single statement.</span></span> <span data-ttu-id="7dca3-155">Tous les enregistrements supprimés faudrait toobe clôturé dans une deuxième instruction.</span><span class="sxs-lookup"><span data-stu-id="7dca3-155">Any deleted records would need toobe closed off in a second statement.</span></span>

<span data-ttu-id="7dca3-156">Voici un exemple d’utilisation d’une instruction consolidée `UPSERT` :</span><span class="sxs-lookup"><span data-stu-id="7dca3-156">An example of an `UPSERT` is available below:</span></span>

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

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="7dca3-157">Recommandation CTAS : déclarer explicitement le type de données et la possibilité de valeur NULL de la sortie</span><span class="sxs-lookup"><span data-stu-id="7dca3-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="7dca3-158">Lorsque vous procédez à la migration de votre code, vous pouvez constater que vous exécutez le type de modèle de codage suivant :</span><span class="sxs-lookup"><span data-stu-id="7dca3-158">When migrating code you might find you run across this type of coding pattern:</span></span>

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

<span data-ttu-id="7dca3-159">Instinctivement, vous pouvez considérer ce tooa code SACT, vous devez migrer et vous serait correcte.</span><span class="sxs-lookup"><span data-stu-id="7dca3-159">Instinctively you might think you should migrate this code tooa CTAS and you would be correct.</span></span> <span data-ttu-id="7dca3-160">Toutefois, un problème se dissimule derrière ce scénario.</span><span class="sxs-lookup"><span data-stu-id="7dca3-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="7dca3-161">Hello de code suivant ne génère pas hello même résultat :</span><span class="sxs-lookup"><span data-stu-id="7dca3-161">hello following code does NOT yield hello same result:</span></span>

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

<span data-ttu-id="7dca3-162">Notez que hello colonne « result » comporte des valeurs de type et la possibilité de valeur null de données d’expression de hello hello vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="7dca3-162">Notice that hello column "result" carries forward hello data type and nullability values of hello expression.</span></span> <span data-ttu-id="7dca3-163">Cela peut entraîner des écarts de toosubtle dans les valeurs si vous ne faites pas attention.</span><span class="sxs-lookup"><span data-stu-id="7dca3-163">This can lead toosubtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="7dca3-164">Essayez les opérations suivantes de hello par exemple :</span><span class="sxs-lookup"><span data-stu-id="7dca3-164">Try hello following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="7dca3-165">valeur Hello stocké pour le résultat est différent.</span><span class="sxs-lookup"><span data-stu-id="7dca3-165">hello value stored for result is different.</span></span> <span data-ttu-id="7dca3-166">Comme une valeur persistante dans la colonne de résultats hello hello est utilisée dans d’autres erreurs de hello expressions devient encore plus important.</span><span class="sxs-lookup"><span data-stu-id="7dca3-166">As hello persisted value in hello result column is used in other expressions hello error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="7dca3-167">Ceci se révèle particulièrement important dans le cas des migrations de données.</span><span class="sxs-lookup"><span data-stu-id="7dca3-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="7dca3-168">Même si la requête de deuxième hello est sans doute plus précis, il existe un problème.</span><span class="sxs-lookup"><span data-stu-id="7dca3-168">Even though hello second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="7dca3-169">les données de salutation serait système de source toohello comparés différentes et qui conduit tooquestions d’intégrité dans la migration hello.</span><span class="sxs-lookup"><span data-stu-id="7dca3-169">hello data would be different compared toohello source system and that leads tooquestions of integrity in hello migration.</span></span> <span data-ttu-id="7dca3-170">Il s’agit d’une des ces rares cas où une réponse « incorrecte » hello est réellement hello droite !</span><span class="sxs-lookup"><span data-stu-id="7dca3-170">This is one of those rare cases where hello "wrong" answer is actually hello right one!</span></span>

<span data-ttu-id="7dca3-171">Hello raison pour laquelle nous voir cette disparité entre les résultats de deux de hello est arrêté tooimplicit cast de type.</span><span class="sxs-lookup"><span data-stu-id="7dca3-171">hello reason we see this disparity between hello two results is down tooimplicit type casting.</span></span> <span data-ttu-id="7dca3-172">Bonjour premier exemple de table hello définit la définition de colonne hello.</span><span class="sxs-lookup"><span data-stu-id="7dca3-172">In hello first example hello table defines hello column definition.</span></span> <span data-ttu-id="7dca3-173">Lors de la ligne de hello est insérée une conversion de type implicite se produit.</span><span class="sxs-lookup"><span data-stu-id="7dca3-173">When hello row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="7dca3-174">Dans le deuxième exemple de hello n’existe aucune conversion de type implicite comme expression de hello définit le type de données de colonne de hello.</span><span class="sxs-lookup"><span data-stu-id="7dca3-174">In hello second example there is no implicit type conversion as hello expression defines data type of hello column.</span></span> <span data-ttu-id="7dca3-175">Notez que également que la colonne hello hello deuxième exemple a été définie comme une colonne acceptant les valeurs NULL alors que dans le premier exemple de hello il n’a pas.</span><span class="sxs-lookup"><span data-stu-id="7dca3-175">Notice also that hello column in hello second example has been defined as a NULLable column whereas in hello first example it has not.</span></span> <span data-ttu-id="7dca3-176">Lors de la création de table de hello dans hello premier exemple colonne possibilité de valeur null a été définie explicitement.</span><span class="sxs-lookup"><span data-stu-id="7dca3-176">When hello table was created in hello first example column nullability was explicitly defined.</span></span> <span data-ttu-id="7dca3-177">Dans le deuxième exemple de hello, il était juste toohello expression et par défaut, cela se traduirait dans une définition de valeur NULL.</span><span class="sxs-lookup"><span data-stu-id="7dca3-177">In hello second example it was just left toohello expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="7dca3-178">tooresolve ces problèmes qui vous devez définir explicitement de conversion de type hello et la possibilité de valeur NULL dans hello `SELECT` partie Hello `CTAS` instruction.</span><span class="sxs-lookup"><span data-stu-id="7dca3-178">tooresolve these issues you must explicitly set hello type conversion and nullability in hello `SELECT` portion of hello `CTAS` statement.</span></span> <span data-ttu-id="7dca3-179">Vous ne pouvez pas définir ces propriétés dans hello créent la partie de la table.</span><span class="sxs-lookup"><span data-stu-id="7dca3-179">You cannot set these properties in hello create table part.</span></span>

<span data-ttu-id="7dca3-180">exemple Hello ci-dessous montre comment toofix hello code :</span><span class="sxs-lookup"><span data-stu-id="7dca3-180">hello example below demonstrates how toofix hello code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="7dca3-181">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="7dca3-181">Note hello following:</span></span>

* <span data-ttu-id="7dca3-182">Nous aurions pu utiliser CAST ou CONVERT.</span><span class="sxs-lookup"><span data-stu-id="7dca3-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="7dca3-183">ISNULL est utilisé tooforce COALESCE pas de valeurs null</span><span class="sxs-lookup"><span data-stu-id="7dca3-183">ISNULL is used tooforce NULLability not COALESCE</span></span>
* <span data-ttu-id="7dca3-184">ISNULL est fonction extérieur hello</span><span class="sxs-lookup"><span data-stu-id="7dca3-184">ISNULL is hello outermost function</span></span>
* <span data-ttu-id="7dca3-185">Hello deuxième partie de hello ISNULL est une constante c'est-à-dire 0</span><span class="sxs-lookup"><span data-stu-id="7dca3-185">hello second part of hello ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="7dca3-186">Pour toobe de possibilité de valeur null hello correctement défini est vital toouse `ISNULL` et non `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="7dca3-186">For hello nullability toobe correctly set it is vital toouse `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="7dca3-187">`COALESCE`n’est pas une fonction déterministe et donc hello résultat d’expression de hello sera toujours NULLable.</span><span class="sxs-lookup"><span data-stu-id="7dca3-187">`COALESCE` is not a deterministic function and so hello result of hello expression will always be NULLable.</span></span> <span data-ttu-id="7dca3-188">`ISNULL` est différent.</span><span class="sxs-lookup"><span data-stu-id="7dca3-188">`ISNULL` is different.</span></span> <span data-ttu-id="7dca3-189">Cette fonction est déterministe.</span><span class="sxs-lookup"><span data-stu-id="7dca3-189">It is deterministic.</span></span> <span data-ttu-id="7dca3-190">Par conséquent, lorsque hello deuxième partie de hello `ISNULL` fonction est une constante ou un littéral, valeur obtenue de hello est non NULL.</span><span class="sxs-lookup"><span data-stu-id="7dca3-190">Therefore when hello second part of hello `ISNULL` function is a constant or a literal then hello resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="7dca3-191">Ce Conseil n’est pas seulement utile pour garantir l’intégrité de hello de vos calculs.</span><span class="sxs-lookup"><span data-stu-id="7dca3-191">This tip is not just useful for ensuring hello integrity of your calculations.</span></span> <span data-ttu-id="7dca3-192">Il est également important dans le cadre du basculement de partition de table.</span><span class="sxs-lookup"><span data-stu-id="7dca3-192">It is also important for table partition switching.</span></span> <span data-ttu-id="7dca3-193">Imaginons que vous ayez défini la table suivante :</span><span class="sxs-lookup"><span data-stu-id="7dca3-193">Imagine you have this table defined as your fact:</span></span>

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

<span data-ttu-id="7dca3-194">Toutefois, le champ de valeur hello est une expression calculée, il n’est pas partie de la source de données hello.</span><span class="sxs-lookup"><span data-stu-id="7dca3-194">However, hello value field is a calculated expression it is not part of hello source data.</span></span>

<span data-ttu-id="7dca3-195">toocreate votre jeu de données partitionnée que vous pourriez toodo cela :</span><span class="sxs-lookup"><span data-stu-id="7dca3-195">toocreate your partitioned dataset you might want toodo this:</span></span>

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

<span data-ttu-id="7dca3-196">requête de Hello s’exécute parfaitement.</span><span class="sxs-lookup"><span data-stu-id="7dca3-196">hello query would run perfectly fine.</span></span> <span data-ttu-id="7dca3-197">problème de Hello est fourni lorsque vous essayez de basculement de partition tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="7dca3-197">hello problem comes when you try tooperform hello partition switch.</span></span> <span data-ttu-id="7dca3-198">les définitions de table Hello ne correspondent pas.</span><span class="sxs-lookup"><span data-stu-id="7dca3-198">hello table definitions do not match.</span></span> <span data-ttu-id="7dca3-199">définitions de table toomake hello correspond à hello que SACT doit toobe modifié.</span><span class="sxs-lookup"><span data-stu-id="7dca3-199">toomake hello table definitions match hello CTAS needs toobe modified.</span></span>

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

<span data-ttu-id="7dca3-200">Vous pouvez alors constater que la cohérence des types et le maintien des propriétés de possibilité de valeur Null sur une instruction CTAS constituent des approches d’ingénierie judicieuses.</span><span class="sxs-lookup"><span data-stu-id="7dca3-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="7dca3-201">Il permet l’intégrité des toomaintain dans vos calculs et garantit également que le basculement de partition est possible.</span><span class="sxs-lookup"><span data-stu-id="7dca3-201">It helps toomaintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="7dca3-202">Pour plus d’informations sur l’utilisation, consultez tooMSDN [SACT][CTAS].</span><span class="sxs-lookup"><span data-stu-id="7dca3-202">Please refer tooMSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="7dca3-203">Il est une des instructions plus importantes de hello dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7dca3-203">It is one of hello most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="7dca3-204">Vous devez donc faire en sorte d’en comprendre les moindres aspects.</span><span class="sxs-lookup"><span data-stu-id="7dca3-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7dca3-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7dca3-205">Next steps</span></span>
<span data-ttu-id="7dca3-206">Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="7dca3-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
