---
title: "Guide de conception pour les tables répliquées - Azure SQL Data Warehouse | Microsoft Docs"
description: "Recommandations relatives à la conception de tables répliquées dans votre schéma Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 437a4f628a343312984d1fa2981df7fa01459e26
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="6eed6-103">Guide de conception pour l’utilisation de tables répliquées dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="6eed6-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="6eed6-104">Cet article vous fournit des recommandations relatives à la conception de tables répliquées dans votre schéma SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6eed6-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="6eed6-105">Utilisez ces recommandations pour améliorer les performances des requêtes en réduisant le déplacement de données et la complexité des requêtes.</span><span class="sxs-lookup"><span data-stu-id="6eed6-105">Use these recommendations to improve query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="6eed6-106">La fonctionnalité de table répliquée est actuellement disponible en préversion publique.</span><span class="sxs-lookup"><span data-stu-id="6eed6-106">The replicated table feature is currently in public preview.</span></span> <span data-ttu-id="6eed6-107">Certains comportements sont susceptibles d’être modifiés.</span><span class="sxs-lookup"><span data-stu-id="6eed6-107">Some behaviors are subject to change.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="6eed6-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6eed6-108">Prerequisites</span></span>
<span data-ttu-id="6eed6-109">Cet article suppose que vous êtes familiarisé avec les concepts de distribution et de déplacement des données dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6eed6-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="6eed6-110">Pour plus d’informations, consultez [Données distribuées](sql-data-warehouse-distributed-data.md).</span><span class="sxs-lookup"><span data-stu-id="6eed6-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="6eed6-111">Dans le cadre de la conception d’une table, essayez d’en savoir autant que possible sur vos données et la façon dont elles sont interrogées.</span><span class="sxs-lookup"><span data-stu-id="6eed6-111">As part of table design, understand as much as possible about your data and how the data is queried.</span></span>  <span data-ttu-id="6eed6-112">Considérez par exemple les questions suivantes :</span><span class="sxs-lookup"><span data-stu-id="6eed6-112">For example, consider these questions:</span></span>

- <span data-ttu-id="6eed6-113">Quelle est la taille de la table ?</span><span class="sxs-lookup"><span data-stu-id="6eed6-113">How large is the table?</span></span>   
- <span data-ttu-id="6eed6-114">Quelle est la fréquence d’actualisation de la table ?</span><span class="sxs-lookup"><span data-stu-id="6eed6-114">How often is the table refreshed?</span></span>   
- <span data-ttu-id="6eed6-115">Est-ce que je dispose de tables de faits et de dimension dans un entrepôt de données ?</span><span class="sxs-lookup"><span data-stu-id="6eed6-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="6eed6-116">Qu’est-ce qu’une table répliquée ?</span><span class="sxs-lookup"><span data-stu-id="6eed6-116">What is a replicated table?</span></span>
<span data-ttu-id="6eed6-117">Une table répliquée possède une copie complète de la table accessible sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="6eed6-117">A replicated table has a full copy of the table accessible on each Compute node.</span></span> <span data-ttu-id="6eed6-118">La réplication d’une table évite le transfert de données entre des nœuds de calcul avant une jointure ou une agrégation.</span><span class="sxs-lookup"><span data-stu-id="6eed6-118">Replicating a table removes the need to transfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="6eed6-119">Étant donné que la table possède plusieurs copies, le fonctionnement des tables répliquées est optimal lorsque la taille de la table est inférieure à 2 Go compressés.</span><span class="sxs-lookup"><span data-stu-id="6eed6-119">Since the table has multiple copies, replicated tables work best when the table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="6eed6-120">Le diagramme suivant illustre une table répliquée accessible sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="6eed6-120">The following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="6eed6-121">Dans SQL Data Warehouse, la table répliquée est entièrement copiée dans une base de données de distribution sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="6eed6-121">In SQL Data Warehouse, the replicated table is fully copied to a distribution database on each Compute node.</span></span> 

<span data-ttu-id="6eed6-122">![Table répliquée](media/guidance-for-using-replicated-tables/replicated-table.png "Table répliquée")</span><span class="sxs-lookup"><span data-stu-id="6eed6-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="6eed6-123">Le fonctionnement des tables répliquées est mieux adapté aux petites tables de dimension dans un schéma en étoile.</span><span class="sxs-lookup"><span data-stu-id="6eed6-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="6eed6-124">Les tables de dimension ont généralement une taille qui permet de stocker et de gérer plusieurs copies.</span><span class="sxs-lookup"><span data-stu-id="6eed6-124">Dimension tables are usually of a size that makes it feasible to store and maintain multiple copies.</span></span> <span data-ttu-id="6eed6-125">Les dimensions stockent des données descriptives qui se modifient lentement, comme le nom et l’adresse du client, ainsi que les détails sur le produit.</span><span class="sxs-lookup"><span data-stu-id="6eed6-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="6eed6-126">La lenteur de la nature changeante des données entraîne moins de reconstructions de la table répliquée.</span><span class="sxs-lookup"><span data-stu-id="6eed6-126">The slowly changing nature of the data leads to fewer rebuilds of the replicated table.</span></span> 

<span data-ttu-id="6eed6-127">Envisagez d’utiliser une table répliquée dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="6eed6-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="6eed6-128">La taille de la table sur le disque est inférieure à 2 Go, quel que soit le nombre de lignes.</span><span class="sxs-lookup"><span data-stu-id="6eed6-128">The table size on disk is less than 2 GB, regardless of the number of rows.</span></span> <span data-ttu-id="6eed6-129">Pour connaître la taille d’une table, vous pouvez utiliser la commande [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) : `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span><span class="sxs-lookup"><span data-stu-id="6eed6-129">To find the size of a table, you can use the [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="6eed6-130">La table est utilisée dans des jointures qui requièrent normalement un déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="6eed6-130">The table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="6eed6-131">Par exemple, une jointure sur des tables distribuées par hachage requiert le déplacement des données lorsque les colonnes de jointure ne correspondent pas à la colonne de distribution.</span><span class="sxs-lookup"><span data-stu-id="6eed6-131">For example, a join on hash-distributed tables requires data movement when the joining columns are not the same distribution column.</span></span> <span data-ttu-id="6eed6-132">Si l’une des tables distribuées par hachage est de petite taille, pensez à utiliser une table répliquée.</span><span class="sxs-lookup"><span data-stu-id="6eed6-132">If one of the hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="6eed6-133">Une jointure sur une table de distribution par tourniquet (round-robin) requiert le déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="6eed6-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="6eed6-134">Nous vous recommandons d’utiliser des tables répliquées au lieu de tables de distribution par tourniquet dans la plupart des cas.</span><span class="sxs-lookup"><span data-stu-id="6eed6-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="6eed6-135">Envisagez de convertir une table distribuée existante en table répliquée dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="6eed6-135">Consider converting an existing distributed table to a replicated table when:</span></span>

- <span data-ttu-id="6eed6-136">Les plans de requêtes utilisent des opérations de déplacement des données qui diffusent les données sur tous les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="6eed6-136">Query plans use data movement operations that broadcast the data to all the Compute nodes.</span></span> <span data-ttu-id="6eed6-137">L’opération BroadcastMoveOperation est coûteuse et ralentit les performances de requête.</span><span class="sxs-lookup"><span data-stu-id="6eed6-137">The BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="6eed6-138">Pour consulter les opérations de déplacement des données dans les plans de requêtes, utilisez [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="6eed6-138">To view data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="6eed6-139">Les tables répliquées ne produisent sans doute pas les meilleurs résultats dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="6eed6-139">Replicated tables may not yield the best query performance when:</span></span>

- <span data-ttu-id="6eed6-140">La table est l’objet d’opérations d’insertion, de mise à jour et de suppression fréquentes.</span><span class="sxs-lookup"><span data-stu-id="6eed6-140">The table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="6eed6-141">Ces opérations DLM (langage de manipulation de données) nécessitent une regénération de la table répliquée.</span><span class="sxs-lookup"><span data-stu-id="6eed6-141">These data manipulation language (DML) operations require a rebuild of the replicated table.</span></span> <span data-ttu-id="6eed6-142">La reconstruction fréquente peut diminuer les performances.</span><span class="sxs-lookup"><span data-stu-id="6eed6-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="6eed6-143">L’entrepôt de données est souvent mis à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="6eed6-143">The data warehouse is scaled frequently.</span></span> <span data-ttu-id="6eed6-144">La mise à l’échelle d’un entrepôt de données modifie le nombre de nœuds de calcul, ce qui entraîne une reconstruction.</span><span class="sxs-lookup"><span data-stu-id="6eed6-144">Scaling a data warehouse changes the number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="6eed6-145">La table comporte un grand nombre de colonnes, mais les opérations de données n’accèdent généralement qu’à un nombre restreint de colonnes.</span><span class="sxs-lookup"><span data-stu-id="6eed6-145">The table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="6eed6-146">Dans ce scénario, au lieu de répliquer la table entière, il peut s’avérer plus efficace de distribuer la table par hachage et de créer ensuite un index sur les colonnes fréquemment sollicitées.</span><span class="sxs-lookup"><span data-stu-id="6eed6-146">In this scenario, instead of replicating the entire table, it might be more effective to hash distribute the table, and then create an index on the frequently accessed columns.</span></span> <span data-ttu-id="6eed6-147">Lorsqu’une requête requiert le déplacement des données, SQL Data Warehouse déplace uniquement les données dans les colonnes demandées.</span><span class="sxs-lookup"><span data-stu-id="6eed6-147">When a query requires data movement, SQL Data Warehouse only moves data in the requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="6eed6-148">Utiliser des tables répliquées avec des prédicats de requête simples</span><span class="sxs-lookup"><span data-stu-id="6eed6-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="6eed6-149">Avant de décider de distribuer ou de répliquer une table, pensez aux types de requêtes que vous projetez d’exécuter sur la table.</span><span class="sxs-lookup"><span data-stu-id="6eed6-149">Before you choose to distribute or replicate a table, think about the types of queries you plan to run against the table.</span></span> <span data-ttu-id="6eed6-150">Lorsque possible,</span><span class="sxs-lookup"><span data-stu-id="6eed6-150">Whenever possible,</span></span>

- <span data-ttu-id="6eed6-151">Utilisez des tables répliquées pour les requêtes avec des prédicats de requête simples, comme l’égalité ou l’inégalité.</span><span class="sxs-lookup"><span data-stu-id="6eed6-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="6eed6-152">Utilisez des tables distribuées pour les requêtes avec des prédicats de requête complexes, comme LIKE ou NOT LIKE.</span><span class="sxs-lookup"><span data-stu-id="6eed6-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="6eed6-153">Les requêtes sollicitant beaucoup le processeur fonctionnent de manière optimale lorsque le travail est réparti entre tous les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="6eed6-153">CPU-intensive queries perform best when the work is distributed across all of the Compute nodes.</span></span> <span data-ttu-id="6eed6-154">Par exemple, les requêtes qui exécutent des calculs sur chaque ligne d’une table fonctionnent mieux sur les tables distribués que sur les tables répliquées.</span><span class="sxs-lookup"><span data-stu-id="6eed6-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="6eed6-155">Étant donné qu’une table répliquée est entièrement stockée sur chaque nœud de calcul, une requête sollicitant beaucoup le processeur sur une table répliquée s’exécute sur la table entière sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="6eed6-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against the entire table on every Compute node.</span></span> <span data-ttu-id="6eed6-156">Le calcul supplémentaire peut ralentir les performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="6eed6-156">The extra computation can slow query performance.</span></span>

<span data-ttu-id="6eed6-157">Par exemple, cette requête comporte un prédicat complexe.</span><span class="sxs-lookup"><span data-stu-id="6eed6-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="6eed6-158">Elle s’exécute plus rapidement lorsque le fournisseur est une table distribuée au lieu d’une table répliquée.</span><span class="sxs-lookup"><span data-stu-id="6eed6-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="6eed6-159">Dans cet exemple, le fournisseur peut être distribué par hachage ou distribué par tourniquet.</span><span class="sxs-lookup"><span data-stu-id="6eed6-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-to-replicated-tables"></a><span data-ttu-id="6eed6-160">Convertir les tables de distribution par tourniquet (round-robin) en tables répliquées</span><span class="sxs-lookup"><span data-stu-id="6eed6-160">Convert existing round-robin tables to replicated tables</span></span>
<span data-ttu-id="6eed6-161">Si vous avez déjà des tables de distribution par tourniquet, nous vous recommandons de les convertir en tables répliquées si elles sont conformes aux critères décrits dans cet article.</span><span class="sxs-lookup"><span data-stu-id="6eed6-161">If you already have round-robin tables, we recommend converting them to replicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="6eed6-162">Les tables répliquées ont de meilleures performances que les tables de distribution par tourniquet, car elles éliminent le déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="6eed6-162">Replicated tables improve performance over round-robin tables because they eliminate the need for data movement.</span></span>  <span data-ttu-id="6eed6-163">Une table de distribution par tourniquet requiert toujours le déplacement des données pour les jointures.</span><span class="sxs-lookup"><span data-stu-id="6eed6-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="6eed6-164">Cet exemple utilise [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) pour modifier la table DimSalesTerritory en une table répliquée.</span><span class="sxs-lookup"><span data-stu-id="6eed6-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) to change the DimSalesTerritory table to a replicated table.</span></span> <span data-ttu-id="6eed6-165">Cet exemple fonctionne que la table DimSalesTerritory soit distribuée par hachage ou par tourniquet.</span><span class="sxs-lookup"><span data-stu-id="6eed6-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="6eed6-166">Exemple de performances de requête pour une table de distribution par tourniquet et une table répliquée</span><span class="sxs-lookup"><span data-stu-id="6eed6-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="6eed6-167">Une table répliquée ne nécessite pas le déplacement des données pour les jointures, car la table entière est déjà présente sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="6eed6-167">A replicated table does not require any data movement for joins because the entire table is already present on each Compute node.</span></span> <span data-ttu-id="6eed6-168">Si les tables de dimension sont des tables distribuées par tourniquet, une jointure copie entièrement la table de dimension sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="6eed6-168">If the dimension tables are round-robin distributed, a join copies the dimension table in full to each Compute node.</span></span> <span data-ttu-id="6eed6-169">Pour déplacer les données, le plan de requête contient une opération appelée BroadcastMoveOperation.</span><span class="sxs-lookup"><span data-stu-id="6eed6-169">To move the data, the query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="6eed6-170">Ce type d’opération de déplacement des données ralentit les performances des requêtes. Il n’est pas utilisé par les tables répliquées.</span><span class="sxs-lookup"><span data-stu-id="6eed6-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="6eed6-171">Pour afficher les étapes relatives au plan de requête, utilisez la vue catalogue système [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="6eed6-171">To view query plan steps, use the [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="6eed6-172">Par exemple, dans la requête suivante sur le schéma AdventureWorks, la table ` FactInternetSales` est distribuée par hachage.</span><span class="sxs-lookup"><span data-stu-id="6eed6-172">For example, in following query against the AdventureWorks schema, the ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="6eed6-173">Les tables `DimDate` et `DimSalesTerritory` sont des tables de dimension plus petites.</span><span class="sxs-lookup"><span data-stu-id="6eed6-173">The `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="6eed6-174">Cette requête retourne le total des ventes en Amérique du Nord pour l’année fiscale 2004 :</span><span class="sxs-lookup"><span data-stu-id="6eed6-174">This query returns the total sales in North America for fiscal year 2004:</span></span>
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
<span data-ttu-id="6eed6-175">Nous avons recréé les tables `DimDate` et `DimSalesTerritory` en tant que tables de distribution par tourniquet.</span><span class="sxs-lookup"><span data-stu-id="6eed6-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="6eed6-176">Par conséquent, la requête affichait le plan de requête suivant, avec plusieurs opérations de déplacement pour la diffusion :</span><span class="sxs-lookup"><span data-stu-id="6eed6-176">As a result, the query showed the following query plan, which has multiple broadcast move operations:</span></span> 
 
![Plan de requête de type tourniquet (round robin)](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="6eed6-178">Nous avons recréé les tables `DimDate` et `DimSalesTerritory` en tant que tables répliquées et réexécuté la requête.</span><span class="sxs-lookup"><span data-stu-id="6eed6-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran the query again.</span></span> <span data-ttu-id="6eed6-179">Le plan de requête qui en résulte est beaucoup plus court et ne contient pas de mouvements de diffusion.</span><span class="sxs-lookup"><span data-stu-id="6eed6-179">The resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![Plan de requête répliqué](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="6eed6-181">Considérations relatives aux performances pour la modification des tables répliquées</span><span class="sxs-lookup"><span data-stu-id="6eed6-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="6eed6-182">SQL Data Warehouse implémente une table répliquée en conservant une version principale de la table.</span><span class="sxs-lookup"><span data-stu-id="6eed6-182">SQL Data Warehouse implements a replicated table by maintaining a master version of the table.</span></span> <span data-ttu-id="6eed6-183">Il copie la version principale dans une base de données de distribution sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="6eed6-183">It copies the master version to one distribution database on each Compute node.</span></span> <span data-ttu-id="6eed6-184">En cas de modification, SQL Data Warehouse met d’abord à jour la table principale.</span><span class="sxs-lookup"><span data-stu-id="6eed6-184">When there is a change, SQL Data Warehouse first updates the master table.</span></span> <span data-ttu-id="6eed6-185">Puis, il demande une reconstruction des tables sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="6eed6-185">Then it requires a rebuild of the tables on each Compute node.</span></span> <span data-ttu-id="6eed6-186">Une reconstruction d’une table répliquée implique la copie de la table sur chaque nœud de calcul et la reconstruction des index.</span><span class="sxs-lookup"><span data-stu-id="6eed6-186">A rebuild of a replicated table includes copying the table to each Compute node and then rebuilding the indexes.</span></span>

<span data-ttu-id="6eed6-187">Les reconstructions sont requises après les événements suivants :</span><span class="sxs-lookup"><span data-stu-id="6eed6-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="6eed6-188">Des données sont chargées ou modifiées</span><span class="sxs-lookup"><span data-stu-id="6eed6-188">Data is loaded or modified</span></span>
- <span data-ttu-id="6eed6-189">L’entrepôt de données est mis à l’échelle avec un paramètre DWU différent</span><span class="sxs-lookup"><span data-stu-id="6eed6-189">The data warehouse is scaled to a different DWU setting</span></span>
- <span data-ttu-id="6eed6-190">La définition de la table est mise à jour</span><span class="sxs-lookup"><span data-stu-id="6eed6-190">Table definition is updated</span></span>

<span data-ttu-id="6eed6-191">Les reconstructions ne sont pas requises après les événements suivants :</span><span class="sxs-lookup"><span data-stu-id="6eed6-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="6eed6-192">Opération de suspension</span><span class="sxs-lookup"><span data-stu-id="6eed6-192">Pause operation</span></span>
- <span data-ttu-id="6eed6-193">Opération de reprise</span><span class="sxs-lookup"><span data-stu-id="6eed6-193">Resume operation</span></span>

<span data-ttu-id="6eed6-194">La reconstruction ne se produit pas immédiatement après la modification des données.</span><span class="sxs-lookup"><span data-stu-id="6eed6-194">The rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="6eed6-195">Au lieu de cela, la reconstruction est déclenchée la première fois qu’une requête est sélectionnée à partir de la table.</span><span class="sxs-lookup"><span data-stu-id="6eed6-195">Instead, the rebuild is triggered the first time a query selects from the table.</span></span>  <span data-ttu-id="6eed6-196">L’instruction select initiale de la table contient les étapes pour reconstruire la table répliquée.</span><span class="sxs-lookup"><span data-stu-id="6eed6-196">Within the initial select statement from the table are steps to rebuild the replicated table.</span></span>  <span data-ttu-id="6eed6-197">Étant donné que la reconstruction est effectuée dans la requête, l’impact sur l’instruction select initiale peut être significatif selon la taille de la table.</span><span class="sxs-lookup"><span data-stu-id="6eed6-197">Because the rebuild is done within the query, the impact to the initial select statement could be significant depending on the size of the table.</span></span>  <span data-ttu-id="6eed6-198">Si plusieurs tables répliquées nécessitant une reconstruction sont impliquées, chaque copie est reconstruite en série en fonction des étapes de l’instruction.</span><span class="sxs-lookup"><span data-stu-id="6eed6-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within the statement.</span></span>  <span data-ttu-id="6eed6-199">Pour maintenir la cohérence des données pendant la reconstruction de la table répliquée, un verrou exclusif est placé sur la table.</span><span class="sxs-lookup"><span data-stu-id="6eed6-199">To maintain data consistency during the rebuild of the replicated table an exclusive lock is taken on the table.</span></span>  <span data-ttu-id="6eed6-200">Le verrou empêche tout accès à la table pendant la durée de la reconstruction.</span><span class="sxs-lookup"><span data-stu-id="6eed6-200">The lock prevents all access to the table for the duration of the rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="6eed6-201">Utilisation restrictive des index</span><span class="sxs-lookup"><span data-stu-id="6eed6-201">Use indexes conservatively</span></span>
<span data-ttu-id="6eed6-202">Les pratiques d’indexation standard s’appliquent aux tables répliquées.</span><span class="sxs-lookup"><span data-stu-id="6eed6-202">Standard indexing practices apply to replicated tables.</span></span> <span data-ttu-id="6eed6-203">SQL Data Warehouse reconstruit chaque index de table répliquée dans le cadre de la reconstruction.</span><span class="sxs-lookup"><span data-stu-id="6eed6-203">SQL Data Warehouse rebuilds each replicated table index as part of the rebuild.</span></span> <span data-ttu-id="6eed6-204">Utilisez les index uniquement lorsque le gain de performances compense le coût de reconstruction des index.</span><span class="sxs-lookup"><span data-stu-id="6eed6-204">Only use indexes when the performance gain outweighs the cost of rebuilding the indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="6eed6-205">Chargements de données par lots</span><span class="sxs-lookup"><span data-stu-id="6eed6-205">Batch data loads</span></span>
<span data-ttu-id="6eed6-206">Lors du chargement de données dans des tables répliquées, essayez de réduire les reconstructions en regroupant les chargements par lots.</span><span class="sxs-lookup"><span data-stu-id="6eed6-206">When loading data into replicated tables, try to minimize rebuilds by batching loads together.</span></span> <span data-ttu-id="6eed6-207">Effectuez tous les chargements par lots avant d’exécuter des instructions select.</span><span class="sxs-lookup"><span data-stu-id="6eed6-207">Perform all the batched loads before running select statements.</span></span>

<span data-ttu-id="6eed6-208">Par exemple, ce modèle de chargement charge les données à partir de quatre sources et appelle quatre reconstructions.</span><span class="sxs-lookup"><span data-stu-id="6eed6-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="6eed6-209">Charger à partir de la source 1.</span><span class="sxs-lookup"><span data-stu-id="6eed6-209">Load from source 1.</span></span>
- <span data-ttu-id="6eed6-210">Instruction select qui déclenche la reconstruction 1.</span><span class="sxs-lookup"><span data-stu-id="6eed6-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="6eed6-211">Charger à partir de la source 2.</span><span class="sxs-lookup"><span data-stu-id="6eed6-211">Load from source 2.</span></span>
- <span data-ttu-id="6eed6-212">Instruction select qui déclenche la reconstruction 2.</span><span class="sxs-lookup"><span data-stu-id="6eed6-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="6eed6-213">Charger à partir de la source 3.</span><span class="sxs-lookup"><span data-stu-id="6eed6-213">Load from source 3.</span></span>
- <span data-ttu-id="6eed6-214">Instruction select qui déclenche la reconstruction 3.</span><span class="sxs-lookup"><span data-stu-id="6eed6-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="6eed6-215">Charger à partir de la source 4.</span><span class="sxs-lookup"><span data-stu-id="6eed6-215">Load from source 4.</span></span>
- <span data-ttu-id="6eed6-216">Instruction select qui déclenche la reconstruction 4.</span><span class="sxs-lookup"><span data-stu-id="6eed6-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="6eed6-217">Par exemple, ce modèle de chargement charge les données à partir de quatre sources mais n’appelle qu’une seule reconstruction.</span><span class="sxs-lookup"><span data-stu-id="6eed6-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="6eed6-218">Charger à partir de la source 1.</span><span class="sxs-lookup"><span data-stu-id="6eed6-218">Load from source 1.</span></span>
- <span data-ttu-id="6eed6-219">Charger à partir de la source 2.</span><span class="sxs-lookup"><span data-stu-id="6eed6-219">Load from source 2.</span></span>
- <span data-ttu-id="6eed6-220">Charger à partir de la source 3.</span><span class="sxs-lookup"><span data-stu-id="6eed6-220">Load from source 3.</span></span>
- <span data-ttu-id="6eed6-221">Charger à partir de la source 4.</span><span class="sxs-lookup"><span data-stu-id="6eed6-221">Load from source 4.</span></span>
- <span data-ttu-id="6eed6-222">Instruction select qui déclenche la reconstruction.</span><span class="sxs-lookup"><span data-stu-id="6eed6-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="6eed6-223">Reconstruire une table répliquée après un chargement par lots</span><span class="sxs-lookup"><span data-stu-id="6eed6-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="6eed6-224">Pour garantir des temps d’exécution de requête cohérents, nous vous recommandons de forcer une actualisation des tables répliquées après un chargement par lots.</span><span class="sxs-lookup"><span data-stu-id="6eed6-224">To ensure consistent query execution times, we recommend forcing a refresh of the replicated tables after a batch load.</span></span> <span data-ttu-id="6eed6-225">Sinon, la première requête doit attendre que les tables s’actualisent, ce qui implique la reconstruction des index.</span><span class="sxs-lookup"><span data-stu-id="6eed6-225">Otherwise, the first query must wait for the tables to refresh, which includes rebuilding the indexes.</span></span> <span data-ttu-id="6eed6-226">Selon la taille et le nombre des tables répliquées affectées, l’impact sur les performances peut être important.</span><span class="sxs-lookup"><span data-stu-id="6eed6-226">Depending on the size and number of replicated tables affected, the performance impact can be significant.</span></span>  

<span data-ttu-id="6eed6-227">Cette requête utilise le DMV [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) pour répertorier les tables répliquées qui ont été modifiées mais pas reconstruites.</span><span class="sxs-lookup"><span data-stu-id="6eed6-227">This query uses the [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV to list the replicated tables that have been modified, but not rebuilt.</span></span>

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
<span data-ttu-id="6eed6-228">Pour forcer une reconstruction, exécutez l’instruction suivante sur chaque table dans la sortie précédente.</span><span class="sxs-lookup"><span data-stu-id="6eed6-228">To force a rebuild, run the following statement on each table in the preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="6eed6-229">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6eed6-229">Next steps</span></span> 
<span data-ttu-id="6eed6-230">Pour créer une table répliquée, utilisez l’une de ces instructions :</span><span class="sxs-lookup"><span data-stu-id="6eed6-230">To create a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="6eed6-231">CREATE TABLE (Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="6eed6-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="6eed6-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="6eed6-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="6eed6-233">Pour une vue d’ensemble des tables distribuées, consultez [Tables distribuées](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="6eed6-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



