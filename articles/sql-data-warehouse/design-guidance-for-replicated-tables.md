---
title: "conseils d’aaaDesign pour les tables répliquées - Azure SQL Data Warehouse | Documents Microsoft"
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
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="5c93f-103">Guide de conception pour l’utilisation de tables répliquées dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5c93f-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="5c93f-104">Cet article vous fournit des recommandations relatives à la conception de tables répliquées dans votre schéma SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5c93f-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="5c93f-105">Utilisez ces performances des requêtes tooimprove recommandations en réduisant la complexité de requête et de déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="5c93f-105">Use these recommendations tooimprove query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="5c93f-106">fonctionnalité de table répliquée Hello n’est actuellement en version préliminaire publique.</span><span class="sxs-lookup"><span data-stu-id="5c93f-106">hello replicated table feature is currently in public preview.</span></span> <span data-ttu-id="5c93f-107">Certains comportements sont toochange de sujet.</span><span class="sxs-lookup"><span data-stu-id="5c93f-107">Some behaviors are subject toochange.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="5c93f-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5c93f-108">Prerequisites</span></span>
<span data-ttu-id="5c93f-109">Cet article suppose que vous êtes familiarisé avec les concepts de distribution et de déplacement des données dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5c93f-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="5c93f-110">Pour plus d’informations, consultez [Données distribuées](sql-data-warehouse-distributed-data.md).</span><span class="sxs-lookup"><span data-stu-id="5c93f-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="5c93f-111">Dans le cadre de la création de table, comprendre autant que possible sur vos données et la façon dont les données de salutation sont interrogées.</span><span class="sxs-lookup"><span data-stu-id="5c93f-111">As part of table design, understand as much as possible about your data and how hello data is queried.</span></span>  <span data-ttu-id="5c93f-112">Considérez par exemple les questions suivantes :</span><span class="sxs-lookup"><span data-stu-id="5c93f-112">For example, consider these questions:</span></span>

- <span data-ttu-id="5c93f-113">La taille est la table de hello ?</span><span class="sxs-lookup"><span data-stu-id="5c93f-113">How large is hello table?</span></span>   
- <span data-ttu-id="5c93f-114">La fréquence d’actualisation de table de hello</span><span class="sxs-lookup"><span data-stu-id="5c93f-114">How often is hello table refreshed?</span></span>   
- <span data-ttu-id="5c93f-115">Est-ce que je dispose de tables de faits et de dimension dans un entrepôt de données ?</span><span class="sxs-lookup"><span data-stu-id="5c93f-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="5c93f-116">Qu’est-ce qu’une table répliquée ?</span><span class="sxs-lookup"><span data-stu-id="5c93f-116">What is a replicated table?</span></span>
<span data-ttu-id="5c93f-117">Une table répliquée possède une copie complète de la table hello accessible sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="5c93f-117">A replicated table has a full copy of hello table accessible on each Compute node.</span></span> <span data-ttu-id="5c93f-118">Réplication d’une table supprime les données de tootransfer besoin de hello entre les nœuds de calcul avant une jointure ou une agrégation.</span><span class="sxs-lookup"><span data-stu-id="5c93f-118">Replicating a table removes hello need tootransfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="5c93f-119">Étant donné que la table de hello a plusieurs copies, les tables répliquées convient mieux lorsque la taille de la table hello est inférieure à 2 Go compressé.</span><span class="sxs-lookup"><span data-stu-id="5c93f-119">Since hello table has multiple copies, replicated tables work best when hello table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="5c93f-120">Hello diagramme suivant illustre une table répliquée est accessible sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="5c93f-120">hello following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="5c93f-121">Dans l’entrepôt de données SQL, répliquée hello est la base de données de distribution tooa entièrement copiée sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="5c93f-121">In SQL Data Warehouse, hello replicated table is fully copied tooa distribution database on each Compute node.</span></span> 

<span data-ttu-id="5c93f-122">![Table répliquée](media/guidance-for-using-replicated-tables/replicated-table.png "Table répliquée")</span><span class="sxs-lookup"><span data-stu-id="5c93f-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="5c93f-123">Le fonctionnement des tables répliquées est mieux adapté aux petites tables de dimension dans un schéma en étoile.</span><span class="sxs-lookup"><span data-stu-id="5c93f-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="5c93f-124">Tables de dimension sont généralement d’une taille qui rend possible toostore et maintenir plusieurs copies.</span><span class="sxs-lookup"><span data-stu-id="5c93f-124">Dimension tables are usually of a size that makes it feasible toostore and maintain multiple copies.</span></span> <span data-ttu-id="5c93f-125">Les dimensions stockent des données descriptives qui se modifient lentement, comme le nom et l’adresse du client, ainsi que les détails sur le produit.</span><span class="sxs-lookup"><span data-stu-id="5c93f-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="5c93f-126">Hello variation nature des données de hello entraîne les reconstructions toofewer de la table répliquée de hello.</span><span class="sxs-lookup"><span data-stu-id="5c93f-126">hello slowly changing nature of hello data leads toofewer rebuilds of hello replicated table.</span></span> 

<span data-ttu-id="5c93f-127">Envisagez d’utiliser une table répliquée dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="5c93f-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="5c93f-128">taille de la table Hello sur le disque est inférieur à 2 Go, quelle que soit le nombre de hello de lignes.</span><span class="sxs-lookup"><span data-stu-id="5c93f-128">hello table size on disk is less than 2 GB, regardless of hello number of rows.</span></span> <span data-ttu-id="5c93f-129">taille de hello toofind d’une table, vous pouvez utiliser hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) commande : `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span><span class="sxs-lookup"><span data-stu-id="5c93f-129">toofind hello size of a table, you can use hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="5c93f-130">table de Hello est utilisée dans les jointures qui requièrent normalement un déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="5c93f-130">hello table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="5c93f-131">Par exemple, une jointure sur les tables de hachage distribué requiert le déplacement des données lorsque les colonnes de jointure hello sont hello pas la même colonne de distribution.</span><span class="sxs-lookup"><span data-stu-id="5c93f-131">For example, a join on hash-distributed tables requires data movement when hello joining columns are not hello same distribution column.</span></span> <span data-ttu-id="5c93f-132">Si une des tables de hachage distribué hello est petite, considérez une table répliquée.</span><span class="sxs-lookup"><span data-stu-id="5c93f-132">If one of hello hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="5c93f-133">Une jointure sur une table de distribution par tourniquet (round-robin) requiert le déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="5c93f-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="5c93f-134">Nous vous recommandons d’utiliser des tables répliquées au lieu de tables de distribution par tourniquet dans la plupart des cas.</span><span class="sxs-lookup"><span data-stu-id="5c93f-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="5c93f-135">Envisagez de convertir un existant distributed tooa table répliquée table lorsque :</span><span class="sxs-lookup"><span data-stu-id="5c93f-135">Consider converting an existing distributed table tooa replicated table when:</span></span>

- <span data-ttu-id="5c93f-136">Opérations de déplacement de données utilisez qui diffusent des nœuds de calcul hello hello données tooall les plans de requête.</span><span class="sxs-lookup"><span data-stu-id="5c93f-136">Query plans use data movement operations that broadcast hello data tooall hello Compute nodes.</span></span> <span data-ttu-id="5c93f-137">Hello BroadcastMoveOperation est coûteuse et ralentit les performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="5c93f-137">hello BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="5c93f-138">tooview les opérations de déplacement de données dans les plans de requête, utilisez [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="5c93f-138">tooview data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="5c93f-139">Les tables répliquées ne peuvent pas produire de meilleures performances des requêtes hello lorsque :</span><span class="sxs-lookup"><span data-stu-id="5c93f-139">Replicated tables may not yield hello best query performance when:</span></span>

- <span data-ttu-id="5c93f-140">table de Hello a fréquentes d’insertion, mise à jour et les opérations de suppression.</span><span class="sxs-lookup"><span data-stu-id="5c93f-140">hello table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="5c93f-141">Ces opérations data manipulation language (DML) nécessitent une régénération de la table de hello répliquée.</span><span class="sxs-lookup"><span data-stu-id="5c93f-141">These data manipulation language (DML) operations require a rebuild of hello replicated table.</span></span> <span data-ttu-id="5c93f-142">La reconstruction fréquente peut diminuer les performances.</span><span class="sxs-lookup"><span data-stu-id="5c93f-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="5c93f-143">entrepôt de données Hello est souvent à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="5c93f-143">hello data warehouse is scaled frequently.</span></span> <span data-ttu-id="5c93f-144">Mise à l’échelle d’un entrepôt de données modifie nombre hello de nœuds de calcul, ce qui entraîne une régénération.</span><span class="sxs-lookup"><span data-stu-id="5c93f-144">Scaling a data warehouse changes hello number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="5c93f-145">table de Hello possède un grand nombre de colonnes, mais les opérations de données généralement accéder uniquement à un petit nombre de colonnes.</span><span class="sxs-lookup"><span data-stu-id="5c93f-145">hello table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="5c93f-146">Dans ce scénario, au lieu de répliquer la table entière de hello, il peut être plus efficace toohash distribuer les table hello et ensuite créer un index sur les colonnes hello fréquemment.</span><span class="sxs-lookup"><span data-stu-id="5c93f-146">In this scenario, instead of replicating hello entire table, it might be more effective toohash distribute hello table, and then create an index on hello frequently accessed columns.</span></span> <span data-ttu-id="5c93f-147">Quand une requête requiert le déplacement des données, l’entrepôt de données SQL que déplace les données Bonjour demandé de colonnes.</span><span class="sxs-lookup"><span data-stu-id="5c93f-147">When a query requires data movement, SQL Data Warehouse only moves data in hello requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="5c93f-148">Utiliser des tables répliquées avec des prédicats de requête simples</span><span class="sxs-lookup"><span data-stu-id="5c93f-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="5c93f-149">Avant de choisir toodistribute ou répliquer une table, pensez aux types de requêtes que vous projetez toorun par rapport à la table de hello hello.</span><span class="sxs-lookup"><span data-stu-id="5c93f-149">Before you choose toodistribute or replicate a table, think about hello types of queries you plan toorun against hello table.</span></span> <span data-ttu-id="5c93f-150">Lorsque possible,</span><span class="sxs-lookup"><span data-stu-id="5c93f-150">Whenever possible,</span></span>

- <span data-ttu-id="5c93f-151">Utilisez des tables répliquées pour les requêtes avec des prédicats de requête simples, comme l’égalité ou l’inégalité.</span><span class="sxs-lookup"><span data-stu-id="5c93f-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="5c93f-152">Utilisez des tables distribuées pour les requêtes avec des prédicats de requête complexes, comme LIKE ou NOT LIKE.</span><span class="sxs-lookup"><span data-stu-id="5c93f-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="5c93f-153">Les requêtes sollicitant beaucoup le processeur fonctionnent de manière optimale lors de la charge de travail hello est répartie entre tous les nœuds de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="5c93f-153">CPU-intensive queries perform best when hello work is distributed across all of hello Compute nodes.</span></span> <span data-ttu-id="5c93f-154">Par exemple, les requêtes qui exécutent des calculs sur chaque ligne d’une table fonctionnent mieux sur les tables distribués que sur les tables répliquées.</span><span class="sxs-lookup"><span data-stu-id="5c93f-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="5c93f-155">Étant donné qu’une table répliquée est stockée dans son intégralité sur chaque nœud de calcul, une requête de gourmande en ressources processeur sur une table répliquée s’exécute par rapport à la totalité de la table hello sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="5c93f-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against hello entire table on every Compute node.</span></span> <span data-ttu-id="5c93f-156">Hello calcul supplémentaire peut ralentir les performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="5c93f-156">hello extra computation can slow query performance.</span></span>

<span data-ttu-id="5c93f-157">Par exemple, cette requête comporte un prédicat complexe.</span><span class="sxs-lookup"><span data-stu-id="5c93f-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="5c93f-158">Elle s’exécute plus rapidement lorsque le fournisseur est une table distribuée au lieu d’une table répliquée.</span><span class="sxs-lookup"><span data-stu-id="5c93f-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="5c93f-159">Dans cet exemple, le fournisseur peut être distribué par hachage ou distribué par tourniquet.</span><span class="sxs-lookup"><span data-stu-id="5c93f-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a><span data-ttu-id="5c93f-160">Convertir les tables de tooreplicated alternée tables existantes</span><span class="sxs-lookup"><span data-stu-id="5c93f-160">Convert existing round-robin tables tooreplicated tables</span></span>
<span data-ttu-id="5c93f-161">Si vous avez déjà des tables de tourniquet, nous vous recommandons en les convertissant tooreplicated tables si elles répondent aux critères décrites dans cet article.</span><span class="sxs-lookup"><span data-stu-id="5c93f-161">If you already have round-robin tables, we recommend converting them tooreplicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="5c93f-162">Les tables répliquées améliorent les performances sur les tables de tourniquet, car celles-ci éliminent le besoin de hello pour le déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="5c93f-162">Replicated tables improve performance over round-robin tables because they eliminate hello need for data movement.</span></span>  <span data-ttu-id="5c93f-163">Une table de distribution par tourniquet requiert toujours le déplacement des données pour les jointures.</span><span class="sxs-lookup"><span data-stu-id="5c93f-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="5c93f-164">Cet exemple utilise [SACT](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory table tooa de table répliquée.</span><span class="sxs-lookup"><span data-stu-id="5c93f-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory table tooa replicated table.</span></span> <span data-ttu-id="5c93f-165">Cet exemple fonctionne que la table DimSalesTerritory soit distribuée par hachage ou par tourniquet.</span><span class="sxs-lookup"><span data-stu-id="5c93f-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

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
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="5c93f-166">Exemple de performances de requête pour une table de distribution par tourniquet et une table répliquée</span><span class="sxs-lookup"><span data-stu-id="5c93f-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="5c93f-167">Une table répliquée ne nécessite pas de tout déplacement de données pour les jointures étant donné que la totalité de la table hello est déjà présent sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="5c93f-167">A replicated table does not require any data movement for joins because hello entire table is already present on each Compute node.</span></span> <span data-ttu-id="5c93f-168">Si les tables de dimension hello sont tourniquet distribué, une jointure copie table de dimension hello tooeach complète de nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="5c93f-168">If hello dimension tables are round-robin distributed, a join copies hello dimension table in full tooeach Compute node.</span></span> <span data-ttu-id="5c93f-169">les données de salutation toomove, plan de requête hello contient une opération appelée BroadcastMoveOperation.</span><span class="sxs-lookup"><span data-stu-id="5c93f-169">toomove hello data, hello query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="5c93f-170">Ce type d’opération de déplacement des données ralentit les performances des requêtes. Il n’est pas utilisé par les tables répliquées.</span><span class="sxs-lookup"><span data-stu-id="5c93f-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="5c93f-171">étapes du plan de requête de tooview, utilisez hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) affichage catalogue système.</span><span class="sxs-lookup"><span data-stu-id="5c93f-171">tooview query plan steps, use hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="5c93f-172">Par exemple, dans la requête suivante sur le schéma d’AdventureWorks hello, hello ` FactInternetSales` table est distribué de hachage.</span><span class="sxs-lookup"><span data-stu-id="5c93f-172">For example, in following query against hello AdventureWorks schema, hello ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="5c93f-173">Hello `DimDate` et `DimSalesTerritory` sont des tables de dimension plus petites.</span><span class="sxs-lookup"><span data-stu-id="5c93f-173">hello `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="5c93f-174">Cette requête retourne les ventes totales hello en Amérique du Nord pour l’année fiscale 2004 :</span><span class="sxs-lookup"><span data-stu-id="5c93f-174">This query returns hello total sales in North America for fiscal year 2004:</span></span>
 
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
<span data-ttu-id="5c93f-175">Nous avons recréé les tables `DimDate` et `DimSalesTerritory` en tant que tables de distribution par tourniquet.</span><span class="sxs-lookup"><span data-stu-id="5c93f-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="5c93f-176">Par conséquent, les requêtes hello ont montré hello suivant le plan de requête, ce qui a diffusion plusieurs opérations de déplacement :</span><span class="sxs-lookup"><span data-stu-id="5c93f-176">As a result, hello query showed hello following query plan, which has multiple broadcast move operations:</span></span> 
 
![Plan de requête de type tourniquet (round robin)](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="5c93f-178">Nous recréée `DimDate` et `DimSalesTerritory` comme des tables répliquées et exécution de requête de hello à nouveau.</span><span class="sxs-lookup"><span data-stu-id="5c93f-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran hello query again.</span></span> <span data-ttu-id="5c93f-179">plan de requête résultant Hello est beaucoup plus courte et ne pas avoir une diffusion se déplace.</span><span class="sxs-lookup"><span data-stu-id="5c93f-179">hello resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![Plan de requête répliqué](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="5c93f-181">Considérations relatives aux performances pour la modification des tables répliquées</span><span class="sxs-lookup"><span data-stu-id="5c93f-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="5c93f-182">SQL Data Warehouse implémente une table répliquée en conservant une copie principale de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="5c93f-182">SQL Data Warehouse implements a replicated table by maintaining a master version of hello table.</span></span> <span data-ttu-id="5c93f-183">Il copie la base de données de distribution de hello version maître tooone sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="5c93f-183">It copies hello master version tooone distribution database on each Compute node.</span></span> <span data-ttu-id="5c93f-184">Lorsqu’il existe une modification, l’entrepôt de données SQL met à jour table principale de hello en premier.</span><span class="sxs-lookup"><span data-stu-id="5c93f-184">When there is a change, SQL Data Warehouse first updates hello master table.</span></span> <span data-ttu-id="5c93f-185">Il requiert une régénération des tables hello sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="5c93f-185">Then it requires a rebuild of hello tables on each Compute node.</span></span> <span data-ttu-id="5c93f-186">Une reconstruction d’une table répliquée inclut copie le nœud de calcul tooeach hello table et la reconstruction des index de hello.</span><span class="sxs-lookup"><span data-stu-id="5c93f-186">A rebuild of a replicated table includes copying hello table tooeach Compute node and then rebuilding hello indexes.</span></span>

<span data-ttu-id="5c93f-187">Les reconstructions sont requises après les événements suivants :</span><span class="sxs-lookup"><span data-stu-id="5c93f-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="5c93f-188">Des données sont chargées ou modifiées</span><span class="sxs-lookup"><span data-stu-id="5c93f-188">Data is loaded or modified</span></span>
- <span data-ttu-id="5c93f-189">entrepôt de données Hello est mis à l’échelle tooa valeur dwu différents</span><span class="sxs-lookup"><span data-stu-id="5c93f-189">hello data warehouse is scaled tooa different DWU setting</span></span>
- <span data-ttu-id="5c93f-190">La définition de la table est mise à jour</span><span class="sxs-lookup"><span data-stu-id="5c93f-190">Table definition is updated</span></span>

<span data-ttu-id="5c93f-191">Les reconstructions ne sont pas requises après les événements suivants :</span><span class="sxs-lookup"><span data-stu-id="5c93f-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="5c93f-192">Opération de suspension</span><span class="sxs-lookup"><span data-stu-id="5c93f-192">Pause operation</span></span>
- <span data-ttu-id="5c93f-193">Opération de reprise</span><span class="sxs-lookup"><span data-stu-id="5c93f-193">Resume operation</span></span>

<span data-ttu-id="5c93f-194">reconstruction de Hello ne se produit pas immédiatement après la modification des données.</span><span class="sxs-lookup"><span data-stu-id="5c93f-194">hello rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="5c93f-195">Au lieu de cela, hello reconstruction est déclenchée hello la première fois une requête sélectionne à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="5c93f-195">Instead, hello rebuild is triggered hello first time a query selects from hello table.</span></span>  <span data-ttu-id="5c93f-196">Dans l’instruction select de hello initiale à partir de la table de hello sont étapes toorebuild hello répliquée.</span><span class="sxs-lookup"><span data-stu-id="5c93f-196">Within hello initial select statement from hello table are steps toorebuild hello replicated table.</span></span>  <span data-ttu-id="5c93f-197">Hello régénération est effectuée au sein de la requête de hello, instruction select initiale toohello hello impact peut être significative selon la taille de hello de table de hello.</span><span class="sxs-lookup"><span data-stu-id="5c93f-197">Because hello rebuild is done within hello query, hello impact toohello initial select statement could be significant depending on hello size of hello table.</span></span>  <span data-ttu-id="5c93f-198">Si plusieurs tables répliquées sont impliquées nécessitant une reconstruction, chaque copie est reconstruit en série en tant qu’étapes au sein de l’instruction de hello.</span><span class="sxs-lookup"><span data-stu-id="5c93f-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within hello statement.</span></span>  <span data-ttu-id="5c93f-199">la cohérence des données pendant la reconstruction hello Hello toomaintain répliquées table qu'un verrou exclusif est établi sur la table de hello.</span><span class="sxs-lookup"><span data-stu-id="5c93f-199">toomaintain data consistency during hello rebuild of hello replicated table an exclusive lock is taken on hello table.</span></span>  <span data-ttu-id="5c93f-200">verrou de Hello pour la durée de reconstruction de hello hello, ce qui empêche la table de toohello tous les accès.</span><span class="sxs-lookup"><span data-stu-id="5c93f-200">hello lock prevents all access toohello table for hello duration of hello rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="5c93f-201">Utilisation restrictive des index</span><span class="sxs-lookup"><span data-stu-id="5c93f-201">Use indexes conservatively</span></span>
<span data-ttu-id="5c93f-202">Les pratiques d’indexation standards s’appliquent tooreplicated tables.</span><span class="sxs-lookup"><span data-stu-id="5c93f-202">Standard indexing practices apply tooreplicated tables.</span></span> <span data-ttu-id="5c93f-203">SQL Data Warehouse reconstruit l’index de chaque table répliquée dans le cadre de la reconstruction de hello.</span><span class="sxs-lookup"><span data-stu-id="5c93f-203">SQL Data Warehouse rebuilds each replicated table index as part of hello rebuild.</span></span> <span data-ttu-id="5c93f-204">Utilisez les index uniquement lorsque le gain de performances hello compense le coût hello de reconstruction d’index de hello.</span><span class="sxs-lookup"><span data-stu-id="5c93f-204">Only use indexes when hello performance gain outweighs hello cost of rebuilding hello indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="5c93f-205">Chargements de données par lots</span><span class="sxs-lookup"><span data-stu-id="5c93f-205">Batch data loads</span></span>
<span data-ttu-id="5c93f-206">Lors du chargement des données dans des tables répliquées, essayez les reconstructions toominimize en charges de traitement par lot.</span><span class="sxs-lookup"><span data-stu-id="5c93f-206">When loading data into replicated tables, try toominimize rebuilds by batching loads together.</span></span> <span data-ttu-id="5c93f-207">Effectuer toutes les charges hello traités par lot avant d’exécuter des instructions select.</span><span class="sxs-lookup"><span data-stu-id="5c93f-207">Perform all hello batched loads before running select statements.</span></span>

<span data-ttu-id="5c93f-208">Par exemple, ce modèle de chargement charge les données à partir de quatre sources et appelle quatre reconstructions.</span><span class="sxs-lookup"><span data-stu-id="5c93f-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="5c93f-209">Charger à partir de la source 1.</span><span class="sxs-lookup"><span data-stu-id="5c93f-209">Load from source 1.</span></span>
- <span data-ttu-id="5c93f-210">Instruction select qui déclenche la reconstruction 1.</span><span class="sxs-lookup"><span data-stu-id="5c93f-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="5c93f-211">Charger à partir de la source 2.</span><span class="sxs-lookup"><span data-stu-id="5c93f-211">Load from source 2.</span></span>
- <span data-ttu-id="5c93f-212">Instruction select qui déclenche la reconstruction 2.</span><span class="sxs-lookup"><span data-stu-id="5c93f-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="5c93f-213">Charger à partir de la source 3.</span><span class="sxs-lookup"><span data-stu-id="5c93f-213">Load from source 3.</span></span>
- <span data-ttu-id="5c93f-214">Instruction select qui déclenche la reconstruction 3.</span><span class="sxs-lookup"><span data-stu-id="5c93f-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="5c93f-215">Charger à partir de la source 4.</span><span class="sxs-lookup"><span data-stu-id="5c93f-215">Load from source 4.</span></span>
- <span data-ttu-id="5c93f-216">Instruction select qui déclenche la reconstruction 4.</span><span class="sxs-lookup"><span data-stu-id="5c93f-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="5c93f-217">Par exemple, ce modèle de chargement charge les données à partir de quatre sources mais n’appelle qu’une seule reconstruction.</span><span class="sxs-lookup"><span data-stu-id="5c93f-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="5c93f-218">Charger à partir de la source 1.</span><span class="sxs-lookup"><span data-stu-id="5c93f-218">Load from source 1.</span></span>
- <span data-ttu-id="5c93f-219">Charger à partir de la source 2.</span><span class="sxs-lookup"><span data-stu-id="5c93f-219">Load from source 2.</span></span>
- <span data-ttu-id="5c93f-220">Charger à partir de la source 3.</span><span class="sxs-lookup"><span data-stu-id="5c93f-220">Load from source 3.</span></span>
- <span data-ttu-id="5c93f-221">Charger à partir de la source 4.</span><span class="sxs-lookup"><span data-stu-id="5c93f-221">Load from source 4.</span></span>
- <span data-ttu-id="5c93f-222">Instruction select qui déclenche la reconstruction.</span><span class="sxs-lookup"><span data-stu-id="5c93f-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="5c93f-223">Reconstruire une table répliquée après un chargement par lots</span><span class="sxs-lookup"><span data-stu-id="5c93f-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="5c93f-224">temps d’exécution de requête cohérente tooensure, nous vous recommandons de forcer une actualisation des tables de hello répliquée après une charge de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="5c93f-224">tooensure consistent query execution times, we recommend forcing a refresh of hello replicated tables after a batch load.</span></span> <span data-ttu-id="5c93f-225">Dans le cas contraire, première requête de hello doit attendre de toorefresh de tables hello, qui inclut la reconstruction des index de hello.</span><span class="sxs-lookup"><span data-stu-id="5c93f-225">Otherwise, hello first query must wait for hello tables toorefresh, which includes rebuilding hello indexes.</span></span> <span data-ttu-id="5c93f-226">Selon la taille de hello et le nombre de tables répliquées affectées, impact sur les performances hello peut être importantes.</span><span class="sxs-lookup"><span data-stu-id="5c93f-226">Depending on hello size and number of replicated tables affected, hello performance impact can be significant.</span></span>  

<span data-ttu-id="5c93f-227">Cette requête utilise hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) hello toolist DMV répliquées des tables qui ont été modifiées mais ne pas reconstruits.</span><span class="sxs-lookup"><span data-stu-id="5c93f-227">This query uses hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello replicated tables that have been modified, but not rebuilt.</span></span>

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
 
<span data-ttu-id="5c93f-228">tooforce une régénération, exécutez hello instruction suivante sur chaque table Bonjour précédant la sortie.</span><span class="sxs-lookup"><span data-stu-id="5c93f-228">tooforce a rebuild, run hello following statement on each table in hello preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="5c93f-229">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5c93f-229">Next steps</span></span> 
<span data-ttu-id="5c93f-230">toocreate une table répliquée, utilisez une de ces instructions :</span><span class="sxs-lookup"><span data-stu-id="5c93f-230">toocreate a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="5c93f-231">CREATE TABLE (Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="5c93f-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="5c93f-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="5c93f-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="5c93f-233">Pour une vue d’ensemble des tables distribuées, consultez [Tables distribuées](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="5c93f-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



