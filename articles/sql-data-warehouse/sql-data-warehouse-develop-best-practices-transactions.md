---
title: Optimisation des transactions pour SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: f9f19d75a37351b3562ce8c2f3629df14c5437c6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a>Optimisation des transactions pour SQL Data Warehouse
Cet article vous explique comment optimiser les performances de votre code transactionnel tout en limitant les risques de restaurations de longue durée.

## <a name="transactions-and-logging"></a>Transactions et journalisation
Les transactions sont une composante importante d’un moteur de base de données relationnelle. SQL Data Warehouse utilise les transactions durant la modification des données. Ces transactions peuvent être explicites ou implicites. Les instructions uniques `INSERT`, `UPDATE` et `DELETE` sont toutes des exemples de transactions implicites. Les transactions explicites sont écrites de manière explicite par un développeur à l’aide de `BEGIN TRAN`, `COMMIT TRAN` ou `ROLLBACK TRAN`. Généralement, elles sont utilisées dans les situations où plusieurs instructions de modification doivent être liées dans une seule unité atomique. 

Azure SQL Data Warehouse valide les modifications apportées à la base de données à l’aide de fichiers journaux de transactions. Chaque distribution présente son propre fichier journal. Les écritures des fichiers journaux de transactions sont automatiques. Aucune configuration n’est requise. Notez toutefois que ce processus, qui garantit l’écriture, introduit par ailleurs une surcharge dans le système. Pour réduire des effets, vous pouvez écrire du code efficace sur le plan transactionnel. Ce type de code se classe principalement en deux catégories.

* Valorisez des structures minimalistes de journalisation, dans la mesure du possible.
* Traitez les données en les regroupant par lots définis, afin d’éviter les transactions isolées de longue durée.
* Adoptez un modèle de basculement de partitions en cas de modifications importantes apportées à une partition donnée.

## <a name="minimal-vs-full-logging"></a>Journalisation minimale et journalisation complète
Contrairement aux opérations entièrement journalisées, qui utilisent le fichier journal de transactions pour effectuer le suivi de chaque modification de ligne, les journalisations minimales assurent le suivi des allocations d’étendue et des modifications de métadonnées uniquement. Par conséquent, la journalisation minimale implique la consignation exclusive des informations nécessaires à la restauration de la transaction en cas de défaillance ou de requête explicite (`ROLLBACK TRAN`). Dans la mesure où la journalisation minimale implique le suivi d’un volume de données moins important, cette opération est plus performante qu’une journalisation complète de taille similaire. En outre, un volume moins important d’écritures étant transmis vers le fichier journal de transactions, la quantité de données de journal générées est elle aussi réduite, et les performances E/S s’en trouvent accrues.

Les limites de sécurité des transactions s’appliquent uniquement aux opérations faisant l’objet d’une journalisation complète.

> [!NOTE]
> Les opérations faisant l’objet d’une journalisation minimale peuvent prendre part à des transactions explicites. Comme toutes les modifications des structures d’allocations font l’objet d’un suivi, il est possible de restaurer les journalisations minimales. Il est important de comprendre la nuance : la modification fait bien l’objet d’une journalisation, aussi minimale soit-elle.
> 
> 

## <a name="minimally-logged-operations"></a>Journalisations minimales
Les opérations suivantes peuvent faire l’objet d’une journalisation minimale :

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
> Les opérations de déplacement de données internes (telles que `BROADCAST` et `SHUFFLE`) ne sont pas affectées par la limite de sécurité des transactions.
> 
> 

## <a name="minimal-logging-with-bulk-load"></a>Journalisation minimale avec chargement en bloc
`CTAS` et `INSERT...SELECT` sont des opérations de chargement en bloc. Toutefois, ces deux éléments sont affectés par la définition de table cible et dépendent du scénario de chargement. Voici un tableau détaillant les situations de journalisations minimales ou complètes des opérations de chargement en bloc :  

| Index primaire | Scénario de chargement | Mode de journalisation |
| --- | --- | --- |
| Segment de mémoire |Quelconque |**Minimal** |
| Index cluster |Table cible vide |**Minimal** |
| Index cluster |Les lignes chargées ne se chevauchent pas avec les pages existantes dans la cible. |**Minimal** |
| Index cluster |Les lignes chargées se chevauchent avec les pages existantes dans la cible. |Complet |
| Index columstore en cluster |Taille de lot >= 102 400 par distribution alignée sur la partition |**Minimal** |
| Index columstore en cluster |Taille de lot < 102 400 par distribution alignée sur la partition |Complet |

Il est important de noter que toute opération d’écriture effectuée dans le cadre d’une mise à jour d’index secondaires ou non cluster correspond à une journalisation complète.

> [!IMPORTANT]
> SQL Data Warehouse présente 60 distributions. Par conséquent, en partant du principe que l’ensemble des lignes sont distribuées équitablement et placées dans une partition unique, votre lot devra comporter 6 144 000 lots ou plus pour faire l’objet d’une journalisation minimale lors d’une écriture vers un index columstore en cluster. Si la table est partitionnée et que les lignes insérées dépassent les limites de la partition, il vous faudra 6 144 000 lignes par limite de partition, pour une distribution uniforme des données. Dans chaque distribution, l’ensemble des partitions doivent isolément dépasser le seuil de 102 400 lignes pour que l’insertion fasse l’objet d’une journalisation minimale dans la distribution.
> 
> 

Le chargement de données dans une table non vide avec un index cluster comporte bien souvent une combinaison de lignes ayant fait l’objet d’une journalisation minimale et complète. Un index cluster est un arbre équilibré (arbre b) de pages. Si la page cible de l’écriture comporte déjà des lignes d’une autre transaction, ces opérations d’écriture feront l’objet d’une journalisation complète. Toutefois, si la page est vide, l’opération d’écriture fera l’objet d’une journalisation minimale.

## <a name="optimizing-deletes"></a>Optimisation des suppressions
`DELETE` est une opération entièrement journalisée.  Si vous avez besoin de supprimer un volume important de données dans une table ou une partition, il est souvent plus judicieux d’appliquer une opération `SELECT` aux données que vous souhaitez conserver, qui peut être exécutée en tant qu’opération de journalisation minimale.  Pour ce faire, créez une table avec [CTAS][CTAS].  Une fois la table créée, utilisez [RENAME][RENAME] pour permuter l’ancienne table et la table nouvellement créée.

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only the records we want to kep (PromotionKey 2)
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

--Step 02. Rename the Tables to replace the 
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] TO [FactInternetSales];
```

## <a name="optimizing-updates"></a>Optimisation des mises à jour
`UPDATE` est une opération entièrement journalisée.  SI vous devez mettre à jour un nombre important de lignes d’une table ou d’une partition, il peut souvent s’avérer plus efficace de recourir à une opération avec une journalisation minimale, comme [CTAS][CTAS].

Dans l’exemple suivant, une mise à jour complète de table a été convertie en `CTAS` , ce qui rend possible la mise en place d’une journalisation minimale.

Dans ce cas, nous ajoutons a posteriori une valeur de remise aux ventes dans la table :

```sql
--Step 01. Create a new table containing the "Update". 
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

--Step 02. Rename the tables
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] TO [FactInternetSales];

--Step 03. Drop the old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> Les fonctions de gestion des charges de travail SQL Data Warehouse peuvent faciliter la recréation des tables de grande taille. Pour plus d’informations, consultez la section relative à la gestion des charges de travail, dans l’article sur [l’accès concurrentiel][concurrency].
> 
> 

## <a name="optimizing-with-partition-switching"></a>Optimisation avec basculement de partitions
Quand vous devez procéder à des modifications à grande échelle au sein d’une [partition de table][table partition], il est bien plus judicieux d’adopter un modèle de basculement de partitions. Si la modification de données est considérable et relative à plusieurs partitions, vous obtiendrez un résultat identique en effectuant une itération sur les partitions.

Les étapes constitutives d’un basculement de partitions sont les suivantes :

1. Créer une partition vide
2. Effectuez la mise à jour en tant que CTAS
3. Extraire les données existantes vers la table cible
4. Basculer les nouvelles données
5. Nettoyer les données

Toutefois, pour faciliter l’identification des partitions à basculer, nous devons dans un premier temps générer une procédure d’assistance, semblable à celle ci-dessous. 

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

Cette procédure optimise la réutilisation du code et permet de conserver un exemple de basculement de partitions plus compact.

Le code ci-dessous représente les cinq étapes mentionnées plus haut pour l’exécution d’une opération de basculement complet de partitions.

```sql
--Create a partitioned aligned empty table to switch out the data 
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

--Create a partitioned aligned table and update the data in the select portion of the CTAS
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

--Use the helper procedure to identify the partitions
--The source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--The "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--The "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch the partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' TO [dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' TO [dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform the clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a>Minimiser la journalisation avec des lots de petite taille
Pour les opérations de grande envergure de modifications de données, il peut s’avérer judicieux de diviser l’activité en segments ou lots afin de répartir la charge de travail.

Vous trouverez ci-dessous un exemple de travail. La taille du lot a été définie sur un nombre insignifiant, ceci pour mettre en évidence la technique. Dans la réalité, la taille du lot serait bien plus importante. 

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
Azure SQL Data Warehouse vous permet de suspendre, de reprendre et de mettre à l’échelle à la demande votre entrepôt de données. Lorsque vous suspendez ou mettez à l’échelle votre instance SQL Data Warehouse, il est important de comprendre que l’ensemble des transactions en cours sont immédiatement arrêtées ; toute transaction ouverte est restaurée. Si votre charge de travail a émis une modification de données incomplète et de longue durée avant l’opération de suspension ou de mise à l’échelle, cette tâche devra être annulée. Cela peut avoir une incidence sur le délai nécessaire à la suspension ou à la mise à jour de votre base de données Azure SQL Data Warehouse. 

> [!IMPORTANT]
> `UPDATE` et `DELETE` correspondant toutes deux à des journalisations complètes, ces opérations d’annulation et de rétablissement peuvent nécessiter un délai considérablement plus important que des journalisations minimales de taille équivalente. 
> 
> 

La configuration idéale consiste à laisser les modifications en cours de données se terminer avant la suspension ou la mise à l’échelle de SQL Data Warehouse. Toutefois, cela n’est pas toujours pratique. Pour pallier le risque d’une longue restauration, envisagez l’une des options suivantes :

* Réécrire les opérations de longue durée à l’aide de [CTAS][CTAS]
* Décomposer l’opération en segments, en traitant un sous-ensemble des lignes

## <a name="next-steps"></a>Étapes suivantes
Consultez [Transactions dans SQL Data Warehouse][Transactions in SQL Data Warehouse] pour en savoir plus sur les niveaux d’isolement et les limites transactionnelles.  Pour une vue d’ensemble des autres bonnes pratiques, consultez [Bonnes pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices].

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

