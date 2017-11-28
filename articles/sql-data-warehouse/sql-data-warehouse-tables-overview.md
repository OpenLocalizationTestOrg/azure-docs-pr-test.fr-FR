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
# <a name="overview-of-tables-in-sql-data-warehouse"></a><span data-ttu-id="74d04-103">Vue d’ensemble des tables dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="74d04-103">Overview of tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="74d04-104">[Vue d’ensemble][Overview]</span><span class="sxs-lookup"><span data-stu-id="74d04-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="74d04-105">[Types de données][Data Types]</span><span class="sxs-lookup"><span data-stu-id="74d04-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="74d04-106">[Distribuer][Distribute]</span><span class="sxs-lookup"><span data-stu-id="74d04-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="74d04-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="74d04-107">[Index][Index]</span></span>
> * <span data-ttu-id="74d04-108">[Partition][Partition]</span><span class="sxs-lookup"><span data-stu-id="74d04-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="74d04-109">[Statistiques][Statistics]</span><span class="sxs-lookup"><span data-stu-id="74d04-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="74d04-110">[Temporaire][Temporary]</span><span class="sxs-lookup"><span data-stu-id="74d04-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="74d04-111">La prise en main de la création de tables dans SQL Data Warehouse est simple.</span><span class="sxs-lookup"><span data-stu-id="74d04-111">Getting started with creating tables in SQL Data Warehouse is simple.</span></span>  <span data-ttu-id="74d04-112">Hello base [CREATE TABLE] [ CREATE TABLE] syntaxe suit la syntaxe courantes de hello sans doute déjà familiarisés avec d’autres bases de données.</span><span class="sxs-lookup"><span data-stu-id="74d04-112">hello basic [CREATE TABLE][CREATE TABLE] syntax follows hello common syntax you are most likely already familiar with from working with other databases.</span></span>  <span data-ttu-id="74d04-113">toocreate une table, vous devez simplement tooname nommer vos colonnes de votre table et définir des types de données pour chaque colonne.</span><span class="sxs-lookup"><span data-stu-id="74d04-113">toocreate a table, you simply need tooname your table, name your columns and define data types for each column.</span></span>  <span data-ttu-id="74d04-114">Si vous avez créer des tables dans les autres bases de données, cela doit ressembler tooyou très familier.</span><span class="sxs-lookup"><span data-stu-id="74d04-114">If you've create tables in other databases, this should look very familiar tooyou.</span></span>

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

<span data-ttu-id="74d04-115">Bonjour à l’exemple ci-dessus crée une table nommée Customers avec deux colonnes, FirstName et LastName.</span><span class="sxs-lookup"><span data-stu-id="74d04-115">hello above example creates a table named Customers with two columns, FirstName and LastName.</span></span>  <span data-ttu-id="74d04-116">Chaque colonne est définie avec un type de données de VARCHAR(25), ce qui limite les caractères de too25 données hello.</span><span class="sxs-lookup"><span data-stu-id="74d04-116">Each column is defined with a data type of VARCHAR(25), which limits hello data too25 characters.</span></span>  <span data-ttu-id="74d04-117">Ces attributs fondamentaux d’une table, ainsi que d’autres, sont principalement hello identique à celui des autres bases de données.</span><span class="sxs-lookup"><span data-stu-id="74d04-117">These fundamental attributes of a table, as well as others, are mostly hello same as other databases.</span></span>  <span data-ttu-id="74d04-118">Types de données sont définis pour chaque colonne et garantissant l’intégrité des hello de vos données.</span><span class="sxs-lookup"><span data-stu-id="74d04-118">Data types are defined for each column and ensure hello integrity of your data.</span></span>  <span data-ttu-id="74d04-119">Les index peuvent être ajoutés tooimprove performances en réduisant les e/s.</span><span class="sxs-lookup"><span data-stu-id="74d04-119">Indexes can be added tooimprove performance by reducing I/O.</span></span>  <span data-ttu-id="74d04-120">Le partitionnement peut être ajouté tooimprove performances lorsque vous avez besoin des données de toomodify.</span><span class="sxs-lookup"><span data-stu-id="74d04-120">Partitioning can be added tooimprove performance when you need toomodify data.</span></span>

<span data-ttu-id="74d04-121">Le processus consistant à [renommer][RENAME] une table SQL Data Warehouse ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="74d04-121">[Renaming][RENAME] a SQL Data Warehouse table looks like this:</span></span>

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a><span data-ttu-id="74d04-122">Tables distribuées</span><span class="sxs-lookup"><span data-stu-id="74d04-122">Distributed tables</span></span>
<span data-ttu-id="74d04-123">Un nouvel attribut fondamentaux introduit par des systèmes distribués, comme SQL Data Warehouse hello **colonne de distribution**.</span><span class="sxs-lookup"><span data-stu-id="74d04-123">A new fundamental attribute introduced by distributed systems like SQL Data Warehouse is hello **distribution column**.</span></span>  <span data-ttu-id="74d04-124">colonne de distribution Hello est très bien qu’il ressemble.</span><span class="sxs-lookup"><span data-stu-id="74d04-124">hello distribution column is very much what it sounds like.</span></span>  <span data-ttu-id="74d04-125">Il s’agit des colonne hello qui détermine comment toodistribute, ou la division, vos données coulisses hello.</span><span class="sxs-lookup"><span data-stu-id="74d04-125">It is hello column that determines how toodistribute, or divide, your data behind hello scenes.</span></span>  <span data-ttu-id="74d04-126">Lorsque vous créez une table sans spécifier de colonne de distribution hello, table de hello est automatiquement distribué à l’aide de **tourniquet (Round Robin)**.</span><span class="sxs-lookup"><span data-stu-id="74d04-126">When you create a table without specifying hello distribution column, hello table is automatically distributed using **round robin**.</span></span>  <span data-ttu-id="74d04-127">Bien que les tables de tourniquet (round robin) puissent être suffisantes dans certains scénarios, la définition des colonnes de distribution peut considérablement réduire le déplacement des données pendant les requêtes, optimisant ainsi les performances.</span><span class="sxs-lookup"><span data-stu-id="74d04-127">While round robin tables can be sufficient in some scenarios, defining distribution columns can greatly reduce data movement during queries, thus optimizing performance.</span></span>  <span data-ttu-id="74d04-128">Dans les situations où il existe une petite quantité de données dans une table, en choisissant toocreate de table hello avec hello **répliquer** type de distribution copie le nœud de calcul de données tooeach et enregistre le déplacement des données au moment de l’exécution de requête.</span><span class="sxs-lookup"><span data-stu-id="74d04-128">In situations where there is a small amount of data in a table, choosing toocreate hello table with hello **replicate** distribution type copies data tooeach compute node and saves data movement at query execution time.</span></span> <span data-ttu-id="74d04-129">Consultez [distribution d’une Table] [ Distribute] toolearn plus sur la façon tooselect une colonne de distribution.</span><span class="sxs-lookup"><span data-stu-id="74d04-129">See [Distributing a Table][Distribute] toolearn more about how tooselect a distribution column.</span></span>

## <a name="indexing-and-partitioning-tables"></a><span data-ttu-id="74d04-130">Indexation et partitionnement des tables</span><span class="sxs-lookup"><span data-stu-id="74d04-130">Indexing and partitioning tables</span></span>
<span data-ttu-id="74d04-131">Comme vous deviennent plus avancées à l’aide de l’entrepôt de données SQL et que vous souhaitez toooptimize performances, vous souhaiterez toolearn plus sur la création de Table.</span><span class="sxs-lookup"><span data-stu-id="74d04-131">As you become more advanced in using SQL Data Warehouse and want toooptimize performance, you'll want toolearn more about Table Design.</span></span>  <span data-ttu-id="74d04-132">toolearn, voir les articles hello sur [les Types de données de Table][Data Types], [distribution d’une Table][Distribute], [l’indexation d’une Table] [ Index] et [partitionnement d’une Table][Partition].</span><span class="sxs-lookup"><span data-stu-id="74d04-132">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index] and  [Partitioning a Table][Partition].</span></span>

## <a name="table-statistics"></a><span data-ttu-id="74d04-133">Statistiques de table</span><span class="sxs-lookup"><span data-stu-id="74d04-133">Table statistics</span></span>
<span data-ttu-id="74d04-134">Les statistiques sont un toogetting extrêmement important hello performances optimales de votre entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="74d04-134">Statistics are an extremely important toogetting hello best performance out of your SQL Data Warehouse.</span></span>  <span data-ttu-id="74d04-135">Étant donné que l’entrepôt de données SQL pas encore automatiquement créer et mettre à jour des statistiques, telles que vous pouvez provenir tooexpect dans la base de données SQL Azure, la lecture de notre article sur [statistiques] [ Statistics] peut être un de hello principaux articles vous lisez tooensure, vous obtenez des performances optimales hello de vos requêtes.</span><span class="sxs-lookup"><span data-stu-id="74d04-135">Since SQL Data Warehouse does not yet automatically create and update statistics for you, like you may have come tooexpect in Azure SQL Database, reading our article on [Statistics][Statistics] might be one of hello most important articles you read tooensure that you get hello best performance from your queries.</span></span>

## <a name="temporary-tables"></a><span data-ttu-id="74d04-136">Tables temporaires</span><span class="sxs-lookup"><span data-stu-id="74d04-136">Temporary tables</span></span>
<span data-ttu-id="74d04-137">Les tables temporaires sont des tables qui existent pour la durée de l’ouverture de session hello uniquement et qui ne sont pas visibles par d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="74d04-137">Temporary tables are tables which only exist for hello duration of your logon and cannot be seen by other users.</span></span>  <span data-ttu-id="74d04-138">Les tables temporaires peuvent être un bon moyen tooprevent d’autres utilisateurs de voir les résultats temporaires et également réduire la nécessité de hello pour le nettoyage.</span><span class="sxs-lookup"><span data-stu-id="74d04-138">Temporary tables can be a good way tooprevent others from seeing temporary results and also reduce hello need for cleanup.</span></span>  <span data-ttu-id="74d04-139">Étant donné que les tables temporaires utilisent également le stockage local, elles peuvent offrir des performances plus rapides pour certaines opérations.</span><span class="sxs-lookup"><span data-stu-id="74d04-139">Since temporary tables also utilize local storage, they can offer faster performance for some operations.</span></span>  <span data-ttu-id="74d04-140">Consultez hello [Table temporaire] [ Temporary] articles pour plus d’informations sur les tables temporaires.</span><span class="sxs-lookup"><span data-stu-id="74d04-140">See hello [Temporary Table][Temporary] articles for more details about temporary tables.</span></span>

## <a name="external-tables"></a><span data-ttu-id="74d04-141">Tables externes</span><span class="sxs-lookup"><span data-stu-id="74d04-141">External tables</span></span>
<span data-ttu-id="74d04-142">Tables externes, également connu sous le nom des tables de Polybase, sont des tables qui peuvent être interrogées à partir de l’entrepôt de données SQL, mais toodata point externe à partir de l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="74d04-142">External tables, also known as Polybase tables, are tables which can be queried from SQL Data Warehouse, but point toodata external from SQL Data Warehouse.</span></span>  <span data-ttu-id="74d04-143">Par exemple, vous pouvez créer une table externe qui toofiles points sur le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="74d04-143">For example, you can create an external table which points toofiles on Azure Blob Storage.</span></span>  <span data-ttu-id="74d04-144">Pour plus d’informations sur la façon dont toocreate et interrogent une table externe, consultez [charger des données avec Polybase][Load data with Polybase].</span><span class="sxs-lookup"><span data-stu-id="74d04-144">For more details on how toocreate and query an external table, see [Load data with Polybase][Load data with Polybase].</span></span>  

## <a name="unsupported-table-features"></a><span data-ttu-id="74d04-145">Fonctionnalités de table non prises en charge</span><span class="sxs-lookup"><span data-stu-id="74d04-145">Unsupported table features</span></span>
<span data-ttu-id="74d04-146">Lors de l’entrepôt de données SQL contient de nombreux hello même table des fonctionnalités offertes par les autres bases de données, il existe certaines fonctionnalités qui ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="74d04-146">While SQL Data Warehouse contains many of hello same table features offered by other databases, there are some features which are not yet supported.</span></span>  <span data-ttu-id="74d04-147">Voici une liste de certaines hello table des fonctionnalités qui ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="74d04-147">Below is a list of some of hello table features which are not yet supported.</span></span>

| <span data-ttu-id="74d04-148">Fonctionnalités non prises en charge</span><span class="sxs-lookup"><span data-stu-id="74d04-148">Unsupported features</span></span> |
| --- |
| <span data-ttu-id="74d04-149">Clé primaire, clés étrangères, [contraintes de table][Table Constraints]</span><span class="sxs-lookup"><span data-stu-id="74d04-149">Primary key, Foreign keys, Unique and Check [Table Constraints][Table Constraints]</span></span> |
| <span data-ttu-id="74d04-150">[Index uniques][Unique Indexes]</span><span class="sxs-lookup"><span data-stu-id="74d04-150">[Unique Indexes][Unique Indexes]</span></span> |
| <span data-ttu-id="74d04-151">[Colonnes calculées][Computed Columns]</span><span class="sxs-lookup"><span data-stu-id="74d04-151">[Computed Columns][Computed Columns]</span></span> |
| <span data-ttu-id="74d04-152">[Colonnes éparses][Sparse Columns]</span><span class="sxs-lookup"><span data-stu-id="74d04-152">[Sparse Columns][Sparse Columns]</span></span> |
| <span data-ttu-id="74d04-153">[Types définis par l’utilisateur][User-Defined Types]</span><span class="sxs-lookup"><span data-stu-id="74d04-153">[User-Defined Types][User-Defined Types]</span></span> |
| <span data-ttu-id="74d04-154">[Séquence][Sequence]</span><span class="sxs-lookup"><span data-stu-id="74d04-154">[Sequence][Sequence]</span></span> |
| <span data-ttu-id="74d04-155">[Déclencheurs][Triggers]</span><span class="sxs-lookup"><span data-stu-id="74d04-155">[Triggers][Triggers]</span></span> |
| <span data-ttu-id="74d04-156">[Vues indexées][Indexed Views]</span><span class="sxs-lookup"><span data-stu-id="74d04-156">[Indexed Views][Indexed Views]</span></span> |
| <span data-ttu-id="74d04-157">[Synonymes][Synonyms]</span><span class="sxs-lookup"><span data-stu-id="74d04-157">[Synonyms][Synonyms]</span></span> |

## <a name="table-size-queries"></a><span data-ttu-id="74d04-158">Requêtes de taille de table</span><span class="sxs-lookup"><span data-stu-id="74d04-158">Table size queries</span></span>
<span data-ttu-id="74d04-159">Un seul espace tooidentify de façon simple et consommées par une table dans chacun des distributions de hello 60, des lignes est toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span><span class="sxs-lookup"><span data-stu-id="74d04-159">One simple way tooidentify space and rows consumed by a table in each of hello 60 distributions, is toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span></span>

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="74d04-160">Toutefois, l’utilisation des commandes DBCC peut être très limitante.</span><span class="sxs-lookup"><span data-stu-id="74d04-160">However, using DBCC commands can be quite limiting.</span></span>  <span data-ttu-id="74d04-161">Vues de gestion dynamique (DMV) vous permettra de toosee beaucoup plus de détail ainsi que vous permettent de contrôler beaucoup plus importante des résultats de requête hello.</span><span class="sxs-lookup"><span data-stu-id="74d04-161">Dynamic management views (DMVs) will allow you toosee much more detail as well as give you much greater control over hello query results.</span></span>  <span data-ttu-id="74d04-162">Commencez par créer cette vue, qui sera référencé tooby de nombreux exemples dans cette section et autres articles.</span><span class="sxs-lookup"><span data-stu-id="74d04-162">Start by creating this view, which will be referred tooby many of our examples in this and other articles.</span></span>

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

### <a name="table-space-summary"></a><span data-ttu-id="74d04-163">Résumé de l’espace de table</span><span class="sxs-lookup"><span data-stu-id="74d04-163">Table space summary</span></span>
<span data-ttu-id="74d04-164">Cette requête renvoie les lignes hello et l’espace par table.</span><span class="sxs-lookup"><span data-stu-id="74d04-164">This query returns hello rows and space by table.</span></span>  <span data-ttu-id="74d04-165">Il s’agit d’un toosee requête excellent les tables qui sont vos tables les plus volumineuses et qu’ils sont tourniquet (Round Robin), répliquées ou distribuées de hachage.</span><span class="sxs-lookup"><span data-stu-id="74d04-165">It is a great query toosee which tables are your largest tables and whether they are round robin, replicated or hash distributed.</span></span>  <span data-ttu-id="74d04-166">Pour les tables de hachage distribué il montre également la colonne de distribution hello.</span><span class="sxs-lookup"><span data-stu-id="74d04-166">For hash distributed tables it also shows hello distribution column.</span></span>  <span data-ttu-id="74d04-167">Dans la plupart des cas, les plus grandes tables doivent être à distribution par hachage avec un index columnstore en cluster.</span><span class="sxs-lookup"><span data-stu-id="74d04-167">In most cases your largest tables should be hash distributed with a clustered columnstore index.</span></span>

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

### <a name="table-space-by-distribution-type"></a><span data-ttu-id="74d04-168">Espace de table par type de distribution</span><span class="sxs-lookup"><span data-stu-id="74d04-168">Table space by distribution type</span></span>
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

### <a name="table-space-by-index-type"></a><span data-ttu-id="74d04-169">Espace de table par type d’index</span><span class="sxs-lookup"><span data-stu-id="74d04-169">Table space by index type</span></span>
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

### <a name="distribution-space-summary"></a><span data-ttu-id="74d04-170">Résumé de l’espace de distribution</span><span class="sxs-lookup"><span data-stu-id="74d04-170">Distribution space summary</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="74d04-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="74d04-171">Next steps</span></span>
<span data-ttu-id="74d04-172">toolearn, voir les articles hello sur [les Types de données de Table][Data Types], [distribution d’une Table][Distribute], [l’indexation d’une Table] [ Index], [Partitionnement d’une Table][Partition], [gestion de statistiques de Table] [ Statistics] et [ Tables temporaires][Temporary].</span><span class="sxs-lookup"><span data-stu-id="74d04-172">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="74d04-173">Pour en savoir plus sur les meilleures pratiques, consultez [Meilleures pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="74d04-173">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
