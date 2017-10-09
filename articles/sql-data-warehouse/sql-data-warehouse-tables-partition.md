---
title: tables aaaPartitioning SQL Data Warehouse | Documents Microsoft
description: Prise en main du partitionnement de tables dans Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 6cef870c-114f-470c-af10-02300c58885d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: aa63c51562f3e6f83063320860b195e135a721e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a>Partitionnement de tables dans SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Vue d’ensemble][Overview]
> * [Types de données][Data Types]
> * [Distribuer][Distribute]
> * [Index][Index]
> * [Partition][Partition]
> * [Statistiques][Statistics]
> * [Temporaire][Temporary]
> 
> 

Le partitionnement est pris en charge sur tous les types de table SQL Data Warehouse, notamment columnstore en cluster, index en cluster et segment de mémoire.  Le partitionnement est également pris en charge sur tous les types de distribution, notamment le hachage ou le tourniquet (round robin) distribué.  Il permet de toodivide vos données en groupes plus petits de données et dans la plupart des cas, le partitionnement sont effectuées sur une colonne de date.

## <a name="benefits-of-partitioning"></a>Avantages du partitionnement
Le partitionnement peut bénéficier de la maintenance des données et des performances des requêtes.  Si il tire parti à la fois ou une seule est dépendante de la façon dont les données sont chargées et si hello même colonne peut être utilisé pour les deux cas, étant donné que le partitionnement peut uniquement être effectué sur une colonne.

### <a name="benefits-tooloads"></a>Avantages tooloads
le principal avantage de Hello du partitionnement dans l’entrepôt de données SQL est améliorer l’efficacité de hello et les performances de chargement des données à l’aide de la suppression de la partition, en basculant et la fusion.  Dans la plupart des cas, les données sont partitionnées sur une date de colonne qui est étroitement liée séquence toohello quelles données hello sont chargé toohello de base de données.  Un des avantages de plus grand hello d’à l’aide de données des partitions toomaintain il hello évitement de journalisation des transactions.  Tout simplement d’insertion, de mise à jour ou de suppression de données soient l’approche la plus simple hello, avec un peu de réflexion et d’efforts, à l’aide du partitionnement pendant le processus de chargement peut considérablement améliorer les performances.

Basculement de partition peut être utilisé tooquickly supprimer ou remplacer une section d’une table.  Par exemple, une table de faits de ventes peut contenir seulement les données pour hello derniers mois 36.  À fin hello de chaque mois, hello mois plus anciens des données de vente est supprimé à partir de la table de hello.  Ces données pu être supprimées en utilisant des données delete instruction toodelete hello pour hello mois plus ancien.  Toutefois, la suppression d’une grande quantité de données en ligne avec une instruction delete peut prendre beaucoup de temps, ainsi que créer risque hello des transactions volumineuses, ce qui peut prendre un certain temps toorollback si une erreur survient.  Une approche plus optimale est toosimply dépôt hello partition la plus ancienne des données.  Où la suppression des lignes individuelles hello plusieurs heures, la suppression d’une partition complète peut prendre des secondes.

### <a name="benefits-tooqueries"></a>Avantages tooqueries
Le partitionnement peut être également les performances des requêtes tooimprove utilisé.  Si une requête qui applique un filtre sur une colonne partitionnée, cela peut limiter Bonjour analyse tooonly Bonjour qualification des partitions qui peuvent être un beaucoup plus petit sous-ensemble de données hello, en évitant une analyse complète.  Avec l’introduction de hello des index columnstore en cluster, des gains de performance élimination prédicat hello sont moins utile, mais dans certains cas, il peut être un tooqueries avantage.  Par exemple, si la table de faits de ventes hello est partitionnée en 36 mois à l’aide du champ de date de vente hello, puis requêtes filtrer sur la date de vente hello peuvent doit effectuer des recherches dans les partitions ne correspondent pas aux filtres de hello.

## <a name="partition-sizing-guidance"></a>Guide de dimensionnement de partition
Lors de la partition peut être utilisé tooimprove performances certains scénarios, la création d’une table avec **trop** partitions peuvent nuire aux performances dans certaines circonstances.  Ces inquiétudes sont particulièrement avérées pour les tables columnstore en cluster.  Pour le partitionnement toobe utile, il est important toounderstand lorsque toouse de partitionnement et de hello le nombre de partitions toocreate.  Il est aucune règle dur rapide comme toohow le nombre de partitions est trop nombreux, il dépend de vos données et le nombre de partitions vous chargez toosimultaneously.  Mais en règle générale, envisager l’ajout de 10 s too100s de partitions, pas pour 1 000.

Lors de la création de partitionnement sur **columnstore cluster** tables, il est important tooconsider obtiendrons ainsi le nombre de lignes dans chaque partition.  Pour une compression et des performances des tables columnstore en cluster optimales, un minimum de 1 million de lignes par partition et par distribution est nécessaire.  Avant la création des partitions, SQL Data Warehouse divise déjà chaque table en 60 bases de données distribuées.  N’importe quelle table ajoutée tooa partitionnement est en plus des distributions toohello créées coulisses hello.  À l’aide de cet exemple, si table de faits de ventes hello contenus des partitions mensuelles 36, étant donné que l’entrepôt de données SQL a des distributions de 60, puis hello faits de ventes table doit contenir des millions de 60 lignes par mois ou 2.1 milliards de lignes lorsque tous les mois sont remplies.  Si une table contient beaucoup moins de lignes que hello recommandé nombre minimal de lignes par partition, envisagez d’utiliser moins de partitions dans le numéro de commande toomake augmentation hello de lignes par partition.  Voir aussi hello [indexation] [ Index] article qui comprend des requêtes qui peuvent être exécutés sur SQL Data Warehouse tooassess hello de qualité des index cluster columnstore.

## <a name="syntax-difference-from-sql-server"></a>Différence de syntaxe à partir de SQL Server
SQL Data Warehouse présente une définition simplifiée de partitions qui diffère légèrement de celle de SQL Server.  Les fonctions et les schémas de partitionnement ne sont pas utilisés dans SQL Data Warehouse, car ils se trouvent dans SQL Server.  Au lieu de cela, vous devez toodo est identifier les points de limite partitionnées hello et de colonne.  Syntaxe hello de partitionnement peut être légèrement différente de SQL Server, les concepts de base hello sont hello même.  SQL Server et SQL Data Warehouse prennent en charge une colonne de partition par table, qui peut être une partition par plage.  toolearn en savoir plus sur le partitionnement, consultez [Partitioned Tables and Indexes][Partitioned Tables and Indexes].

Hello, Voici un exemple d’un entrepôt de données SQL partitionnée [CREATE TABLE] [ CREATE TABLE] instruction, partitions de table de FactInternetSales hello sur la colonne OrderDateKey de hello :

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

## <a name="migrating-partitioning-from-sql-server"></a>Migration du partitionnement dans SQL Server
toomigrate SQL Server partitionner simplement les définitions tooSQL l’entrepôt de données :

* Éliminer hello SQL Server [schéma de partition][partition scheme].
* Ajouter hello [fonction de partition] [ partition function] définition tooyour CREATE TABLE.

Si vous migrez une table partitionnée à partir d’un Bonjour d’instance de SQL Server sous SQL peut vous aider à nombre de hello toointerrogate de lignes qui se trouvent dans chaque partition.  Gardez à l’esprit que si hello même granularité de partitionnement est utilisée sur l’entrepôt de données SQL, nombre hello de lignes par partition diminue d’un facteur de 60.  

```sql
-- Partition information for a SQL Server Database
SELECT      s.[name]                        AS      [schema_name]
,           t.[name]                        AS      [table_name]
,           i.[name]                        AS      [index_name]
,           p.[partition_number]            AS      [partition_number]
,           SUM(a.[used_pages]*8.0)         AS      [partition_size_kb]
,           SUM(a.[used_pages]*8.0)/1024    AS      [partition_size_mb]
,           SUM(a.[used_pages]*8.0)/1048576 AS      [partition_size_gb]
,           p.[rows]                        AS      [partition_row_count]
,           rv.[value]                      AS      [partition_boundary_value]
,           p.[data_compression_desc]       AS      [partition_compression_desc]
FROM        sys.schemas s
JOIN        sys.tables t                    ON      t.[schema_id]         = s.[schema_id]
JOIN        sys.partitions p                ON      p.[object_id]         = t.[object_id]
JOIN        sys.allocation_units a          ON      a.[container_id]      = p.[partition_id]
JOIN        sys.indexes i                   ON      i.[object_id]         = p.[object_id]
                                            AND     i.[index_id]          = p.[index_id]
JOIN        sys.data_spaces ds              ON      ds.[data_space_id]    = i.[data_space_id]
LEFT JOIN   sys.partition_schemes ps        ON      ps.[data_space_id]    = ds.[data_space_id]
LEFT JOIN   sys.partition_functions pf      ON      pf.[function_id]      = ps.[function_id]
LEFT JOIN   sys.partition_range_values rv   ON      rv.[function_id]      = pf.[function_id]
                                            AND     rv.[boundary_id]      = p.[partition_number]
WHERE       p.[index_id] <=1
GROUP BY    s.[name]
,           t.[name]
,           i.[name]
,           p.[partition_number]
,           p.[rows]
,           rv.[value]
,           p.[data_compression_desc]
;
```

## <a name="workload-management"></a>Gestion des charges de travail
Toofactor de prendre en compte un dernier dans la décision de partition de table toohello est [gestion de la charge de travail][workload management].  Gestion de la charge de travail dans l’entrepôt de données SQL est principalement les gestion hello de mémoire et d’accès concurrentiel.  Mémoire maximale allouée distribution tooeach pendant l’exécution de requête hello de l’entrepôt de données SQL est les classes de ressource gouvernée.  Dans l’idéal, vos partitions seront redimensionnées par d’autres facteurs tels que les besoins en mémoire de la création d’index columnstore cluster hello.  Les index columnstore en cluster présentent des avantages non négligeables lorsque davantage de mémoire leur est allouée.  Par conséquent, vous pouvez tooensure reconstruction d’un index de partition n’est pas privé de la mémoire. Augmentation hello de mémoire disponible tooyour requête peut être obtenue en activant le rôle par défaut de hello, smallrc, tooone de hello autres rôles, tels que largerc.

Pour plus d’informations sur l’allocation de mémoire par distribution hello sont disponibles en interrogeant les vues de gestion dynamique de gouverneur de ressources hello. En réalité, votre allocation de mémoire sera inférieure à figures hello ci-dessous. Toutefois, cette figure peut vous aider à dimensionner vos partitions lors d’opérations de gestion des données.  Essayez tooavoid dimensionnement des partitions au-delà d’allocation de mémoire hello fourni par classe de ressource de très nombreuses hello. Si vos partitions de croître au-delà de cette illustration, vous exécutez risque hello pression sur la mémoire, ce qui à son tour entraîne la compression optimale accessible sans.

```sql
SELECT  rp.[name]                                AS [pool_name]
,       rp.[max_memory_kb]                        AS [max_memory_kb]
,       rp.[max_memory_kb]/1024                    AS [max_memory_mb]
,       rp.[max_memory_kb]/1048576                AS [mex_memory_gb]
,       rp.[max_memory_percent]                    AS [max_memory_percent]
,       wg.[name]                                AS [group_name]
,       wg.[importance]                            AS [group_importance]
,       wg.[request_max_memory_grant_percent]    AS [request_max_memory_grant_percent]
FROM    sys.dm_pdw_nodes_resource_governor_workload_groups    wg
JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools    rp ON wg.[pool_id] = rp.[pool_id]
WHERE   wg.[name] like 'SloDWGroup%'
AND     rp.[name]    = 'SloDWPool'
;
```

## <a name="partition-switching"></a>Basculement de partitions
SQL Data Warehouse prend en charge le fractionnement, la fusion et le basculement de partition. Chacune de ces fonctions est incapable d’à l’aide de hello [ALTER TABLE] [ ALTER TABLE] instruction.

partitions tooswitch entre deux tables, que vous devez vous assurer que les partitions hello s’aligner sur leurs limites respectifs et que les définitions de table hello correspondent. Comme les contraintes check ne sont pas disponibles tooenforce hello plage de valeurs dans une table de source de table hello doit contenir hello même des limites de partition en tant que la table cible hello. Si cela n’est pas le cas de hello, basculement de partition hello échouera car les métadonnées de partition hello ne seront pas synchronisées.

### <a name="how-toosplit-a-partition-that-contains-data"></a>Comment toosplit une partition qui contient des données
Bonjour toosplit méthode la plus efficace une partition qui contient déjà des données est toouse un `CTAS` instruction. Si la table partitionnée de hello est un index columnstore en cluster puis partition de table hello doit être vide avant elle peut être divisée.

Voici un exemple de table columnstore partitionnée qui inclut une ligne dans chaque partition :

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
        [ProductKey]            int          NOT NULL
    ,   [OrderDateKey]          int          NOT NULL
    ,   [CustomerKey]           int          NOT NULL
    ,   [PromotionKey]          int          NOT NULL
    ,   [SalesOrderNumber]      nvarchar(20) NOT NULL
    ,   [OrderQuantity]         smallint     NOT NULL
    ,   [UnitPrice]             money        NOT NULL
    ,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101
                    )
                )
)
;

INSERT INTO dbo.FactInternetSales
VALUES (1,19990101,1,1,1,1,1,1);
INSERT INTO dbo.FactInternetSales
VALUES (1,20000101,1,1,1,1,1,1);


CREATE STATISTICS Stat_dbo_FactInternetSales_OrderDateKey ON dbo.FactInternetSales(OrderDateKey);
```

> [!NOTE]
> Par objet de statistiques création hello, nous nous assurons que ces métadonnées de table sont plus précises. Si ces statistiques ne sont pas créées, SQL Data Warehouse utilise les valeurs par défaut. Pour en savoir plus sur les statistiques, consultez la rubrique [Statistiques][statistics].
> 
> 

Nous pouvons ensuite interroger pour le nombre de lignes hello à l’aide de hello `sys.partitions` affichage catalogue :

```sql
SELECT  QUOTENAME(s.[name])+'.'+QUOTENAME(t.[name]) as Table_name
,       i.[name] as Index_name
,       p.partition_number as Partition_nmbr
,       p.[rows] as Row_count
,       p.[data_compression_desc] as Data_Compression_desc
FROM    sys.partitions p
JOIN    sys.tables     t    ON    p.[object_id]   = t.[object_id]
JOIN    sys.schemas    s    ON    t.[schema_id]   = s.[schema_id]
JOIN    sys.indexes    i    ON    p.[object_id]   = i.[object_Id]
                            AND   p.[index_Id]    = i.[index_Id]
WHERE t.[name] = 'FactInternetSales'
;
```

Si nous essayons toosplit cette table, nous allons une erreur :

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Msg 35346, niveau 15, état 1, ligne 44 fractionnée de clause d’instruction ALTER PARTITION a échoué, car la partition de hello n’est pas vide.  Seules les partitions vides peuvent être fractionnées lorsqu’il existe un index columnstore sur la table de hello. Envisagez de désactiver l’index columnstore de hello avant d’émettre l’instruction ALTER PARTITION de hello, puis reconstruisez les index columnstore de hello après ALTER PARTITION.

Toutefois, nous pouvons utiliser `CTAS` toocreate un toohold table nouvelle nos données.

```sql
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    FactInternetSales
WHERE   1=2
;
```

Comme les limites de partition hello sont alignés, un commutateur est autorisé. Cela laisse une table de source de hello avec une partition vide qui nous pouvons fractionnée par la suite.

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Tout ce qui reste toodo est tooalign toohello de nos données de partition nouvelles limites à l’aide de `CTAS` et basculez nos données dans la table principale de toohello

```sql
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales_20000101]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 toodbo.FactInternetSales PARTITION 2;
```

Une fois que vous avez terminé le déplacement des hello de données de hello il s’agit d’une bonne idée toorefresh hello de statistiques sur hello cible table tooensure qu’ils reflètent précisément nouvelle distribution des données hello dans leurs partitions respectifs de hello :

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a>Contrôle de code source dans le cadre du partitionnement d’une table
tooavoid votre définition de la table à partir de **bullage** dans votre système de contrôle de code source, vous pouvez vouloir hello tooconsider approche :

1. Créer la table de hello comme une table partitionnée, mais sans valeurs de partition

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    ()
                )
)
;
```

1. `SPLIT`table Hello dans le cadre du processus de déploiement hello :

```sql
-- Create a table containing hello partition boundaries

CREATE TABLE #partitions
WITH
(
    LOCATION = USER_DB
,   DISTRIBUTION = HASH(ptn_no)
)
AS
SELECT  ptn_no
,       ROW_NUMBER() OVER (ORDER BY (ptn_no)) as seq_no
FROM    (
        SELECT CAST(20000101 AS INT) ptn_no
        UNION ALL
        SELECT CAST(20010101 AS INT)
        UNION ALL
        SELECT CAST(20020101 AS INT)
        UNION ALL
        SELECT CAST(20030101 AS INT)
        UNION ALL
        SELECT CAST(20040101 AS INT)
        ) a
;

-- Iterate over hello partition boundaries and split hello table

DECLARE @c INT = (SELECT COUNT(*) FROM #partitions)
,       @i INT = 1                                 --iterator for while loop
,       @q NVARCHAR(4000)                          --query
,       @p NVARCHAR(20)     = N''                  --partition_number
,       @s NVARCHAR(128)    = N'dbo'               --schema
,       @t NVARCHAR(128)    = N'FactInternetSales' --table
;

WHILE @i <= @c
BEGIN
    SET @p = (SELECT ptn_no FROM #partitions WHERE seq_no = @i);
    SET @q = (SELECT N'ALTER TABLE '+@s+N'.'+@t+N' SPLIT RANGE ('+@p+N');');

    -- PRINT @q;
    EXECUTE sp_executesql @q;

    SET @i+=1;
END

-- Code clean-up

DROP TABLE #partitions;
```

Avec cette hello approche code de contrôle de code source reste statique et les valeurs limites partitionnement hello sont autorisées toobe dynamique ; évolution avec l’entrepôt de hello au fil du temps.

## <a name="next-steps"></a>Étapes suivantes
toolearn, voir les articles hello sur [vue d’ensemble de la Table][Overview], [les Types de données de Table][Data Types], [distribution d’une Table] [ Distribute], [L’indexation d’une Table][Index], [gestion de statistiques de Table] [ Statistics] et [ Tables temporaires][Temporary].  Pour en savoir plus sur les meilleures pratiques, consultez [Meilleures pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[workload management]: ./sql-data-warehouse-develop-concurrency.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!-- MSDN Articles -->
[Partitioned Tables and Indexes]: https://msdn.microsoft.com/library/ms190787.aspx
[ALTER TABLE]: https://msdn.microsoft.com/en-us/library/ms190273.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[partition function]: https://msdn.microsoft.com/library/ms187802.aspx
[partition scheme]: https://msdn.microsoft.com/library/ms179854.aspx


<!-- Other web references -->
