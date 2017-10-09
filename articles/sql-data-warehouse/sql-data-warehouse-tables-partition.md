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
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="ce89d-103">Partitionnement de tables dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ce89d-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="ce89d-104">[Vue d’ensemble][Overview]</span><span class="sxs-lookup"><span data-stu-id="ce89d-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="ce89d-105">[Types de données][Data Types]</span><span class="sxs-lookup"><span data-stu-id="ce89d-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="ce89d-106">[Distribuer][Distribute]</span><span class="sxs-lookup"><span data-stu-id="ce89d-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="ce89d-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="ce89d-107">[Index][Index]</span></span>
> * <span data-ttu-id="ce89d-108">[Partition][Partition]</span><span class="sxs-lookup"><span data-stu-id="ce89d-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="ce89d-109">[Statistiques][Statistics]</span><span class="sxs-lookup"><span data-stu-id="ce89d-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="ce89d-110">[Temporaire][Temporary]</span><span class="sxs-lookup"><span data-stu-id="ce89d-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="ce89d-111">Le partitionnement est pris en charge sur tous les types de table SQL Data Warehouse, notamment columnstore en cluster, index en cluster et segment de mémoire.</span><span class="sxs-lookup"><span data-stu-id="ce89d-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="ce89d-112">Le partitionnement est également pris en charge sur tous les types de distribution, notamment le hachage ou le tourniquet (round robin) distribué.</span><span class="sxs-lookup"><span data-stu-id="ce89d-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="ce89d-113">Il permet de toodivide vos données en groupes plus petits de données et dans la plupart des cas, le partitionnement sont effectuées sur une colonne de date.</span><span class="sxs-lookup"><span data-stu-id="ce89d-113">Partitioning enables you toodivide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="ce89d-114">Avantages du partitionnement</span><span class="sxs-lookup"><span data-stu-id="ce89d-114">Benefits of partitioning</span></span>
<span data-ttu-id="ce89d-115">Le partitionnement peut bénéficier de la maintenance des données et des performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="ce89d-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="ce89d-116">Si il tire parti à la fois ou une seule est dépendante de la façon dont les données sont chargées et si hello même colonne peut être utilisé pour les deux cas, étant donné que le partitionnement peut uniquement être effectué sur une colonne.</span><span class="sxs-lookup"><span data-stu-id="ce89d-116">Whether it benefits both or just one is dependent on how data is loaded and whether hello same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-tooloads"></a><span data-ttu-id="ce89d-117">Avantages tooloads</span><span class="sxs-lookup"><span data-stu-id="ce89d-117">Benefits tooloads</span></span>
<span data-ttu-id="ce89d-118">le principal avantage de Hello du partitionnement dans l’entrepôt de données SQL est améliorer l’efficacité de hello et les performances de chargement des données à l’aide de la suppression de la partition, en basculant et la fusion.</span><span class="sxs-lookup"><span data-stu-id="ce89d-118">hello primary benefit of partitioning in SQL Data Warehouse is improve hello efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="ce89d-119">Dans la plupart des cas, les données sont partitionnées sur une date de colonne qui est étroitement liée séquence toohello quelles données hello sont chargé toohello de base de données.</span><span class="sxs-lookup"><span data-stu-id="ce89d-119">In most cases data is partitioned on a date column that is closely tied toohello sequence which hello data is loaded toohello database.</span></span>  <span data-ttu-id="ce89d-120">Un des avantages de plus grand hello d’à l’aide de données des partitions toomaintain il hello évitement de journalisation des transactions.</span><span class="sxs-lookup"><span data-stu-id="ce89d-120">One of hello greatest benefits of using partitions toomaintain data it hello avoidance of transaction logging.</span></span>  <span data-ttu-id="ce89d-121">Tout simplement d’insertion, de mise à jour ou de suppression de données soient l’approche la plus simple hello, avec un peu de réflexion et d’efforts, à l’aide du partitionnement pendant le processus de chargement peut considérablement améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="ce89d-121">While simply inserting, updating or deleting data can be hello most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="ce89d-122">Basculement de partition peut être utilisé tooquickly supprimer ou remplacer une section d’une table.</span><span class="sxs-lookup"><span data-stu-id="ce89d-122">Partition switching can be used tooquickly remove or replace a section of a table.</span></span>  <span data-ttu-id="ce89d-123">Par exemple, une table de faits de ventes peut contenir seulement les données pour hello derniers mois 36.</span><span class="sxs-lookup"><span data-stu-id="ce89d-123">For example, a sales fact table might contain just data for hello past 36 months.</span></span>  <span data-ttu-id="ce89d-124">À fin hello de chaque mois, hello mois plus anciens des données de vente est supprimé à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="ce89d-124">At hello end of every month, hello oldest month of sales data is deleted from hello table.</span></span>  <span data-ttu-id="ce89d-125">Ces données pu être supprimées en utilisant des données delete instruction toodelete hello pour hello mois plus ancien.</span><span class="sxs-lookup"><span data-stu-id="ce89d-125">This data could be deleted by using a delete statement toodelete hello data for hello oldest month.</span></span>  <span data-ttu-id="ce89d-126">Toutefois, la suppression d’une grande quantité de données en ligne avec une instruction delete peut prendre beaucoup de temps, ainsi que créer risque hello des transactions volumineuses, ce qui peut prendre un certain temps toorollback si une erreur survient.</span><span class="sxs-lookup"><span data-stu-id="ce89d-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create hello risk of large transactions which could take a long time toorollback if something goes wrong.</span></span>  <span data-ttu-id="ce89d-127">Une approche plus optimale est toosimply dépôt hello partition la plus ancienne des données.</span><span class="sxs-lookup"><span data-stu-id="ce89d-127">A more optimal approach is toosimply drop hello oldest partition of data.</span></span>  <span data-ttu-id="ce89d-128">Où la suppression des lignes individuelles hello plusieurs heures, la suppression d’une partition complète peut prendre des secondes.</span><span class="sxs-lookup"><span data-stu-id="ce89d-128">Where deleting hello individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-tooqueries"></a><span data-ttu-id="ce89d-129">Avantages tooqueries</span><span class="sxs-lookup"><span data-stu-id="ce89d-129">Benefits tooqueries</span></span>
<span data-ttu-id="ce89d-130">Le partitionnement peut être également les performances des requêtes tooimprove utilisé.</span><span class="sxs-lookup"><span data-stu-id="ce89d-130">Partitioning can also be used tooimprove query performance.</span></span>  <span data-ttu-id="ce89d-131">Si une requête qui applique un filtre sur une colonne partitionnée, cela peut limiter Bonjour analyse tooonly Bonjour qualification des partitions qui peuvent être un beaucoup plus petit sous-ensemble de données hello, en évitant une analyse complète.</span><span class="sxs-lookup"><span data-stu-id="ce89d-131">If a query applies a filter on a partitioned column, this can limit hello scan tooonly hello qualifying partitions which may be a much smaller subset of hello data, avoiding a full table scan.</span></span>  <span data-ttu-id="ce89d-132">Avec l’introduction de hello des index columnstore en cluster, des gains de performance élimination prédicat hello sont moins utile, mais dans certains cas, il peut être un tooqueries avantage.</span><span class="sxs-lookup"><span data-stu-id="ce89d-132">With hello introduction of clustered columnstore indexes, hello predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit tooqueries.</span></span>  <span data-ttu-id="ce89d-133">Par exemple, si la table de faits de ventes hello est partitionnée en 36 mois à l’aide du champ de date de vente hello, puis requêtes filtrer sur la date de vente hello peuvent doit effectuer des recherches dans les partitions ne correspondent pas aux filtres de hello.</span><span class="sxs-lookup"><span data-stu-id="ce89d-133">For example, if hello sales fact table is partitioned into 36 months using hello sales date field, then queries that filter on hello sale date can skip searching in partitions that don’t match hello filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="ce89d-134">Guide de dimensionnement de partition</span><span class="sxs-lookup"><span data-stu-id="ce89d-134">Partition sizing guidance</span></span>
<span data-ttu-id="ce89d-135">Lors de la partition peut être utilisé tooimprove performances certains scénarios, la création d’une table avec **trop** partitions peuvent nuire aux performances dans certaines circonstances.</span><span class="sxs-lookup"><span data-stu-id="ce89d-135">While partitioning can be used tooimprove performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="ce89d-136">Ces inquiétudes sont particulièrement avérées pour les tables columnstore en cluster.</span><span class="sxs-lookup"><span data-stu-id="ce89d-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="ce89d-137">Pour le partitionnement toobe utile, il est important toounderstand lorsque toouse de partitionnement et de hello le nombre de partitions toocreate.</span><span class="sxs-lookup"><span data-stu-id="ce89d-137">For partitioning toobe helpful, it is important toounderstand when toouse partitioning and hello number of partitions toocreate.</span></span>  <span data-ttu-id="ce89d-138">Il est aucune règle dur rapide comme toohow le nombre de partitions est trop nombreux, il dépend de vos données et le nombre de partitions vous chargez toosimultaneously.</span><span class="sxs-lookup"><span data-stu-id="ce89d-138">There is no hard fast rule as toohow many partitions are too many, it depends on your data and how many partitions you are loading toosimultaneously.</span></span>  <span data-ttu-id="ce89d-139">Mais en règle générale, envisager l’ajout de 10 s too100s de partitions, pas pour 1 000.</span><span class="sxs-lookup"><span data-stu-id="ce89d-139">But as a general rule of thumb, think of adding 10s too100s of partitions, not 1000s.</span></span>

<span data-ttu-id="ce89d-140">Lors de la création de partitionnement sur **columnstore cluster** tables, il est important tooconsider obtiendrons ainsi le nombre de lignes dans chaque partition.</span><span class="sxs-lookup"><span data-stu-id="ce89d-140">When creating partitioning on **clustered columnstore** tables, it is important tooconsider how many rows will land in each partition.</span></span>  <span data-ttu-id="ce89d-141">Pour une compression et des performances des tables columnstore en cluster optimales, un minimum de 1 million de lignes par partition et par distribution est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ce89d-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="ce89d-142">Avant la création des partitions, SQL Data Warehouse divise déjà chaque table en 60 bases de données distribuées.</span><span class="sxs-lookup"><span data-stu-id="ce89d-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="ce89d-143">N’importe quelle table ajoutée tooa partitionnement est en plus des distributions toohello créées coulisses hello.</span><span class="sxs-lookup"><span data-stu-id="ce89d-143">Any partitioning added tooa table is in addition toohello distributions created behind hello scenes.</span></span>  <span data-ttu-id="ce89d-144">À l’aide de cet exemple, si table de faits de ventes hello contenus des partitions mensuelles 36, étant donné que l’entrepôt de données SQL a des distributions de 60, puis hello faits de ventes table doit contenir des millions de 60 lignes par mois ou 2.1 milliards de lignes lorsque tous les mois sont remplies.</span><span class="sxs-lookup"><span data-stu-id="ce89d-144">Using this example, if hello sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then hello sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="ce89d-145">Si une table contient beaucoup moins de lignes que hello recommandé nombre minimal de lignes par partition, envisagez d’utiliser moins de partitions dans le numéro de commande toomake augmentation hello de lignes par partition.</span><span class="sxs-lookup"><span data-stu-id="ce89d-145">If a table contains significantly less rows than hello recommended minimum number of rows per partition, consider using fewer partitions in order toomake increase hello number of rows per partition.</span></span>  <span data-ttu-id="ce89d-146">Voir aussi hello [indexation] [ Index] article qui comprend des requêtes qui peuvent être exécutés sur SQL Data Warehouse tooassess hello de qualité des index cluster columnstore.</span><span class="sxs-lookup"><span data-stu-id="ce89d-146">Also see hello [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse tooassess hello quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="ce89d-147">Différence de syntaxe à partir de SQL Server</span><span class="sxs-lookup"><span data-stu-id="ce89d-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="ce89d-148">SQL Data Warehouse présente une définition simplifiée de partitions qui diffère légèrement de celle de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ce89d-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="ce89d-149">Les fonctions et les schémas de partitionnement ne sont pas utilisés dans SQL Data Warehouse, car ils se trouvent dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ce89d-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="ce89d-150">Au lieu de cela, vous devez toodo est identifier les points de limite partitionnées hello et de colonne.</span><span class="sxs-lookup"><span data-stu-id="ce89d-150">Instead, all you need toodo is identify partitioned column and hello boundary points.</span></span>  <span data-ttu-id="ce89d-151">Syntaxe hello de partitionnement peut être légèrement différente de SQL Server, les concepts de base hello sont hello même.</span><span class="sxs-lookup"><span data-stu-id="ce89d-151">While hello syntax of partitioning may be slightly different from SQL Server, hello basic concepts are hello same.</span></span>  <span data-ttu-id="ce89d-152">SQL Server et SQL Data Warehouse prennent en charge une colonne de partition par table, qui peut être une partition par plage.</span><span class="sxs-lookup"><span data-stu-id="ce89d-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="ce89d-153">toolearn en savoir plus sur le partitionnement, consultez [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span><span class="sxs-lookup"><span data-stu-id="ce89d-153">toolearn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="ce89d-154">Hello, Voici un exemple d’un entrepôt de données SQL partitionnée [CREATE TABLE] [ CREATE TABLE] instruction, partitions de table de FactInternetSales hello sur la colonne OrderDateKey de hello :</span><span class="sxs-lookup"><span data-stu-id="ce89d-154">hello below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions hello FactInternetSales table on hello OrderDateKey column:</span></span>

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

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="ce89d-155">Migration du partitionnement dans SQL Server</span><span class="sxs-lookup"><span data-stu-id="ce89d-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="ce89d-156">toomigrate SQL Server partitionner simplement les définitions tooSQL l’entrepôt de données :</span><span class="sxs-lookup"><span data-stu-id="ce89d-156">toomigrate SQL Server partition definitions tooSQL Data Warehouse simply:</span></span>

* <span data-ttu-id="ce89d-157">Éliminer hello SQL Server [schéma de partition][partition scheme].</span><span class="sxs-lookup"><span data-stu-id="ce89d-157">Eliminate hello SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="ce89d-158">Ajouter hello [fonction de partition] [ partition function] définition tooyour CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="ce89d-158">Add hello [partition function][partition function] definition tooyour CREATE TABLE.</span></span>

<span data-ttu-id="ce89d-159">Si vous migrez une table partitionnée à partir d’un Bonjour d’instance de SQL Server sous SQL peut vous aider à nombre de hello toointerrogate de lignes qui se trouvent dans chaque partition.</span><span class="sxs-lookup"><span data-stu-id="ce89d-159">If you are migrating a partitioned table from a SQL Server instance hello below SQL can help you toointerrogate hello number of rows that are in each partition.</span></span>  <span data-ttu-id="ce89d-160">Gardez à l’esprit que si hello même granularité de partitionnement est utilisée sur l’entrepôt de données SQL, nombre hello de lignes par partition diminue d’un facteur de 60.</span><span class="sxs-lookup"><span data-stu-id="ce89d-160">Keep in mind that if hello same partitioning granularity is used on SQL Data Warehouse, hello number of rows per partition will decrease by a factor of 60.</span></span>  

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

## <a name="workload-management"></a><span data-ttu-id="ce89d-161">Gestion des charges de travail</span><span class="sxs-lookup"><span data-stu-id="ce89d-161">Workload management</span></span>
<span data-ttu-id="ce89d-162">Toofactor de prendre en compte un dernier dans la décision de partition de table toohello est [gestion de la charge de travail][workload management].</span><span class="sxs-lookup"><span data-stu-id="ce89d-162">One final piece consideration toofactor in toohello table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="ce89d-163">Gestion de la charge de travail dans l’entrepôt de données SQL est principalement les gestion hello de mémoire et d’accès concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="ce89d-163">Workload management in SQL Data Warehouse is primarily hello management of memory and concurrency.</span></span>  <span data-ttu-id="ce89d-164">Mémoire maximale allouée distribution tooeach pendant l’exécution de requête hello de l’entrepôt de données SQL est les classes de ressource gouvernée.</span><span class="sxs-lookup"><span data-stu-id="ce89d-164">In SQL Data Warehouse hello maximum memory allocated tooeach distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="ce89d-165">Dans l’idéal, vos partitions seront redimensionnées par d’autres facteurs tels que les besoins en mémoire de la création d’index columnstore cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ce89d-165">Ideally your partitions will be sized in consideration of other factors like hello memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="ce89d-166">Les index columnstore en cluster présentent des avantages non négligeables lorsque davantage de mémoire leur est allouée.</span><span class="sxs-lookup"><span data-stu-id="ce89d-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="ce89d-167">Par conséquent, vous pouvez tooensure reconstruction d’un index de partition n’est pas privé de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="ce89d-167">Therefore, you will want tooensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="ce89d-168">Augmentation hello de mémoire disponible tooyour requête peut être obtenue en activant le rôle par défaut de hello, smallrc, tooone de hello autres rôles, tels que largerc.</span><span class="sxs-lookup"><span data-stu-id="ce89d-168">Increasing hello amount of memory available tooyour query can be achieved by switching from hello default role, smallrc, tooone of hello other roles such as largerc.</span></span>

<span data-ttu-id="ce89d-169">Pour plus d’informations sur l’allocation de mémoire par distribution hello sont disponibles en interrogeant les vues de gestion dynamique de gouverneur de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="ce89d-169">Information on hello allocation of memory per distribution is available by querying hello resource governor dynamic management views.</span></span> <span data-ttu-id="ce89d-170">En réalité, votre allocation de mémoire sera inférieure à figures hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ce89d-170">In reality your memory grant will be less than hello figures below.</span></span> <span data-ttu-id="ce89d-171">Toutefois, cette figure peut vous aider à dimensionner vos partitions lors d’opérations de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="ce89d-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="ce89d-172">Essayez tooavoid dimensionnement des partitions au-delà d’allocation de mémoire hello fourni par classe de ressource de très nombreuses hello.</span><span class="sxs-lookup"><span data-stu-id="ce89d-172">Try tooavoid sizing your partitions beyond hello memory grant provided by hello extra large resource class.</span></span> <span data-ttu-id="ce89d-173">Si vos partitions de croître au-delà de cette illustration, vous exécutez risque hello pression sur la mémoire, ce qui à son tour entraîne la compression optimale accessible sans.</span><span class="sxs-lookup"><span data-stu-id="ce89d-173">If your partitions grow beyond this figure you run hello risk of memory pressure which in turn leads tooless optimal compression.</span></span>

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

## <a name="partition-switching"></a><span data-ttu-id="ce89d-174">Basculement de partitions</span><span class="sxs-lookup"><span data-stu-id="ce89d-174">Partition switching</span></span>
<span data-ttu-id="ce89d-175">SQL Data Warehouse prend en charge le fractionnement, la fusion et le basculement de partition.</span><span class="sxs-lookup"><span data-stu-id="ce89d-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="ce89d-176">Chacune de ces fonctions est incapable d’à l’aide de hello [ALTER TABLE] [ ALTER TABLE] instruction.</span><span class="sxs-lookup"><span data-stu-id="ce89d-176">Each of these functions is excuted using hello [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="ce89d-177">partitions tooswitch entre deux tables, que vous devez vous assurer que les partitions hello s’aligner sur leurs limites respectifs et que les définitions de table hello correspondent.</span><span class="sxs-lookup"><span data-stu-id="ce89d-177">tooswitch partitions between two tables you must ensure that hello partitions align on their respective boundaries and that hello table definitions match.</span></span> <span data-ttu-id="ce89d-178">Comme les contraintes check ne sont pas disponibles tooenforce hello plage de valeurs dans une table de source de table hello doit contenir hello même des limites de partition en tant que la table cible hello.</span><span class="sxs-lookup"><span data-stu-id="ce89d-178">As check constraints are not available tooenforce hello range of values in a table hello source table must contain hello same partition boundaries as hello target table.</span></span> <span data-ttu-id="ce89d-179">Si cela n’est pas le cas de hello, basculement de partition hello échouera car les métadonnées de partition hello ne seront pas synchronisées.</span><span class="sxs-lookup"><span data-stu-id="ce89d-179">If this is not hello case, then hello partition switch will fail as hello partition metadata will not be synchronized.</span></span>

### <a name="how-toosplit-a-partition-that-contains-data"></a><span data-ttu-id="ce89d-180">Comment toosplit une partition qui contient des données</span><span class="sxs-lookup"><span data-stu-id="ce89d-180">How toosplit a partition that contains data</span></span>
<span data-ttu-id="ce89d-181">Bonjour toosplit méthode la plus efficace une partition qui contient déjà des données est toouse un `CTAS` instruction.</span><span class="sxs-lookup"><span data-stu-id="ce89d-181">hello most efficient method toosplit a partition that already contains data is toouse a `CTAS` statement.</span></span> <span data-ttu-id="ce89d-182">Si la table partitionnée de hello est un index columnstore en cluster puis partition de table hello doit être vide avant elle peut être divisée.</span><span class="sxs-lookup"><span data-stu-id="ce89d-182">If hello partitioned table is a clustered columnstore then hello table partition must be empty before it can be split.</span></span>

<span data-ttu-id="ce89d-183">Voici un exemple de table columnstore partitionnée qui inclut une ligne dans chaque partition :</span><span class="sxs-lookup"><span data-stu-id="ce89d-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

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
> <span data-ttu-id="ce89d-184">Par objet de statistiques création hello, nous nous assurons que ces métadonnées de table sont plus précises.</span><span class="sxs-lookup"><span data-stu-id="ce89d-184">By Creating hello statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="ce89d-185">Si ces statistiques ne sont pas créées, SQL Data Warehouse utilise les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="ce89d-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="ce89d-186">Pour en savoir plus sur les statistiques, consultez la rubrique [Statistiques][statistics].</span><span class="sxs-lookup"><span data-stu-id="ce89d-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="ce89d-187">Nous pouvons ensuite interroger pour le nombre de lignes hello à l’aide de hello `sys.partitions` affichage catalogue :</span><span class="sxs-lookup"><span data-stu-id="ce89d-187">We can then query for hello row count using hello `sys.partitions` catalog view:</span></span>

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

<span data-ttu-id="ce89d-188">Si nous essayons toosplit cette table, nous allons une erreur :</span><span class="sxs-lookup"><span data-stu-id="ce89d-188">If we try toosplit this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="ce89d-189">Msg 35346, niveau 15, état 1, ligne 44 fractionnée de clause d’instruction ALTER PARTITION a échoué, car la partition de hello n’est pas vide.</span><span class="sxs-lookup"><span data-stu-id="ce89d-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because hello partition is not empty.</span></span>  <span data-ttu-id="ce89d-190">Seules les partitions vides peuvent être fractionnées lorsqu’il existe un index columnstore sur la table de hello.</span><span class="sxs-lookup"><span data-stu-id="ce89d-190">Only empty partitions can be split in when a columnstore index exists on hello table.</span></span> <span data-ttu-id="ce89d-191">Envisagez de désactiver l’index columnstore de hello avant d’émettre l’instruction ALTER PARTITION de hello, puis reconstruisez les index columnstore de hello après ALTER PARTITION.</span><span class="sxs-lookup"><span data-stu-id="ce89d-191">Consider disabling hello columnstore index before issuing hello ALTER PARTITION statement, then rebuilding hello columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="ce89d-192">Toutefois, nous pouvons utiliser `CTAS` toocreate un toohold table nouvelle nos données.</span><span class="sxs-lookup"><span data-stu-id="ce89d-192">However, we can use `CTAS` toocreate a new table toohold our data.</span></span>

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

<span data-ttu-id="ce89d-193">Comme les limites de partition hello sont alignés, un commutateur est autorisé.</span><span class="sxs-lookup"><span data-stu-id="ce89d-193">As hello partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="ce89d-194">Cela laisse une table de source de hello avec une partition vide qui nous pouvons fractionnée par la suite.</span><span class="sxs-lookup"><span data-stu-id="ce89d-194">This will leave hello source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="ce89d-195">Tout ce qui reste toodo est tooalign toohello de nos données de partition nouvelles limites à l’aide de `CTAS` et basculez nos données dans la table principale de toohello</span><span class="sxs-lookup"><span data-stu-id="ce89d-195">All that is left toodo is tooalign our data toohello new partition boundaries using `CTAS` and switch our data back in toohello main table</span></span>

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

<span data-ttu-id="ce89d-196">Une fois que vous avez terminé le déplacement des hello de données de hello il s’agit d’une bonne idée toorefresh hello de statistiques sur hello cible table tooensure qu’ils reflètent précisément nouvelle distribution des données hello dans leurs partitions respectifs de hello :</span><span class="sxs-lookup"><span data-stu-id="ce89d-196">Once you have completed hello movement of hello data it is a good idea toorefresh hello statistics on hello target table tooensure they accurately reflect hello new distribution of hello data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="ce89d-197">Contrôle de code source dans le cadre du partitionnement d’une table</span><span class="sxs-lookup"><span data-stu-id="ce89d-197">Table partitioning source control</span></span>
<span data-ttu-id="ce89d-198">tooavoid votre définition de la table à partir de **bullage** dans votre système de contrôle de code source, vous pouvez vouloir hello tooconsider approche :</span><span class="sxs-lookup"><span data-stu-id="ce89d-198">tooavoid your table definition from **rusting** in your source control system you may want tooconsider hello following approach:</span></span>

1. <span data-ttu-id="ce89d-199">Créer la table de hello comme une table partitionnée, mais sans valeurs de partition</span><span class="sxs-lookup"><span data-stu-id="ce89d-199">Create hello table as a partitioned table but with no partition values</span></span>

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

1. <span data-ttu-id="ce89d-200">`SPLIT`table Hello dans le cadre du processus de déploiement hello :</span><span class="sxs-lookup"><span data-stu-id="ce89d-200">`SPLIT` hello table as part of hello deployment process:</span></span>

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

<span data-ttu-id="ce89d-201">Avec cette hello approche code de contrôle de code source reste statique et les valeurs limites partitionnement hello sont autorisées toobe dynamique ; évolution avec l’entrepôt de hello au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="ce89d-201">With this approach hello code in source control remains static and hello partitioning boundary values are allowed toobe dynamic; evolving with hello warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce89d-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ce89d-202">Next steps</span></span>
<span data-ttu-id="ce89d-203">toolearn, voir les articles hello sur [vue d’ensemble de la Table][Overview], [les Types de données de Table][Data Types], [distribution d’une Table] [ Distribute], [L’indexation d’une Table][Index], [gestion de statistiques de Table] [ Statistics] et [ Tables temporaires][Temporary].</span><span class="sxs-lookup"><span data-stu-id="ce89d-203">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="ce89d-204">Pour en savoir plus sur les meilleures pratiques, consultez [Meilleures pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="ce89d-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
