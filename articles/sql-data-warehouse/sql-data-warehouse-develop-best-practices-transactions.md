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
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="06175-103">Optimisation des transactions pour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="06175-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="06175-104">Cet article vous explique comment optimiser les performances de votre code transactionnel tout en limitant les risques de restaurations de longue durée.</span><span class="sxs-lookup"><span data-stu-id="06175-104">This article explains how to optimize the performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="06175-105">Transactions et journalisation</span><span class="sxs-lookup"><span data-stu-id="06175-105">Transactions and logging</span></span>
<span data-ttu-id="06175-106">Les transactions sont une composante importante d’un moteur de base de données relationnelle.</span><span class="sxs-lookup"><span data-stu-id="06175-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="06175-107">SQL Data Warehouse utilise les transactions durant la modification des données.</span><span class="sxs-lookup"><span data-stu-id="06175-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="06175-108">Ces transactions peuvent être explicites ou implicites.</span><span class="sxs-lookup"><span data-stu-id="06175-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="06175-109">Les instructions uniques `INSERT`, `UPDATE` et `DELETE` sont toutes des exemples de transactions implicites.</span><span class="sxs-lookup"><span data-stu-id="06175-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="06175-110">Les transactions explicites sont écrites de manière explicite par un développeur à l’aide de `BEGIN TRAN`, `COMMIT TRAN` ou `ROLLBACK TRAN`. Généralement, elles sont utilisées dans les situations où plusieurs instructions de modification doivent être liées dans une seule unité atomique.</span><span class="sxs-lookup"><span data-stu-id="06175-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need to be tied together in a single atomic unit.</span></span> 

<span data-ttu-id="06175-111">Azure SQL Data Warehouse valide les modifications apportées à la base de données à l’aide de fichiers journaux de transactions.</span><span class="sxs-lookup"><span data-stu-id="06175-111">Azure SQL Data Warehouse commits changes to the database using transaction logs.</span></span> <span data-ttu-id="06175-112">Chaque distribution présente son propre fichier journal.</span><span class="sxs-lookup"><span data-stu-id="06175-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="06175-113">Les écritures des fichiers journaux de transactions sont automatiques.</span><span class="sxs-lookup"><span data-stu-id="06175-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="06175-114">Aucune configuration n’est requise.</span><span class="sxs-lookup"><span data-stu-id="06175-114">There is no configuration required.</span></span> <span data-ttu-id="06175-115">Notez toutefois que ce processus, qui garantit l’écriture, introduit par ailleurs une surcharge dans le système.</span><span class="sxs-lookup"><span data-stu-id="06175-115">However, whilst this process guarantees the write it does introduce an overhead in the system.</span></span> <span data-ttu-id="06175-116">Pour réduire des effets, vous pouvez écrire du code efficace sur le plan transactionnel.</span><span class="sxs-lookup"><span data-stu-id="06175-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="06175-117">Ce type de code se classe principalement en deux catégories.</span><span class="sxs-lookup"><span data-stu-id="06175-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="06175-118">Valorisez des structures minimalistes de journalisation, dans la mesure du possible.</span><span class="sxs-lookup"><span data-stu-id="06175-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="06175-119">Traitez les données en les regroupant par lots définis, afin d’éviter les transactions isolées de longue durée.</span><span class="sxs-lookup"><span data-stu-id="06175-119">Process data using scoped batches to avoid singular long running transactions</span></span>
* <span data-ttu-id="06175-120">Adoptez un modèle de basculement de partitions en cas de modifications importantes apportées à une partition donnée.</span><span class="sxs-lookup"><span data-stu-id="06175-120">Adopt a partition switching pattern for large modifications to a given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="06175-121">Journalisation minimale et journalisation complète</span><span class="sxs-lookup"><span data-stu-id="06175-121">Minimal vs. full logging</span></span>
<span data-ttu-id="06175-122">Contrairement aux opérations entièrement journalisées, qui utilisent le fichier journal de transactions pour effectuer le suivi de chaque modification de ligne, les journalisations minimales assurent le suivi des allocations d’étendue et des modifications de métadonnées uniquement.</span><span class="sxs-lookup"><span data-stu-id="06175-122">Unlike fully logged operations, which use the transaction log to keep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="06175-123">Par conséquent, la journalisation minimale implique la consignation exclusive des informations nécessaires à la restauration de la transaction en cas de défaillance ou de requête explicite (`ROLLBACK TRAN`).</span><span class="sxs-lookup"><span data-stu-id="06175-123">Therefore, minimal logging involves logging only the information that is required to rollback the transaction in the event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="06175-124">Dans la mesure où la journalisation minimale implique le suivi d’un volume de données moins important, cette opération est plus performante qu’une journalisation complète de taille similaire.</span><span class="sxs-lookup"><span data-stu-id="06175-124">As much less information is tracked in the transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="06175-125">En outre, un volume moins important d’écritures étant transmis vers le fichier journal de transactions, la quantité de données de journal générées est elle aussi réduite, et les performances E/S s’en trouvent accrues.</span><span class="sxs-lookup"><span data-stu-id="06175-125">Furthermore, because fewer writes go the transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="06175-126">Les limites de sécurité des transactions s’appliquent uniquement aux opérations faisant l’objet d’une journalisation complète.</span><span class="sxs-lookup"><span data-stu-id="06175-126">The transaction safety limits only apply to fully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="06175-127">Les opérations faisant l’objet d’une journalisation minimale peuvent prendre part à des transactions explicites.</span><span class="sxs-lookup"><span data-stu-id="06175-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="06175-128">Comme toutes les modifications des structures d’allocations font l’objet d’un suivi, il est possible de restaurer les journalisations minimales.</span><span class="sxs-lookup"><span data-stu-id="06175-128">As all changes in allocation structures are tracked, it is possible to roll back minimally logged operations.</span></span> <span data-ttu-id="06175-129">Il est important de comprendre la nuance : la modification fait bien l’objet d’une journalisation, aussi minimale soit-elle.</span><span class="sxs-lookup"><span data-stu-id="06175-129">It is important to understand that the change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="06175-130">Journalisations minimales</span><span class="sxs-lookup"><span data-stu-id="06175-130">Minimally logged operations</span></span>
<span data-ttu-id="06175-131">Les opérations suivantes peuvent faire l’objet d’une journalisation minimale :</span><span class="sxs-lookup"><span data-stu-id="06175-131">The following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="06175-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="06175-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="06175-133">INSERT..SELECT</span><span class="sxs-lookup"><span data-stu-id="06175-133">INSERT..SELECT</span></span>
* <span data-ttu-id="06175-134">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="06175-134">CREATE INDEX</span></span>
* <span data-ttu-id="06175-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="06175-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="06175-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="06175-136">DROP INDEX</span></span>
* <span data-ttu-id="06175-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="06175-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="06175-138">DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="06175-138">DROP TABLE</span></span>
* <span data-ttu-id="06175-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="06175-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="06175-140">Les opérations de déplacement de données internes (telles que `BROADCAST` et `SHUFFLE`) ne sont pas affectées par la limite de sécurité des transactions.</span><span class="sxs-lookup"><span data-stu-id="06175-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by the transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="06175-141">Journalisation minimale avec chargement en bloc</span><span class="sxs-lookup"><span data-stu-id="06175-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="06175-142">`CTAS` et `INSERT...SELECT` sont des opérations de chargement en bloc.</span><span class="sxs-lookup"><span data-stu-id="06175-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="06175-143">Toutefois, ces deux éléments sont affectés par la définition de table cible et dépendent du scénario de chargement.</span><span class="sxs-lookup"><span data-stu-id="06175-143">However, both are influenced by the target table definition and depend on the load scenario.</span></span> <span data-ttu-id="06175-144">Voici un tableau détaillant les situations de journalisations minimales ou complètes des opérations de chargement en bloc :</span><span class="sxs-lookup"><span data-stu-id="06175-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="06175-145">Index primaire</span><span class="sxs-lookup"><span data-stu-id="06175-145">Primary Index</span></span> | <span data-ttu-id="06175-146">Scénario de chargement</span><span class="sxs-lookup"><span data-stu-id="06175-146">Load Scenario</span></span> | <span data-ttu-id="06175-147">Mode de journalisation</span><span class="sxs-lookup"><span data-stu-id="06175-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="06175-148">Segment de mémoire</span><span class="sxs-lookup"><span data-stu-id="06175-148">Heap</span></span> |<span data-ttu-id="06175-149">Quelconque</span><span class="sxs-lookup"><span data-stu-id="06175-149">Any</span></span> |<span data-ttu-id="06175-150">**Minimal**</span><span class="sxs-lookup"><span data-stu-id="06175-150">**Minimal**</span></span> |
| <span data-ttu-id="06175-151">Index cluster</span><span class="sxs-lookup"><span data-stu-id="06175-151">Clustered Index</span></span> |<span data-ttu-id="06175-152">Table cible vide</span><span class="sxs-lookup"><span data-stu-id="06175-152">Empty target table</span></span> |<span data-ttu-id="06175-153">**Minimal**</span><span class="sxs-lookup"><span data-stu-id="06175-153">**Minimal**</span></span> |
| <span data-ttu-id="06175-154">Index cluster</span><span class="sxs-lookup"><span data-stu-id="06175-154">Clustered Index</span></span> |<span data-ttu-id="06175-155">Les lignes chargées ne se chevauchent pas avec les pages existantes dans la cible.</span><span class="sxs-lookup"><span data-stu-id="06175-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="06175-156">**Minimal**</span><span class="sxs-lookup"><span data-stu-id="06175-156">**Minimal**</span></span> |
| <span data-ttu-id="06175-157">Index cluster</span><span class="sxs-lookup"><span data-stu-id="06175-157">Clustered Index</span></span> |<span data-ttu-id="06175-158">Les lignes chargées se chevauchent avec les pages existantes dans la cible.</span><span class="sxs-lookup"><span data-stu-id="06175-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="06175-159">Complet</span><span class="sxs-lookup"><span data-stu-id="06175-159">Full</span></span> |
| <span data-ttu-id="06175-160">Index columstore en cluster</span><span class="sxs-lookup"><span data-stu-id="06175-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="06175-161">Taille de lot >= 102 400 par distribution alignée sur la partition</span><span class="sxs-lookup"><span data-stu-id="06175-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="06175-162">**Minimal**</span><span class="sxs-lookup"><span data-stu-id="06175-162">**Minimal**</span></span> |
| <span data-ttu-id="06175-163">Index columstore en cluster</span><span class="sxs-lookup"><span data-stu-id="06175-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="06175-164">Taille de lot < 102 400 par distribution alignée sur la partition</span><span class="sxs-lookup"><span data-stu-id="06175-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="06175-165">Complet</span><span class="sxs-lookup"><span data-stu-id="06175-165">Full</span></span> |

<span data-ttu-id="06175-166">Il est important de noter que toute opération d’écriture effectuée dans le cadre d’une mise à jour d’index secondaires ou non cluster correspond à une journalisation complète.</span><span class="sxs-lookup"><span data-stu-id="06175-166">It is worth noting that any writes to update secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06175-167">SQL Data Warehouse présente 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="06175-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="06175-168">Par conséquent, en partant du principe que l’ensemble des lignes sont distribuées équitablement et placées dans une partition unique, votre lot devra comporter 6 144 000 lots ou plus pour faire l’objet d’une journalisation minimale lors d’une écriture vers un index columstore en cluster.</span><span class="sxs-lookup"><span data-stu-id="06175-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need to contain 6,144,000 rows or larger to be minimally logged when writing to a Clustered Columnstore Index.</span></span> <span data-ttu-id="06175-169">Si la table est partitionnée et que les lignes insérées dépassent les limites de la partition, il vous faudra 6 144 000 lignes par limite de partition, pour une distribution uniforme des données.</span><span class="sxs-lookup"><span data-stu-id="06175-169">If the table is partitioned and the rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="06175-170">Dans chaque distribution, l’ensemble des partitions doivent isolément dépasser le seuil de 102 400 lignes pour que l’insertion fasse l’objet d’une journalisation minimale dans la distribution.</span><span class="sxs-lookup"><span data-stu-id="06175-170">Each partition in each distribution must independently exceed the 102,400 row threshold for the insert to be minimally logged into the distribution.</span></span>
> 
> 

<span data-ttu-id="06175-171">Le chargement de données dans une table non vide avec un index cluster comporte bien souvent une combinaison de lignes ayant fait l’objet d’une journalisation minimale et complète.</span><span class="sxs-lookup"><span data-stu-id="06175-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="06175-172">Un index cluster est un arbre équilibré (arbre b) de pages.</span><span class="sxs-lookup"><span data-stu-id="06175-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="06175-173">Si la page cible de l’écriture comporte déjà des lignes d’une autre transaction, ces opérations d’écriture feront l’objet d’une journalisation complète.</span><span class="sxs-lookup"><span data-stu-id="06175-173">If the page being written to already contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="06175-174">Toutefois, si la page est vide, l’opération d’écriture fera l’objet d’une journalisation minimale.</span><span class="sxs-lookup"><span data-stu-id="06175-174">However, if the page is empty then the write to that page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="06175-175">Optimisation des suppressions</span><span class="sxs-lookup"><span data-stu-id="06175-175">Optimizing deletes</span></span>
<span data-ttu-id="06175-176">`DELETE` est une opération entièrement journalisée.</span><span class="sxs-lookup"><span data-stu-id="06175-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="06175-177">Si vous avez besoin de supprimer un volume important de données dans une table ou une partition, il est souvent plus judicieux d’appliquer une opération `SELECT` aux données que vous souhaitez conserver, qui peut être exécutée en tant qu’opération de journalisation minimale.</span><span class="sxs-lookup"><span data-stu-id="06175-177">If you need to delete a large amount of data in a table or a partition, it often makes more sense to `SELECT` the data you wish to keep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="06175-178">Pour ce faire, créez une table avec [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="06175-178">To accomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="06175-179">Une fois la table créée, utilisez [RENAME][RENAME] pour permuter l’ancienne table et la table nouvellement créée.</span><span class="sxs-lookup"><span data-stu-id="06175-179">Once created, use [RENAME][RENAME] to swap out your old table with the newly created table.</span></span>

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

## <a name="optimizing-updates"></a><span data-ttu-id="06175-180">Optimisation des mises à jour</span><span class="sxs-lookup"><span data-stu-id="06175-180">Optimizing updates</span></span>
<span data-ttu-id="06175-181">`UPDATE` est une opération entièrement journalisée.</span><span class="sxs-lookup"><span data-stu-id="06175-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="06175-182">SI vous devez mettre à jour un nombre important de lignes d’une table ou d’une partition, il peut souvent s’avérer plus efficace de recourir à une opération avec une journalisation minimale, comme [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="06175-182">If you need to update a large number of rows in a table or a partition it can often be far more efficient to use a minimally logged operation such as [CTAS][CTAS] to do so.</span></span>

<span data-ttu-id="06175-183">Dans l’exemple suivant, une mise à jour complète de table a été convertie en `CTAS` , ce qui rend possible la mise en place d’une journalisation minimale.</span><span class="sxs-lookup"><span data-stu-id="06175-183">In the example below a full table update has been converted to a `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="06175-184">Dans ce cas, nous ajoutons a posteriori une valeur de remise aux ventes dans la table :</span><span class="sxs-lookup"><span data-stu-id="06175-184">In this case we are retrospectively adding a discount amount to the sales in the table:</span></span>

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
> <span data-ttu-id="06175-185">Les fonctions de gestion des charges de travail SQL Data Warehouse peuvent faciliter la recréation des tables de grande taille.</span><span class="sxs-lookup"><span data-stu-id="06175-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="06175-186">Pour plus d’informations, consultez la section relative à la gestion des charges de travail, dans l’article sur [l’accès concurrentiel][concurrency].</span><span class="sxs-lookup"><span data-stu-id="06175-186">For more details please refer to the workload management section in the [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="06175-187">Optimisation avec basculement de partitions</span><span class="sxs-lookup"><span data-stu-id="06175-187">Optimizing with partition switching</span></span>
<span data-ttu-id="06175-188">Quand vous devez procéder à des modifications à grande échelle au sein d’une [partition de table][table partition], il est bien plus judicieux d’adopter un modèle de basculement de partitions.</span><span class="sxs-lookup"><span data-stu-id="06175-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="06175-189">Si la modification de données est considérable et relative à plusieurs partitions, vous obtiendrez un résultat identique en effectuant une itération sur les partitions.</span><span class="sxs-lookup"><span data-stu-id="06175-189">If the data modification is significant and spans multiple partitions, then simply iterating over the partitions achieves the same result.</span></span>

<span data-ttu-id="06175-190">Les étapes constitutives d’un basculement de partitions sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="06175-190">The steps to perform a partition switch are as follows:</span></span>

1. <span data-ttu-id="06175-191">Créer une partition vide</span><span class="sxs-lookup"><span data-stu-id="06175-191">Create an empty out partition</span></span>
2. <span data-ttu-id="06175-192">Effectuez la mise à jour en tant que CTAS</span><span class="sxs-lookup"><span data-stu-id="06175-192">Perform the 'update' as a CTAS</span></span>
3. <span data-ttu-id="06175-193">Extraire les données existantes vers la table cible</span><span class="sxs-lookup"><span data-stu-id="06175-193">Switch out the existing data to the out table</span></span>
4. <span data-ttu-id="06175-194">Basculer les nouvelles données</span><span class="sxs-lookup"><span data-stu-id="06175-194">Switch in the new data</span></span>
5. <span data-ttu-id="06175-195">Nettoyer les données</span><span class="sxs-lookup"><span data-stu-id="06175-195">Clean up the data</span></span>

<span data-ttu-id="06175-196">Toutefois, pour faciliter l’identification des partitions à basculer, nous devons dans un premier temps générer une procédure d’assistance, semblable à celle ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="06175-196">However, to help identify the partitions to switch we will first need to build a helper procedure such as the one below.</span></span> 

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

<span data-ttu-id="06175-197">Cette procédure optimise la réutilisation du code et permet de conserver un exemple de basculement de partitions plus compact.</span><span class="sxs-lookup"><span data-stu-id="06175-197">This procedure maximizes code re-use and keeps the partition switching example more compact.</span></span>

<span data-ttu-id="06175-198">Le code ci-dessous représente les cinq étapes mentionnées plus haut pour l’exécution d’une opération de basculement complet de partitions.</span><span class="sxs-lookup"><span data-stu-id="06175-198">The code below demonstrates the five steps mentioned above to achieve a full partition switching routine.</span></span>

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

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="06175-199">Minimiser la journalisation avec des lots de petite taille</span><span class="sxs-lookup"><span data-stu-id="06175-199">Minimize logging with small batches</span></span>
<span data-ttu-id="06175-200">Pour les opérations de grande envergure de modifications de données, il peut s’avérer judicieux de diviser l’activité en segments ou lots afin de répartir la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="06175-200">For large data modification operations, it may make sense to divide the operation into chunks or batches to scope the unit of work.</span></span>

<span data-ttu-id="06175-201">Vous trouverez ci-dessous un exemple de travail.</span><span class="sxs-lookup"><span data-stu-id="06175-201">A working example is provided below.</span></span> <span data-ttu-id="06175-202">La taille du lot a été définie sur un nombre insignifiant, ceci pour mettre en évidence la technique.</span><span class="sxs-lookup"><span data-stu-id="06175-202">The batch size has been set to a trivial number to highlight the technique.</span></span> <span data-ttu-id="06175-203">Dans la réalité, la taille du lot serait bien plus importante.</span><span class="sxs-lookup"><span data-stu-id="06175-203">In reality the batch size would be significantly larger.</span></span> 

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

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="06175-204">Conseils sur la suspension et la mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="06175-204">Pause and scaling guidance</span></span>
<span data-ttu-id="06175-205">Azure SQL Data Warehouse vous permet de suspendre, de reprendre et de mettre à l’échelle à la demande votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="06175-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="06175-206">Lorsque vous suspendez ou mettez à l’échelle votre instance SQL Data Warehouse, il est important de comprendre que l’ensemble des transactions en cours sont immédiatement arrêtées ; toute transaction ouverte est restaurée.</span><span class="sxs-lookup"><span data-stu-id="06175-206">When you pause or scale your SQL Data Warehouse it is important to understand that any in-flight transactions are terminated immediately; causing any open transactions to be rolled back.</span></span> <span data-ttu-id="06175-207">Si votre charge de travail a émis une modification de données incomplète et de longue durée avant l’opération de suspension ou de mise à l’échelle, cette tâche devra être annulée.</span><span class="sxs-lookup"><span data-stu-id="06175-207">If your workload had issued a long running and incomplete data modification prior to the pause or scale operation, then this work will need to be undone.</span></span> <span data-ttu-id="06175-208">Cela peut avoir une incidence sur le délai nécessaire à la suspension ou à la mise à jour de votre base de données Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="06175-208">This may impact the time it takes to pause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="06175-209">`UPDATE` et `DELETE` correspondant toutes deux à des journalisations complètes, ces opérations d’annulation et de rétablissement peuvent nécessiter un délai considérablement plus important que des journalisations minimales de taille équivalente.</span><span class="sxs-lookup"><span data-stu-id="06175-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="06175-210">La configuration idéale consiste à laisser les modifications en cours de données se terminer avant la suspension ou la mise à l’échelle de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="06175-210">The best scenario is to let in flight data modification transactions complete prior to pausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="06175-211">Toutefois, cela n’est pas toujours pratique.</span><span class="sxs-lookup"><span data-stu-id="06175-211">However, this may not always be practical.</span></span> <span data-ttu-id="06175-212">Pour pallier le risque d’une longue restauration, envisagez l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="06175-212">To mitigate the risk of a long rollback, consider one of the following options:</span></span>

* <span data-ttu-id="06175-213">Réécrire les opérations de longue durée à l’aide de [CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="06175-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="06175-214">Décomposer l’opération en segments, en traitant un sous-ensemble des lignes</span><span class="sxs-lookup"><span data-stu-id="06175-214">Break the operation down into chunks; operating on a subset of the rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="06175-215">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="06175-215">Next steps</span></span>
<span data-ttu-id="06175-216">Consultez [Transactions dans SQL Data Warehouse][Transactions in SQL Data Warehouse] pour en savoir plus sur les niveaux d’isolement et les limites transactionnelles.</span><span class="sxs-lookup"><span data-stu-id="06175-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] to learn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="06175-217">Pour une vue d’ensemble des autres bonnes pratiques, consultez [Bonnes pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="06175-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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

