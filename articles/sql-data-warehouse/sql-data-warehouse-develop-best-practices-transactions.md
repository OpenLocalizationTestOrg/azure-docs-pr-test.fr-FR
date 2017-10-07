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
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="c7bab-103">Optimisation des transactions pour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c7bab-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="c7bab-104">Cet article explique comment toooptimize hello les performances de votre code transactionnel en limitant les risques pour les restaurations de long.</span><span class="sxs-lookup"><span data-stu-id="c7bab-104">This article explains how toooptimize hello performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="c7bab-105">Transactions et journalisation</span><span class="sxs-lookup"><span data-stu-id="c7bab-105">Transactions and logging</span></span>
<span data-ttu-id="c7bab-106">Les transactions sont une composante importante d’un moteur de base de données relationnelle.</span><span class="sxs-lookup"><span data-stu-id="c7bab-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="c7bab-107">SQL Data Warehouse utilise les transactions durant la modification des données.</span><span class="sxs-lookup"><span data-stu-id="c7bab-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="c7bab-108">Ces transactions peuvent être explicites ou implicites.</span><span class="sxs-lookup"><span data-stu-id="c7bab-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="c7bab-109">Les instructions uniques `INSERT`, `UPDATE` et `DELETE` sont toutes des exemples de transactions implicites.</span><span class="sxs-lookup"><span data-stu-id="c7bab-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="c7bab-110">Transactions explicites sont écrites explicitement par un développeur à l’aide de `BEGIN TRAN`, `COMMIT TRAN` ou `ROLLBACK TRAN` et sont généralement utilisées lorsque vous avez besoin de plusieurs instructions de modification toobe tous lié entre eux dans une unité atomique unique.</span><span class="sxs-lookup"><span data-stu-id="c7bab-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need toobe tied together in a single atomic unit.</span></span> 

<span data-ttu-id="c7bab-111">Entrepôt de données SQL Azure valide de base de données de modifications toohello à l’aide des journaux de transactions.</span><span class="sxs-lookup"><span data-stu-id="c7bab-111">Azure SQL Data Warehouse commits changes toohello database using transaction logs.</span></span> <span data-ttu-id="c7bab-112">Chaque distribution présente son propre fichier journal.</span><span class="sxs-lookup"><span data-stu-id="c7bab-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="c7bab-113">Les écritures des fichiers journaux de transactions sont automatiques.</span><span class="sxs-lookup"><span data-stu-id="c7bab-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="c7bab-114">Aucune configuration n’est requise.</span><span class="sxs-lookup"><span data-stu-id="c7bab-114">There is no configuration required.</span></span> <span data-ttu-id="c7bab-115">Toutefois, alors que ce processus garantit l’écriture de hello, il introduit une surcharge dans le système de hello.</span><span class="sxs-lookup"><span data-stu-id="c7bab-115">However, whilst this process guarantees hello write it does introduce an overhead in hello system.</span></span> <span data-ttu-id="c7bab-116">Pour réduire des effets, vous pouvez écrire du code efficace sur le plan transactionnel.</span><span class="sxs-lookup"><span data-stu-id="c7bab-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="c7bab-117">Ce type de code se classe principalement en deux catégories.</span><span class="sxs-lookup"><span data-stu-id="c7bab-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="c7bab-118">Valorisez des structures minimalistes de journalisation, dans la mesure du possible.</span><span class="sxs-lookup"><span data-stu-id="c7bab-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="c7bab-119">Traitement des données à l’aide d’une étendue singulier tooavoid de lots longues transactions</span><span class="sxs-lookup"><span data-stu-id="c7bab-119">Process data using scoped batches tooavoid singular long running transactions</span></span>
* <span data-ttu-id="c7bab-120">Adopter une modèle pour tooa modifications volumineux une partition donnée du basculement de partition</span><span class="sxs-lookup"><span data-stu-id="c7bab-120">Adopt a partition switching pattern for large modifications tooa given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="c7bab-121">Journalisation minimale et journalisation complète</span><span class="sxs-lookup"><span data-stu-id="c7bab-121">Minimal vs. full logging</span></span>
<span data-ttu-id="c7bab-122">Contrairement aux opérations entièrement journalisées, qui utilisent hello transaction journal tookeep le suivi de chaque modification de ligne, les opérations journalisées minimales effectuer le suivi des allocations des extensions et des modifications de métadonnées uniquement.</span><span class="sxs-lookup"><span data-stu-id="c7bab-122">Unlike fully logged operations, which use hello transaction log tookeep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="c7bab-123">Par conséquent, la journalisation minimale implique de ne journaliser que les informations de hello toorollback requis hello transaction les événements hello d’une panne ou demande explicite (`ROLLBACK TRAN`).</span><span class="sxs-lookup"><span data-stu-id="c7bab-123">Therefore, minimal logging involves logging only hello information that is required toorollback hello transaction in hello event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="c7bab-124">Comme beaucoup moins les informations sont suivies dans le journal des transactions hello, une opération journalisée minimale plus performant qu’une opération entièrement journalisée taille similaire.</span><span class="sxs-lookup"><span data-stu-id="c7bab-124">As much less information is tracked in hello transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="c7bab-125">En outre, étant donné que moins d’écritures passent le journal des transactions hello, une plus petite quantité de données de journal est générée et est donc d’e/s plus efficace.</span><span class="sxs-lookup"><span data-stu-id="c7bab-125">Furthermore, because fewer writes go hello transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="c7bab-126">limites de sécurité de transaction Hello s’appliquent uniquement à des opérations de toofully connecté.</span><span class="sxs-lookup"><span data-stu-id="c7bab-126">hello transaction safety limits only apply toofully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="c7bab-127">Les opérations faisant l’objet d’une journalisation minimale peuvent prendre part à des transactions explicites.</span><span class="sxs-lookup"><span data-stu-id="c7bab-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="c7bab-128">Toutes les modifications apportées aux structures d’allocation sont suivies, il est possible tooroll arrière minimale opérations journalisées.</span><span class="sxs-lookup"><span data-stu-id="c7bab-128">As all changes in allocation structures are tracked, it is possible tooroll back minimally logged operations.</span></span> <span data-ttu-id="c7bab-129">Il est important de toounderstand hello modification est « minimale » connecté qu’il n’est pas non connecté.</span><span class="sxs-lookup"><span data-stu-id="c7bab-129">It is important toounderstand that hello change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="c7bab-130">Journalisations minimales</span><span class="sxs-lookup"><span data-stu-id="c7bab-130">Minimally logged operations</span></span>
<span data-ttu-id="c7bab-131">Hello opérations suivantes sont capables d’en cours d’une journalisation minimale :</span><span class="sxs-lookup"><span data-stu-id="c7bab-131">hello following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="c7bab-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="c7bab-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="c7bab-133">INSERT..SELECT</span><span class="sxs-lookup"><span data-stu-id="c7bab-133">INSERT..SELECT</span></span>
* <span data-ttu-id="c7bab-134">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="c7bab-134">CREATE INDEX</span></span>
* <span data-ttu-id="c7bab-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="c7bab-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="c7bab-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="c7bab-136">DROP INDEX</span></span>
* <span data-ttu-id="c7bab-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="c7bab-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="c7bab-138">DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="c7bab-138">DROP TABLE</span></span>
* <span data-ttu-id="c7bab-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="c7bab-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="c7bab-140">Opérations de déplacement de données internes (telles que `BROADCAST` et `SHUFFLE`) ne sont pas affectés par la limite de sécurité de transaction hello.</span><span class="sxs-lookup"><span data-stu-id="c7bab-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by hello transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="c7bab-141">Journalisation minimale avec chargement en bloc</span><span class="sxs-lookup"><span data-stu-id="c7bab-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="c7bab-142">`CTAS` et `INSERT...SELECT` sont des opérations de chargement en bloc.</span><span class="sxs-lookup"><span data-stu-id="c7bab-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="c7bab-143">Toutefois, les deux sont influencées par la définition de la table cible hello et varient selon le scénario de charge hello.</span><span class="sxs-lookup"><span data-stu-id="c7bab-143">However, both are influenced by hello target table definition and depend on hello load scenario.</span></span> <span data-ttu-id="c7bab-144">Voici un tableau détaillant les situations de journalisations minimales ou complètes des opérations de chargement en bloc :</span><span class="sxs-lookup"><span data-stu-id="c7bab-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="c7bab-145">Index primaire</span><span class="sxs-lookup"><span data-stu-id="c7bab-145">Primary Index</span></span> | <span data-ttu-id="c7bab-146">Scénario de chargement</span><span class="sxs-lookup"><span data-stu-id="c7bab-146">Load Scenario</span></span> | <span data-ttu-id="c7bab-147">Mode de journalisation</span><span class="sxs-lookup"><span data-stu-id="c7bab-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c7bab-148">Segment de mémoire</span><span class="sxs-lookup"><span data-stu-id="c7bab-148">Heap</span></span> |<span data-ttu-id="c7bab-149">Quelconque</span><span class="sxs-lookup"><span data-stu-id="c7bab-149">Any</span></span> |<span data-ttu-id="c7bab-150">**Minimal**</span><span class="sxs-lookup"><span data-stu-id="c7bab-150">**Minimal**</span></span> |
| <span data-ttu-id="c7bab-151">Index cluster</span><span class="sxs-lookup"><span data-stu-id="c7bab-151">Clustered Index</span></span> |<span data-ttu-id="c7bab-152">Table cible vide</span><span class="sxs-lookup"><span data-stu-id="c7bab-152">Empty target table</span></span> |<span data-ttu-id="c7bab-153">**Minimal**</span><span class="sxs-lookup"><span data-stu-id="c7bab-153">**Minimal**</span></span> |
| <span data-ttu-id="c7bab-154">Index cluster</span><span class="sxs-lookup"><span data-stu-id="c7bab-154">Clustered Index</span></span> |<span data-ttu-id="c7bab-155">Les lignes chargées ne se chevauchent pas avec les pages existantes dans la cible.</span><span class="sxs-lookup"><span data-stu-id="c7bab-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="c7bab-156">**Minimal**</span><span class="sxs-lookup"><span data-stu-id="c7bab-156">**Minimal**</span></span> |
| <span data-ttu-id="c7bab-157">Index cluster</span><span class="sxs-lookup"><span data-stu-id="c7bab-157">Clustered Index</span></span> |<span data-ttu-id="c7bab-158">Les lignes chargées se chevauchent avec les pages existantes dans la cible.</span><span class="sxs-lookup"><span data-stu-id="c7bab-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="c7bab-159">Complet</span><span class="sxs-lookup"><span data-stu-id="c7bab-159">Full</span></span> |
| <span data-ttu-id="c7bab-160">Index columstore en cluster</span><span class="sxs-lookup"><span data-stu-id="c7bab-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="c7bab-161">Taille de lot >= 102 400 par distribution alignée sur la partition</span><span class="sxs-lookup"><span data-stu-id="c7bab-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="c7bab-162">**Minimal**</span><span class="sxs-lookup"><span data-stu-id="c7bab-162">**Minimal**</span></span> |
| <span data-ttu-id="c7bab-163">Index columstore en cluster</span><span class="sxs-lookup"><span data-stu-id="c7bab-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="c7bab-164">Taille de lot < 102 400 par distribution alignée sur la partition</span><span class="sxs-lookup"><span data-stu-id="c7bab-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="c7bab-165">Complet</span><span class="sxs-lookup"><span data-stu-id="c7bab-165">Full</span></span> |

<span data-ttu-id="c7bab-166">Il est important de noter que toutes les écritures tooupdate secondaire ou non cluster de l’index sera toujours entièrement les opérations journalisées.</span><span class="sxs-lookup"><span data-stu-id="c7bab-166">It is worth noting that any writes tooupdate secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7bab-167">SQL Data Warehouse présente 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="c7bab-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="c7bab-168">Par conséquent, si vous en supposant que toutes les lignes sont réparties uniformément et de destination dans une seule partition, votre lot devez toocontain 6,144,000 lignes ou plus grande toobe minimale connecté lors de l’écriture tooa Index cluster Columnstore.</span><span class="sxs-lookup"><span data-stu-id="c7bab-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need toocontain 6,144,000 rows or larger toobe minimally logged when writing tooa Clustered Columnstore Index.</span></span> <span data-ttu-id="c7bab-169">Si hello table est partitionnée et lignes hello insérées sont réparties entre les limites de partition, vous devez 6,144,000 lignes par limite de partition en supposant que la répartition égale des données.</span><span class="sxs-lookup"><span data-stu-id="c7bab-169">If hello table is partitioned and hello rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="c7bab-170">Chaque partition de chaque point de distribution doit dépasser indépendamment hello 102 400 lignes seuil pour toobe d’insertion hello journalisée dans la distribution de hello.</span><span class="sxs-lookup"><span data-stu-id="c7bab-170">Each partition in each distribution must independently exceed hello 102,400 row threshold for hello insert toobe minimally logged into hello distribution.</span></span>
> 
> 

<span data-ttu-id="c7bab-171">Le chargement de données dans une table non vide avec un index cluster comporte bien souvent une combinaison de lignes ayant fait l’objet d’une journalisation minimale et complète.</span><span class="sxs-lookup"><span data-stu-id="c7bab-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="c7bab-172">Un index cluster est un arbre équilibré (arbre b) de pages.</span><span class="sxs-lookup"><span data-stu-id="c7bab-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="c7bab-173">Si la page de hello écrits tooalready contient des lignes à partir d’une autre transaction, ces écritures doivent être enregistrés entièrement.</span><span class="sxs-lookup"><span data-stu-id="c7bab-173">If hello page being written tooalready contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="c7bab-174">Toutefois, si la page de hello est vide puis page de toothat hello écriture est consignées dans le journal.</span><span class="sxs-lookup"><span data-stu-id="c7bab-174">However, if hello page is empty then hello write toothat page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="c7bab-175">Optimisation des suppressions</span><span class="sxs-lookup"><span data-stu-id="c7bab-175">Optimizing deletes</span></span>
<span data-ttu-id="c7bab-176">`DELETE` est une opération entièrement journalisée.</span><span class="sxs-lookup"><span data-stu-id="c7bab-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="c7bab-177">Si vous devez toodelete une grande quantité de données dans une table ou une partition, il est donc souvent plus judicieux trop`SELECT` les données de salutation que vous souhaitez tookeep, ce qui peut être exécutée en tant qu’une opération journalisée minimale.</span><span class="sxs-lookup"><span data-stu-id="c7bab-177">If you need toodelete a large amount of data in a table or a partition, it often makes more sense too`SELECT` hello data you wish tookeep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="c7bab-178">tooaccomplish, créez une nouvelle table avec [SACT][CTAS].</span><span class="sxs-lookup"><span data-stu-id="c7bab-178">tooaccomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="c7bab-179">Une fois créé, utilisez [renommer] [ RENAME] tooswap votre ancienne table avec la table de hello nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="c7bab-179">Once created, use [RENAME][RENAME] tooswap out your old table with hello newly created table.</span></span>

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

## <a name="optimizing-updates"></a><span data-ttu-id="c7bab-180">Optimisation des mises à jour</span><span class="sxs-lookup"><span data-stu-id="c7bab-180">Optimizing updates</span></span>
<span data-ttu-id="c7bab-181">`UPDATE` est une opération entièrement journalisée.</span><span class="sxs-lookup"><span data-stu-id="c7bab-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="c7bab-182">Si vous avez besoin de tooupdate un grand nombre de lignes dans une table ou d’une partition souvent beaucoup plus efficace toouse une opération journalisée minimale comme [SACT] [ CTAS] toodo donc.</span><span class="sxs-lookup"><span data-stu-id="c7bab-182">If you need tooupdate a large number of rows in a table or a partition it can often be far more efficient toouse a minimally logged operation such as [CTAS][CTAS] toodo so.</span></span>

<span data-ttu-id="c7bab-183">Bonjour exemple ci-dessous, une mise à jour complète de la table a été converti tooa `CTAS` afin que la journalisation minimale est possible.</span><span class="sxs-lookup"><span data-stu-id="c7bab-183">In hello example below a full table update has been converted tooa `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="c7bab-184">Dans ce cas, nous avons ajouté a posteriori une vente toohello du montant remise dans la table de hello :</span><span class="sxs-lookup"><span data-stu-id="c7bab-184">In this case we are retrospectively adding a discount amount toohello sales in hello table:</span></span>

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
> <span data-ttu-id="c7bab-185">Les fonctions de gestion des charges de travail SQL Data Warehouse peuvent faciliter la recréation des tables de grande taille.</span><span class="sxs-lookup"><span data-stu-id="c7bab-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="c7bab-186">Pour plus d’informations, consultez la section de gestion de la charge de travail toohello Bonjour [concurrency] [ concurrency] l’article.</span><span class="sxs-lookup"><span data-stu-id="c7bab-186">For more details please refer toohello workload management section in hello [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="c7bab-187">Optimisation avec basculement de partitions</span><span class="sxs-lookup"><span data-stu-id="c7bab-187">Optimizing with partition switching</span></span>
<span data-ttu-id="c7bab-188">Quand vous devez procéder à des modifications à grande échelle au sein d’une [partition de table][table partition], il est bien plus judicieux d’adopter un modèle de basculement de partitions.</span><span class="sxs-lookup"><span data-stu-id="c7bab-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="c7bab-189">Si hello modification des données est importante et étendues parvient à plusieurs partitions, puis itérer simplement les partitions hello hello même résultat.</span><span class="sxs-lookup"><span data-stu-id="c7bab-189">If hello data modification is significant and spans multiple partitions, then simply iterating over hello partitions achieves hello same result.</span></span>

<span data-ttu-id="c7bab-190">Hello étapes tooperform un basculement de partition sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="c7bab-190">hello steps tooperform a partition switch are as follows:</span></span>

1. <span data-ttu-id="c7bab-191">Créer une partition vide</span><span class="sxs-lookup"><span data-stu-id="c7bab-191">Create an empty out partition</span></span>
2. <span data-ttu-id="c7bab-192">Effectuer hello « mise à jour » comme un SACT</span><span class="sxs-lookup"><span data-stu-id="c7bab-192">Perform hello 'update' as a CTAS</span></span>
3. <span data-ttu-id="c7bab-193">Hello toohello de données existantes à la table d’extraction</span><span class="sxs-lookup"><span data-stu-id="c7bab-193">Switch out hello existing data toohello out table</span></span>
4. <span data-ttu-id="c7bab-194">Insérer des données de nouveau hello</span><span class="sxs-lookup"><span data-stu-id="c7bab-194">Switch in hello new data</span></span>
5. <span data-ttu-id="c7bab-195">Nettoyer les données de hello</span><span class="sxs-lookup"><span data-stu-id="c7bab-195">Clean up hello data</span></span>

<span data-ttu-id="c7bab-196">Cependant, toohelp identifier tooswitch de partitions hello nous devez abord toobuild une procédure d’assistance tels que hello un ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c7bab-196">However, toohelp identify hello partitions tooswitch we will first need toobuild a helper procedure such as hello one below.</span></span> 

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

<span data-ttu-id="c7bab-197">Cette procédure optimise la réutilisation de code et conserve exemple plus compacte du basculement de partition hello.</span><span class="sxs-lookup"><span data-stu-id="c7bab-197">This procedure maximizes code re-use and keeps hello partition switching example more compact.</span></span>

<span data-ttu-id="c7bab-198">code Hello ci-dessous montre cinq étapes de hello mentionnés ci-dessus tooachieve une routine du basculement de partition complète.</span><span class="sxs-lookup"><span data-stu-id="c7bab-198">hello code below demonstrates hello five steps mentioned above tooachieve a full partition switching routine.</span></span>

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

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="c7bab-199">Minimiser la journalisation avec des lots de petite taille</span><span class="sxs-lookup"><span data-stu-id="c7bab-199">Minimize logging with small batches</span></span>
<span data-ttu-id="c7bab-200">Pour les opérations de modification de données de grande taille, il peut être judicieux toodivide hello opération en unité de hello tooscope segments ou des lots de travail.</span><span class="sxs-lookup"><span data-stu-id="c7bab-200">For large data modification operations, it may make sense toodivide hello operation into chunks or batches tooscope hello unit of work.</span></span>

<span data-ttu-id="c7bab-201">Vous trouverez ci-dessous un exemple de travail.</span><span class="sxs-lookup"><span data-stu-id="c7bab-201">A working example is provided below.</span></span> <span data-ttu-id="c7bab-202">taille de lot Hello a été défini tooa trivial technique hello numéro toohighlight.</span><span class="sxs-lookup"><span data-stu-id="c7bab-202">hello batch size has been set tooa trivial number toohighlight hello technique.</span></span> <span data-ttu-id="c7bab-203">En réalité, taille de lot hello serait beaucoup plus important.</span><span class="sxs-lookup"><span data-stu-id="c7bab-203">In reality hello batch size would be significantly larger.</span></span> 

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

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="c7bab-204">Conseils sur la suspension et la mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="c7bab-204">Pause and scaling guidance</span></span>
<span data-ttu-id="c7bab-205">Azure SQL Data Warehouse vous permet de suspendre, de reprendre et de mettre à l’échelle à la demande votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="c7bab-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="c7bab-206">Lorsque vous suspendez ou mettre à l’échelle de votre entrepôt de données SQL qu’il est important toounderstand que toutes les transactions en cours sont terminent immédiatement ; à l’origine de toutes les transactions en cours de toobe restaurée.</span><span class="sxs-lookup"><span data-stu-id="c7bab-206">When you pause or scale your SQL Data Warehouse it is important toounderstand that any in-flight transactions are terminated immediately; causing any open transactions toobe rolled back.</span></span> <span data-ttu-id="c7bab-207">Si votre charge de travail avait émis un long terme et la modification des données incomplètes antérieure toohello pause ou la mise à échelle, puis ce travail devez toobe annulée.</span><span class="sxs-lookup"><span data-stu-id="c7bab-207">If your workload had issued a long running and incomplete data modification prior toohello pause or scale operation, then this work will need toobe undone.</span></span> <span data-ttu-id="c7bab-208">Cela peut avoir un impact sur les temps de hello que toopause nécessaire ou mettre à l’échelle de votre base de données Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c7bab-208">This may impact hello time it takes toopause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c7bab-209">`UPDATE` et `DELETE` correspondant toutes deux à des journalisations complètes, ces opérations d’annulation et de rétablissement peuvent nécessiter un délai considérablement plus important que des journalisations minimales de taille équivalente.</span><span class="sxs-lookup"><span data-stu-id="c7bab-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="c7bab-210">scénario de meilleures Hello est toolet dans les transactions complètes vol données modification précédente toopausing ou mise à l’échelle SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c7bab-210">hello best scenario is toolet in flight data modification transactions complete prior toopausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="c7bab-211">Toutefois, cela n’est pas toujours pratique.</span><span class="sxs-lookup"><span data-stu-id="c7bab-211">However, this may not always be practical.</span></span> <span data-ttu-id="c7bab-212">risque de hello toomitigate une restauration longue, envisagez une des options suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="c7bab-212">toomitigate hello risk of a long rollback, consider one of hello following options:</span></span>

* <span data-ttu-id="c7bab-213">Réécrire les opérations de longue durée à l’aide de [CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="c7bab-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="c7bab-214">Opération de hello se répartissent en plusieurs segments ; fonctionne sur un sous-ensemble de lignes de hello</span><span class="sxs-lookup"><span data-stu-id="c7bab-214">Break hello operation down into chunks; operating on a subset of hello rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7bab-215">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c7bab-215">Next steps</span></span>
<span data-ttu-id="c7bab-216">Consultez [Transactions dans SQL Data Warehouse] [ Transactions in SQL Data Warehouse] toolearn plus d’informations sur les niveaux d’isolement et limites transactionnelles.</span><span class="sxs-lookup"><span data-stu-id="c7bab-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] toolearn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="c7bab-217">Pour une vue d’ensemble des autres bonnes pratiques, consultez [Bonnes pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="c7bab-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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

