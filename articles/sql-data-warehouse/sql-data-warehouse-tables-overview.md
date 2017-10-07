---
title: "aaaOverview de tables dans l’entrepôt de données SQL | Documents Microsoft"
description: Prise en main des tables Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 2114d9ad-c113-43da-859f-419d72604bdf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/29/2016
ms.author: shigu;jrj
ms.openlocfilehash: 4edabcb4b0754bf6c99c2b6b3f0c077749051d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-tables-in-sql-data-warehouse"></a>Vue d’ensemble des tables dans SQL Data Warehouse
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

La prise en main de la création de tables dans SQL Data Warehouse est simple.  Hello base [CREATE TABLE] [ CREATE TABLE] syntaxe suit la syntaxe courantes de hello sans doute déjà familiarisés avec d’autres bases de données.  toocreate une table, vous devez simplement tooname nommer vos colonnes de votre table et définir des types de données pour chaque colonne.  Si vous avez créer des tables dans les autres bases de données, cela doit ressembler tooyou très familier.

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

Bonjour à l’exemple ci-dessus crée une table nommée Customers avec deux colonnes, FirstName et LastName.  Chaque colonne est définie avec un type de données de VARCHAR(25), ce qui limite les caractères de too25 données hello.  Ces attributs fondamentaux d’une table, ainsi que d’autres, sont principalement hello identique à celui des autres bases de données.  Types de données sont définis pour chaque colonne et garantissant l’intégrité des hello de vos données.  Les index peuvent être ajoutés tooimprove performances en réduisant les e/s.  Le partitionnement peut être ajouté tooimprove performances lorsque vous avez besoin des données de toomodify.

Le processus consistant à [renommer][RENAME] une table SQL Data Warehouse ressemble à ceci :

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a>Tables distribuées
Un nouvel attribut fondamentaux introduit par des systèmes distribués, comme SQL Data Warehouse hello **colonne de distribution**.  colonne de distribution Hello est très bien qu’il ressemble.  Il s’agit des colonne hello qui détermine comment toodistribute, ou la division, vos données coulisses hello.  Lorsque vous créez une table sans spécifier de colonne de distribution hello, table de hello est automatiquement distribué à l’aide de **tourniquet (Round Robin)**.  Bien que les tables de tourniquet (round robin) puissent être suffisantes dans certains scénarios, la définition des colonnes de distribution peut considérablement réduire le déplacement des données pendant les requêtes, optimisant ainsi les performances.  Dans les situations où il existe une petite quantité de données dans une table, en choisissant toocreate de table hello avec hello **répliquer** type de distribution copie le nœud de calcul de données tooeach et enregistre le déplacement des données au moment de l’exécution de requête. Consultez [distribution d’une Table] [ Distribute] toolearn plus sur la façon tooselect une colonne de distribution.

## <a name="indexing-and-partitioning-tables"></a>Indexation et partitionnement des tables
Comme vous deviennent plus avancées à l’aide de l’entrepôt de données SQL et que vous souhaitez toooptimize performances, vous souhaiterez toolearn plus sur la création de Table.  toolearn, voir les articles hello sur [les Types de données de Table][Data Types], [distribution d’une Table][Distribute], [l’indexation d’une Table] [ Index] et [partitionnement d’une Table][Partition].

## <a name="table-statistics"></a>Statistiques de table
Les statistiques sont un toogetting extrêmement important hello performances optimales de votre entrepôt de données SQL.  Étant donné que l’entrepôt de données SQL pas encore automatiquement créer et mettre à jour des statistiques, telles que vous pouvez provenir tooexpect dans la base de données SQL Azure, la lecture de notre article sur [statistiques] [ Statistics] peut être un de hello principaux articles vous lisez tooensure, vous obtenez des performances optimales hello de vos requêtes.

## <a name="temporary-tables"></a>Tables temporaires
Les tables temporaires sont des tables qui existent pour la durée de l’ouverture de session hello uniquement et qui ne sont pas visibles par d’autres utilisateurs.  Les tables temporaires peuvent être un bon moyen tooprevent d’autres utilisateurs de voir les résultats temporaires et également réduire la nécessité de hello pour le nettoyage.  Étant donné que les tables temporaires utilisent également le stockage local, elles peuvent offrir des performances plus rapides pour certaines opérations.  Consultez hello [Table temporaire] [ Temporary] articles pour plus d’informations sur les tables temporaires.

## <a name="external-tables"></a>Tables externes
Tables externes, également connu sous le nom des tables de Polybase, sont des tables qui peuvent être interrogées à partir de l’entrepôt de données SQL, mais toodata point externe à partir de l’entrepôt de données SQL.  Par exemple, vous pouvez créer une table externe qui toofiles points sur le stockage d’objets Blob Azure.  Pour plus d’informations sur la façon dont toocreate et interrogent une table externe, consultez [charger des données avec Polybase][Load data with Polybase].  

## <a name="unsupported-table-features"></a>Fonctionnalités de table non prises en charge
Lors de l’entrepôt de données SQL contient de nombreux hello même table des fonctionnalités offertes par les autres bases de données, il existe certaines fonctionnalités qui ne sont pas pris en charge.  Voici une liste de certaines hello table des fonctionnalités qui ne sont pas pris en charge.

| Fonctionnalités non prises en charge |
| --- |
| Clé primaire, clés étrangères, [contraintes de table][Table Constraints] |
| [Index uniques][Unique Indexes] |
| [Colonnes calculées][Computed Columns] |
| [Colonnes éparses][Sparse Columns] |
| [Types définis par l’utilisateur][User-Defined Types] |
| [Séquence][Sequence] |
| [Déclencheurs][Triggers] |
| [Vues indexées][Indexed Views] |
| [Synonymes][Synonyms] |

## <a name="table-size-queries"></a>Requêtes de taille de table
Un seul espace tooidentify de façon simple et consommées par une table dans chacun des distributions de hello 60, des lignes est toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

Toutefois, l’utilisation des commandes DBCC peut être très limitante.  Vues de gestion dynamique (DMV) vous permettra de toosee beaucoup plus de détail ainsi que vous permettent de contrôler beaucoup plus importante des résultats de requête hello.  Commencez par créer cette vue, qui sera référencé tooby de nombreux exemples dans cette section et autres articles.

```sql
CREATE VIEW dbo.vTableSizes
AS
WITH base
AS
(
SELECT 
 GETDATE()                                                             AS  [execution_time]
, DB_NAME()                                                            AS  [database_name]
, s.name                                                               AS  [schema_name]
, t.name                                                               AS  [table_name]
, QUOTENAME(s.name)+'.'+QUOTENAME(t.name)                              AS  [two_part_name]
, nt.[name]                                                            AS  [node_table_name]
, ROW_NUMBER() OVER(PARTITION BY nt.[name] ORDER BY (SELECT NULL))     AS  [node_table_name_seq]
, tp.[distribution_policy_desc]                                        AS  [distribution_policy_name]
, c.[name]                                                             AS  [distribution_column]
, nt.[distribution_id]                                                 AS  [distribution_id]
, i.[type]                                                             AS  [index_type]
, i.[type_desc]                                                        AS  [index_type_desc]
, nt.[pdw_node_id]                                                     AS  [pdw_node_id]
, pn.[type]                                                            AS  [pdw_node_type]
, pn.[name]                                                            AS  [pdw_node_name]
, di.name                                                              AS  [dist_name]
, di.position                                                          AS  [dist_position]
, nps.[partition_number]                                               AS  [partition_nmbr]
, nps.[reserved_page_count]                                            AS  [reserved_space_page_count]
, nps.[reserved_page_count] - nps.[used_page_count]                    AS  [unused_space_page_count]
, nps.[in_row_data_page_count] 
    + nps.[row_overflow_used_page_count] 
    + nps.[lob_used_page_count]                                        AS  [data_space_page_count]
, nps.[reserved_page_count] 
 - (nps.[reserved_page_count] - nps.[used_page_count]) 
 - ([in_row_data_page_count] 
         + [row_overflow_used_page_count]+[lob_used_page_count])       AS  [index_space_page_count]
, nps.[row_count]                                                      AS  [row_count]
from 
    sys.schemas s
INNER JOIN sys.tables t
    ON s.[schema_id] = t.[schema_id]
INNER JOIN sys.indexes i
    ON  t.[object_id] = i.[object_id]
    AND i.[index_id] <= 1
INNER JOIN sys.pdw_table_distribution_properties tp
    ON t.[object_id] = tp.[object_id]
INNER JOIN sys.pdw_table_mappings tm
    ON t.[object_id] = tm.[object_id]
INNER JOIN sys.pdw_nodes_tables nt
    ON tm.[physical_name] = nt.[name]
INNER JOIN sys.dm_pdw_nodes pn
    ON  nt.[pdw_node_id] = pn.[pdw_node_id]
INNER JOIN sys.pdw_distributions di
    ON  nt.[distribution_id] = di.[distribution_id]
INNER JOIN sys.dm_pdw_nodes_db_partition_stats nps
    ON nt.[object_id] = nps.[object_id]
    AND nt.[pdw_node_id] = nps.[pdw_node_id]
    AND nt.[distribution_id] = nps.[distribution_id]
LEFT OUTER JOIN (select * from sys.pdw_column_distribution_properties where distribution_ordinal = 1) cdp
    ON t.[object_id] = cdp.[object_id]
LEFT OUTER JOIN sys.columns c
    ON cdp.[object_id] = c.[object_id]
    AND cdp.[column_id] = c.[column_id]
)
, size
AS
(
SELECT
   [execution_time]
,  [database_name]
,  [schema_name]
,  [table_name]
,  [two_part_name]
,  [node_table_name]
,  [node_table_name_seq]
,  [distribution_policy_name]
,  [distribution_column]
,  [distribution_id]
,  [index_type]
,  [index_type_desc]
,  [pdw_node_id]
,  [pdw_node_type]
,  [pdw_node_name]
,  [dist_name]
,  [dist_position]
,  [partition_nmbr]
,  [reserved_space_page_count]
,  [unused_space_page_count]
,  [data_space_page_count]
,  [index_space_page_count]
,  [row_count]
,  ([reserved_space_page_count] * 8.0)                                 AS [reserved_space_KB]
,  ([reserved_space_page_count] * 8.0)/1000                            AS [reserved_space_MB]
,  ([reserved_space_page_count] * 8.0)/1000000                         AS [reserved_space_GB]
,  ([reserved_space_page_count] * 8.0)/1000000000                      AS [reserved_space_TB]
,  ([unused_space_page_count]   * 8.0)                                 AS [unused_space_KB]
,  ([unused_space_page_count]   * 8.0)/1000                            AS [unused_space_MB]
,  ([unused_space_page_count]   * 8.0)/1000000                         AS [unused_space_GB]
,  ([unused_space_page_count]   * 8.0)/1000000000                      AS [unused_space_TB]
,  ([data_space_page_count]     * 8.0)                                 AS [data_space_KB]
,  ([data_space_page_count]     * 8.0)/1000                            AS [data_space_MB]
,  ([data_space_page_count]     * 8.0)/1000000                         AS [data_space_GB]
,  ([data_space_page_count]     * 8.0)/1000000000                      AS [data_space_TB]
,  ([index_space_page_count]  * 8.0)                                   AS [index_space_KB]
,  ([index_space_page_count]  * 8.0)/1000                              AS [index_space_MB]
,  ([index_space_page_count]  * 8.0)/1000000                           AS [index_space_GB]
,  ([index_space_page_count]  * 8.0)/1000000000                        AS [index_space_TB]
FROM base
)
SELECT * 
FROM size
;
```

### <a name="table-space-summary"></a>Résumé de l’espace de table
Cette requête renvoie les lignes hello et l’espace par table.  Il s’agit d’un toosee requête excellent les tables qui sont vos tables les plus volumineuses et qu’ils sont tourniquet (Round Robin), répliquées ou distribuées de hachage.  Pour les tables de hachage distribué il montre également la colonne de distribution hello.  Dans la plupart des cas, les plus grandes tables doivent être à distribution par hachage avec un index columnstore en cluster.

```sql
SELECT 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
,    COUNT(distinct partition_nmbr) as nbr_partitions
,    SUM(row_count)                 as table_row_count
,    SUM(reserved_space_GB)         as table_reserved_space_GB
,    SUM(data_space_GB)             as table_data_space_GB
,    SUM(index_space_GB)            as table_index_space_GB
,    SUM(unused_space_GB)           as table_unused_space_GB
FROM 
    dbo.vTableSizes
GROUP BY 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
ORDER BY
    table_reserved_space_GB desc
;
```

### <a name="table-space-by-distribution-type"></a>Espace de table par type de distribution
```sql
SELECT 
     distribution_policy_name
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY distribution_policy_name
;
```

### <a name="table-space-by-index-type"></a>Espace de table par type d’index
```sql
SELECT 
     index_type_desc
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY index_type_desc
;
```

### <a name="distribution-space-summary"></a>Résumé de l’espace de distribution
```sql
SELECT 
    distribution_id
,    SUM(row_count)                as total_node_distribution_row_count
,    SUM(reserved_space_MB)        as total_node_distribution_reserved_space_MB
,    SUM(data_space_MB)            as total_node_distribution_data_space_MB
,    SUM(index_space_MB)           as total_node_distribution_index_space_MB
,    SUM(unused_space_MB)          as total_node_distribution_unused_space_MB
FROM dbo.vTableSizes
GROUP BY     distribution_id
ORDER BY    distribution_id
;
```

## <a name="next-steps"></a>Étapes suivantes
toolearn, voir les articles hello sur [les Types de données de Table][Data Types], [distribution d’une Table][Distribute], [l’indexation d’une Table] [ Index], [Partitionnement d’une Table][Partition], [gestion de statistiques de Table] [ Statistics] et [ Tables temporaires][Temporary].  Pour en savoir plus sur les meilleures pratiques, consultez [Meilleures pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Load data with Polybase]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md

<!--MSDN references-->
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx
[DBCC PDW_SHOWSPACEUSED]: https://msdn.microsoft.com/library/mt204028.aspx
[Table Constraints]: https://msdn.microsoft.com/library/ms188066.aspx
[Computed Columns]: https://msdn.microsoft.com/library/ms186241.aspx
[Sparse Columns]: https://msdn.microsoft.com/library/cc280604.aspx
[User-Defined Types]: https://msdn.microsoft.com/library/ms131694.aspx
[Sequence]: https://msdn.microsoft.com/library/ff878091.aspx
[Triggers]: https://msdn.microsoft.com/library/ms189799.aspx
[Indexed Views]: https://msdn.microsoft.com/library/ms191432.aspx
[Synonyms]: https://msdn.microsoft.com/library/ms177544.aspx
[Unique Indexes]: https://msdn.microsoft.com/library/ms188783.aspx

<!--Other Web references-->
