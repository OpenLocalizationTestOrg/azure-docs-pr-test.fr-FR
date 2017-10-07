---
title: transactions aaaOptimizing pour SQL Data Warehouse | Documents Microsoft
description: "Meilleures pratiques sur l’écriture de mises à jour efficaces de transactions dans Azure SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 6f326f26-8a54-49df-a482-9c96a58db371
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 1a821161711db9460b7e10d3cf7ba498d711448b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a>Optimisation des transactions pour SQL Data Warehouse
Cet article explique comment toooptimize hello les performances de votre code transactionnel en limitant les risques pour les restaurations de long.

## <a name="transactions-and-logging"></a>Transactions et journalisation
Les transactions sont une composante importante d’un moteur de base de données relationnelle. SQL Data Warehouse utilise les transactions durant la modification des données. Ces transactions peuvent être explicites ou implicites. Les instructions uniques `INSERT`, `UPDATE` et `DELETE` sont toutes des exemples de transactions implicites. Transactions explicites sont écrites explicitement par un développeur à l’aide de `BEGIN TRAN`, `COMMIT TRAN` ou `ROLLBACK TRAN` et sont généralement utilisées lorsque vous avez besoin de plusieurs instructions de modification toobe tous lié entre eux dans une unité atomique unique. 

Entrepôt de données SQL Azure valide de base de données de modifications toohello à l’aide des journaux de transactions. Chaque distribution présente son propre fichier journal. Les écritures des fichiers journaux de transactions sont automatiques. Aucune configuration n’est requise. Toutefois, alors que ce processus garantit l’écriture de hello, il introduit une surcharge dans le système de hello. Pour réduire des effets, vous pouvez écrire du code efficace sur le plan transactionnel. Ce type de code se classe principalement en deux catégories.

* Valorisez des structures minimalistes de journalisation, dans la mesure du possible.
* Traitement des données à l’aide d’une étendue singulier tooavoid de lots longues transactions
* Adopter une modèle pour tooa modifications volumineux une partition donnée du basculement de partition

## <a name="minimal-vs-full-logging"></a>Journalisation minimale et journalisation complète
Contrairement aux opérations entièrement journalisées, qui utilisent hello transaction journal tookeep le suivi de chaque modification de ligne, les opérations journalisées minimales effectuer le suivi des allocations des extensions et des modifications de métadonnées uniquement. Par conséquent, la journalisation minimale implique de ne journaliser que les informations de hello toorollback requis hello transaction les événements hello d’une panne ou demande explicite (`ROLLBACK TRAN`). Comme beaucoup moins les informations sont suivies dans le journal des transactions hello, une opération journalisée minimale plus performant qu’une opération entièrement journalisée taille similaire. En outre, étant donné que moins d’écritures passent le journal des transactions hello, une plus petite quantité de données de journal est générée et est donc d’e/s plus efficace.

limites de sécurité de transaction Hello s’appliquent uniquement à des opérations de toofully connecté.

> [!NOTE]
> Les opérations faisant l’objet d’une journalisation minimale peuvent prendre part à des transactions explicites. Toutes les modifications apportées aux structures d’allocation sont suivies, il est possible tooroll arrière minimale opérations journalisées. Il est important de toounderstand hello modification est « minimale » connecté qu’il n’est pas non connecté.
> 
> 

## <a name="minimally-logged-operations"></a>Journalisations minimales
Hello opérations suivantes sont capables d’en cours d’une journalisation minimale :

* CREATE TABLE AS SELECT ([CTAS][CTAS])
* INSERT..SELECT
* CREATE INDEX
* ALTER INDEX REBUILD
* DROP INDEX
* TRUNCATE TABLE
* DROP TABLE
* ALTER TABLE SWITCH PARTITION

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> Opérations de déplacement de données internes (telles que `BROADCAST` et `SHUFFLE`) ne sont pas affectés par la limite de sécurité de transaction hello.
> 
> 

## <a name="minimal-logging-with-bulk-load"></a>Journalisation minimale avec chargement en bloc
`CTAS` et `INSERT...SELECT` sont des opérations de chargement en bloc. Toutefois, les deux sont influencées par la définition de la table cible hello et varient selon le scénario de charge hello. Voici un tableau détaillant les situations de journalisations minimales ou complètes des opérations de chargement en bloc :  

| Index primaire | Scénario de chargement | Mode de journalisation |
| --- | --- | --- |
| Segment de mémoire |Quelconque |**Minimal** |
| Index cluster |Table cible vide |**Minimal** |
| Index cluster |Les lignes chargées ne se chevauchent pas avec les pages existantes dans la cible. |**Minimal** |
| Index cluster |Les lignes chargées se chevauchent avec les pages existantes dans la cible. |Complet |
| Index columstore en cluster |Taille de lot >= 102 400 par distribution alignée sur la partition |**Minimal** |
| Index columstore en cluster |Taille de lot < 102 400 par distribution alignée sur la partition |Complet |

Il est important de noter que toutes les écritures tooupdate secondaire ou non cluster de l’index sera toujours entièrement les opérations journalisées.

> [!IMPORTANT]
> SQL Data Warehouse présente 60 distributions. Par conséquent, si vous en supposant que toutes les lignes sont réparties uniformément et de destination dans une seule partition, votre lot devez toocontain 6,144,000 lignes ou plus grande toobe minimale connecté lors de l’écriture tooa Index cluster Columnstore. Si hello table est partitionnée et lignes hello insérées sont réparties entre les limites de partition, vous devez 6,144,000 lignes par limite de partition en supposant que la répartition égale des données. Chaque partition de chaque point de distribution doit dépasser indépendamment hello 102 400 lignes seuil pour toobe d’insertion hello journalisée dans la distribution de hello.
> 
> 

Le chargement de données dans une table non vide avec un index cluster comporte bien souvent une combinaison de lignes ayant fait l’objet d’une journalisation minimale et complète. Un index cluster est un arbre équilibré (arbre b) de pages. Si la page de hello écrits tooalready contient des lignes à partir d’une autre transaction, ces écritures doivent être enregistrés entièrement. Toutefois, si la page de hello est vide puis page de toothat hello écriture est consignées dans le journal.

## <a name="optimizing-deletes"></a>Optimisation des suppressions
`DELETE` est une opération entièrement journalisée.  Si vous devez toodelete une grande quantité de données dans une table ou une partition, il est donc souvent plus judicieux trop`SELECT` les données de salutation que vous souhaitez tookeep, ce qui peut être exécutée en tant qu’une opération journalisée minimale.  tooaccomplish, créez une nouvelle table avec [SACT][CTAS].  Une fois créé, utilisez [renommer] [ RENAME] tooswap votre ancienne table avec la table de hello nouvellement créé.

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only hello records we want tookep (PromotionKey 2)
CREATE TABLE [dbo].[FactInternetSales_d]
WITH
(    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
)
AS
SELECT     *
FROM     [dbo].[FactInternetSales]
WHERE    [PromotionKey] = 2
OPTION (LABEL = 'CTAS : Delete')
;

--Step 02. Rename hello Tables tooreplace hello 
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] too[FactInternetSales];
```

## <a name="optimizing-updates"></a>Optimisation des mises à jour
`UPDATE` est une opération entièrement journalisée.  Si vous avez besoin de tooupdate un grand nombre de lignes dans une table ou d’une partition souvent beaucoup plus efficace toouse une opération journalisée minimale comme [SACT] [ CTAS] toodo donc.

Bonjour exemple ci-dessous, une mise à jour complète de la table a été converti tooa `CTAS` afin que la journalisation minimale est possible.

Dans ce cas, nous avons ajouté a posteriori une vente toohello du montant remise dans la table de hello :

```sql
--Step 01. Create a new table containing hello "Update". 
CREATE TABLE [dbo].[FactInternetSales_u]
WITH
(    CLUSTERED INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
OPTION (LABEL = 'CTAS : Update')
;

--Step 02. Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] too[FactInternetSales];

--Step 03. Drop hello old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> Les fonctions de gestion des charges de travail SQL Data Warehouse peuvent faciliter la recréation des tables de grande taille. Pour plus d’informations, consultez la section de gestion de la charge de travail toohello Bonjour [concurrency] [ concurrency] l’article.
> 
> 

## <a name="optimizing-with-partition-switching"></a>Optimisation avec basculement de partitions
Quand vous devez procéder à des modifications à grande échelle au sein d’une [partition de table][table partition], il est bien plus judicieux d’adopter un modèle de basculement de partitions. Si hello modification des données est importante et étendues parvient à plusieurs partitions, puis itérer simplement les partitions hello hello même résultat.

Hello étapes tooperform un basculement de partition sont les suivantes :

1. Créer une partition vide
2. Effectuer hello « mise à jour » comme un SACT
3. Hello toohello de données existantes à la table d’extraction
4. Insérer des données de nouveau hello
5. Nettoyer les données de hello

Cependant, toohelp identifier tooswitch de partitions hello nous devez abord toobuild une procédure d’assistance tels que hello un ci-dessous. 

```sql
CREATE PROCEDURE dbo.partition_data_get
    @schema_name           NVARCHAR(128)
,    @table_name               NVARCHAR(128)
,    @boundary_value           INT
AS
IF OBJECT_ID('tempdb..#ptn_data') IS NOT NULL
BEGIN
    DROP TABLE #ptn_data
END
CREATE TABLE #ptn_data
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
WITH CTE
AS
(
SELECT     s.name                            AS [schema_name]
,        t.name                            AS [table_name]
,         p.partition_number                AS [ptn_nmbr]
,        p.[rows]                        AS [ptn_rows]
,        CAST(r.[value] AS INT)            AS [boundary_value]
FROM        sys.schemas                    AS s
JOIN        sys.tables                    AS t    ON  s.[schema_id]        = t.[schema_id]
JOIN        sys.indexes                    AS i    ON     t.[object_id]        = i.[object_id]
JOIN        sys.partitions                AS p    ON     i.[object_id]        = p.[object_id] 
                                                AND i.[index_id]        = p.[index_id] 
JOIN        sys.partition_schemes        AS h    ON     i.[data_space_id]    = h.[data_space_id]
JOIN        sys.partition_functions        AS f    ON     h.[function_id]        = f.[function_id]
LEFT JOIN    sys.partition_range_values    AS r     ON     f.[function_id]        = r.[function_id] 
                                                AND r.[boundary_id]        = p.[partition_number]
WHERE i.[index_id] <= 1
)
SELECT    *
FROM    CTE
WHERE    [schema_name]        = @schema_name
AND        [table_name]        = @table_name
AND        [boundary_value]    = @boundary_value
OPTION (LABEL = 'dbo.partition_data_get : CTAS : #ptn_data')
;
GO
```

Cette procédure optimise la réutilisation de code et conserve exemple plus compacte du basculement de partition hello.

code Hello ci-dessous montre cinq étapes de hello mentionnés ci-dessus tooachieve une routine du basculement de partition complète.

```sql
--Create a partitioned aligned empty table tooswitch out hello data 
IF OBJECT_ID('[dbo].[FactInternetSales_out]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_out]
END

CREATE TABLE [dbo].[FactInternetSales_out]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE 1=2
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Create a partitioned aligned table and update hello data in hello select portion of hello CTAS
IF OBJECT_ID('[dbo].[FactInternetSales_in]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_in]
END

CREATE TABLE [dbo].[FactInternetSales_in]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
WHERE    OrderDateKey BETWEEN 20020101 AND 20021231
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Use hello helper procedure tooidentify hello partitions
--hello source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--hello "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--hello "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch hello partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' too[dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' too[dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform hello clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a>Minimiser la journalisation avec des lots de petite taille
Pour les opérations de modification de données de grande taille, il peut être judicieux toodivide hello opération en unité de hello tooscope segments ou des lots de travail.

Vous trouverez ci-dessous un exemple de travail. taille de lot Hello a été défini tooa trivial technique hello numéro toohighlight. En réalité, taille de lot hello serait beaucoup plus important. 

```sql
SET NO_COUNT ON;
IF OBJECT_ID('tempdb..#t') IS NOT NULL
BEGIN
    DROP TABLE #t;
    PRINT '#t dropped';
END

CREATE TABLE #t
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
SELECT    ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS seq_nmbr
,        SalesOrderNumber
,        SalesOrderLineNumber
FROM    dbo.FactInternetSales
WHERE    [OrderDateKey] BETWEEN 20010101 and 20011231
;

DECLARE    @seq_start        INT = 1
,        @batch_iterator    INT = 1
,        @batch_size        INT = 50
,        @max_seq_nmbr    INT = (SELECT MAX(seq_nmbr) FROM dbo.#t)
;

DECLARE    @batch_count    INT = (SELECT CEILING((@max_seq_nmbr*1.0)/@batch_size))
,        @seq_end        INT = @batch_size
;

SELECT COUNT(*)
FROM    dbo.FactInternetSales f

PRINT 'MAX_seq_nmbr '+CAST(@max_seq_nmbr AS VARCHAR(20))
PRINT 'MAX_Batch_count '+CAST(@batch_count AS VARCHAR(20))

WHILE    @batch_iterator <= @batch_count
BEGIN
    DELETE
    FROM    dbo.FactInternetSales
    WHERE EXISTS
    (
            SELECT    1
            FROM    #t t
            WHERE    seq_nmbr BETWEEN  @seq_start AND @seq_end
            AND        FactInternetSales.SalesOrderNumber        = t.SalesOrderNumber
            AND        FactInternetSales.SalesOrderLineNumber    = t.SalesOrderLineNumber
    )
    ;

    SET @seq_start = @seq_end
    SET @seq_end = (@seq_start+@batch_size);
    SET @batch_iterator +=1;
END
```

## <a name="pause-and-scaling-guidance"></a>Conseils sur la suspension et la mise à l’échelle
Azure SQL Data Warehouse vous permet de suspendre, de reprendre et de mettre à l’échelle à la demande votre entrepôt de données. Lorsque vous suspendez ou mettre à l’échelle de votre entrepôt de données SQL qu’il est important toounderstand que toutes les transactions en cours sont terminent immédiatement ; à l’origine de toutes les transactions en cours de toobe restaurée. Si votre charge de travail avait émis un long terme et la modification des données incomplètes antérieure toohello pause ou la mise à échelle, puis ce travail devez toobe annulée. Cela peut avoir un impact sur les temps de hello que toopause nécessaire ou mettre à l’échelle de votre base de données Azure SQL Data Warehouse. 

> [!IMPORTANT]
> `UPDATE` et `DELETE` correspondant toutes deux à des journalisations complètes, ces opérations d’annulation et de rétablissement peuvent nécessiter un délai considérablement plus important que des journalisations minimales de taille équivalente. 
> 
> 

scénario de meilleures Hello est toolet dans les transactions complètes vol données modification précédente toopausing ou mise à l’échelle SQL Data Warehouse. Toutefois, cela n’est pas toujours pratique. risque de hello toomitigate une restauration longue, envisagez une des options suivantes de hello :

* Réécrire les opérations de longue durée à l’aide de [CTAS][CTAS]
* Opération de hello se répartissent en plusieurs segments ; fonctionne sur un sous-ensemble de lignes de hello

## <a name="next-steps"></a>Étapes suivantes
Consultez [Transactions dans SQL Data Warehouse] [ Transactions in SQL Data Warehouse] toolearn plus d’informations sur les niveaux d’isolement et limites transactionnelles.  Pour une vue d’ensemble des autres bonnes pratiques, consultez [Bonnes pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Transactions in SQL Data Warehouse]: ./sql-data-warehouse-develop-transactions.md
[table partition]: ./sql-data-warehouse-tables-partition.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[alter index]:https://msdn.microsoft.com/library/ms188388.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx

<!-- Other web references -->

