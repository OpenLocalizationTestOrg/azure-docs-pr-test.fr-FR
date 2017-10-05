---
title: "Niveau 130 de compatibilité de la base de données - Azure SQL Database | Microsoft Docs"
description: "Dans cet article, nous explorons les avantages liés à l’exécution d’une base de données Azure SQL Database au niveau de compatibilité 130 et tirons parti de nouvelles fonctionnalités comme l’optimiseur de requête et le processeur de requêtes. Nous abordons aussi les éventuels effets secondaires sur les performances des requêtes pour les applications SQL existantes."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: c08c0690df4f389416e4ed2e2df2dbb72d6fd567
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="d1ca8-104">Amélioration des performances des requêtes avec le niveau de compatibilité 130 dans Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d1ca8-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="d1ca8-105">Azure SQL Database exécute en toute transparence des centaines de milliers de bases de données à différents niveaux de compatibilité, en conservant et en garantissant la compatibilité ascendante avec la version correspondante de Microsoft SQL Server pour tous ses clients.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing the backward compatibility to the corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="d1ca8-106">Dans cet article, nous explorons les avantages liés à l’exécution d’une base de données SQL Azure au niveau de compatibilité 130 et tirons parti de nouvelles fonctionnalités comme l’optimiseur de requête et le processeur de requêtes.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-106">In this article, we explore the benefits of running your Azure SQL Databse at compatibility level 130, and leveraging the benefits of the new query optimizer and query processor features.</span></span> <span data-ttu-id="d1ca8-107">Nous abordons aussi les éventuels effets secondaires sur les performances des requêtes pour les applications SQL existantes.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-107">We also address the possible side-effects on the query performance for the existing SQL applications.</span></span>

<span data-ttu-id="d1ca8-108">À titre de rappel historique, la correspondance entre les versions de SQL et les niveaux de compatibilité par défaut est la suivante :</span><span class="sxs-lookup"><span data-stu-id="d1ca8-108">As a reminder of history, the alignment of SQL versions to default compatibility levels are as follows:</span></span>

* <span data-ttu-id="d1ca8-109">100 : dans SQL Server 2008 et Azure SQL Database V11.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="d1ca8-110">110 : dans SQL Server 2012 et Azure SQL Database V11.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="d1ca8-111">120 : dans SQL Server 2014 et Azure SQL Database V12.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="d1ca8-112">130 : dans SQL Server 2016 et Azure SQL Database V12.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1ca8-113">Dès la **mi-juin 2016**, dans Azure SQL Database, le niveau de compatibilité par défaut sera de 130 au lieu de 120 pour les bases de données **nouvellement créées**.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-113">Starting in **mid-June 2016**, in Azure SQL Database, the default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="d1ca8-114">Les bases de données créées avant mi-juin 2016 ne sont *pas* concernées et conservent leur niveau de compatibilité actuel (100, 110 ou 120).</span><span class="sxs-lookup"><span data-stu-id="d1ca8-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="d1ca8-115">Les bases de données qui sont migrées à partir d’Azure SQL Database V11 vers V12 ont un niveau de compatibilité de 100 ou 110.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-115">Databases that migrated from Azure SQL Database version V11 to V12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="d1ca8-116">À propos du niveau de compatibilité 130</span><span class="sxs-lookup"><span data-stu-id="d1ca8-116">About compatibility level 130</span></span>
<span data-ttu-id="d1ca8-117">Tout d’abord, pour connaître le niveau de compatibilité actuel de votre base de données, exécutez l’instruction Transact-SQL suivante.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-117">First, if you want to know the current compatibility level of your database, execute the following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="d1ca8-118">Avant ce passage au niveau 130 pour les **nouvelles** bases de données, examinons les raisons d’un tel changement à l’aide de quelques requêtes très simples et voyons ce que chacun peut en retirer.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-118">Before this change to level 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="d1ca8-119">Le traitement des requêtes dans les bases de données relationnelles peut être très complexe et requérir de grandes compétences en informatique et en mathématiques pour comprendre les choix de conception et les comportements.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-119">Query processing in relational databases can be very complex and can lead to lots of computer science and mathematics to understand the inherent design choices and behaviors.</span></span> <span data-ttu-id="d1ca8-120">Dans ce document, le contenu a été volontairement simplifié pour s’assurer que toute personne disposant de connaissances techniques de base puisse comprendre l’impact du nouveau niveau de compatibilité et déterminer comment bénéficier des applications.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-120">In this document, the content has been intentionally simplified to ensure that anyone with some minimum technical background can understand the impact of the compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="d1ca8-121">Voyons rapidement les apports du niveau de compatibilité 130.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-121">Let’s have a quick look at what the compatibility level 130 brings at the table.</span></span>  <span data-ttu-id="d1ca8-122">Vous trouverez plus de détails dans [Niveau de compatibilité ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), mais voici un bref résumé :</span><span class="sxs-lookup"><span data-stu-id="d1ca8-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="d1ca8-123">L’opération Insert d’une instruction Insert-select peut être multithread ou avoir un plan parallèle. Auparavant, elle était monothread.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-123">The Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="d1ca8-124">La table optimisée en mémoire et les requêtes de variables de table peuvent désormais avoir des plans parallèles. Auparavant, cette opération était également monothread.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="d1ca8-125">Les statistiques de la table optimisée en mémoire peuvent maintenant être échantillonnées et sont mises à jour automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="d1ca8-126">Pour plus d’informations, consultez [Nouveautés : OLTP en mémoire (optimisation en mémoire)](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) .</span><span class="sxs-lookup"><span data-stu-id="d1ca8-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="d1ca8-127">Traitement en mode batch ou en mode ligne avec index columnstore</span><span class="sxs-lookup"><span data-stu-id="d1ca8-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="d1ca8-128">Les tris sur une table avec un index columnstore s’effectuent maintenant en mode batch.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="d1ca8-129">Les agrégats de fenêtres fonctionnent maintenant en mode batch, comme les instructions TSQL LAG/LEAD.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="d1ca8-130">Les requêtes exécutées sur les tables columnstore avec plusieurs clauses distinctes sont traitées en mode batch.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="d1ca8-131">Les requêtes exécutées sous DOP=1 ou avec un plan série sont également traitées en mode batch.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="d1ca8-132">Enfin, les améliorations apportées à l’estimation de la cardinalité sont issues du niveau de compatibilité 120. Pour ceux d’entre vous qui utilisent un niveau de compatibilité antérieur (comme 100 ou 110), le passage au niveau 130 apporte également ces améliorations qui influencent les performances des requêtes de vos applications.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), the move to compatibility level 130 will also bring these improvements, and these can also benefit the query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="d1ca8-133">Mise en pratique du niveau de compatibilité 130</span><span class="sxs-lookup"><span data-stu-id="d1ca8-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="d1ca8-134">Tout d’abord, procurons-nous des tables, des index et des données aléatoires créées pour tester certaines de ces nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-134">First let’s get some tables, indexes and random data created to practice some of these new capabilities.</span></span> <span data-ttu-id="d1ca8-135">Les exemples de script TSQL peuvent s’exécuter sous SQL Server 2016 ou Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-135">The TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="d1ca8-136">Toutefois, lorsque vous créez une base de données SQL Azure, veillez à choisir au moins une base de données P2, car il vous faut deux cœurs au minimum pour utiliser plusieurs threads et tirer parti de ces fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-136">However, when creating an Azure SQL database, make sure you choose at the minimum a P2 database because you need at least a couple of cores to allow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- the second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


<span data-ttu-id="d1ca8-137">Maintenant, intéressons-nous à certaines fonctionnalités de traitement des requêtes, qui sont fournies avec un niveau de compatibilité de 130.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-137">Now, let’s have a look to some of the Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="d1ca8-138">Opération INSERT parallèle</span><span class="sxs-lookup"><span data-stu-id="d1ca8-138">Parallel INSERT</span></span>
<span data-ttu-id="d1ca8-139">Les instructions TSQL ci-dessous exécutent l’opération INSERT sous les niveaux de compatibilité 120 et 130, respectivement dans un modèle monothread (120) et multithread (130).</span><span class="sxs-lookup"><span data-stu-id="d1ca8-139">Executing the TSQL statements below executes the INSERT operation under compatibility level 120 and 130, which respectively executes the INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- The INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- The INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="d1ca8-140">En demandant le plan de requête actuel et en examinant sa représentation sous forme de graphique ou son contenu XML, vous pouvez déterminer la fonction d’estimation de la cardinalité à l’œuvre.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-140">By requesting the actual the query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="d1ca8-141">L’examen des plans côte à côte sur la figure 1 montre clairement que l’opération INSERT avec index columnstore passe du mode série dans le niveau 120 au mode parallèle dans le niveau 130.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-141">Looking at the plans side-by-side on figure 1, we can clearly see that the Column Store INSERT execution goes from serial in 120 to parallel in 130.</span></span> <span data-ttu-id="d1ca8-142">Notez également que l’icône de l’itérateur dans le niveau 130 montre deux flèches parallèles, indiquant une exécution en parallèle.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-142">Also, note that the change of the iterator icon in the 130 plan showing two parallel arrows, illustrating the fact that now the iterator execution is indeed parallel.</span></span> <span data-ttu-id="d1ca8-143">Si vous avez des opérations INSERT volumineuses à traiter, l’exécution en parallèle liée au nombre de cœurs à disposition pour la base de données est plus performante : jusqu’à 100 fois plus rapide selon le cas.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-143">If you have large INSERT operations to complete, the parallel execution, linked to the number of core you have at your disposal for the database, will perform better; up to a 100 times faster depending your situation!</span></span>

<span data-ttu-id="d1ca8-144">*Figure 1 : passage de l’opération INSERT du mode série au mode parallèle dans le niveau de compatibilité 130.*</span><span class="sxs-lookup"><span data-stu-id="d1ca8-144">*Figure 1: INSERT operation changes from serial to parallel with compatibility level 130.*</span></span>

![La figure 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="d1ca8-146">Mode Batch SÉRIE</span><span class="sxs-lookup"><span data-stu-id="d1ca8-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="d1ca8-147">Dans le niveau de compatibilité 130, le traitement des lignes de données s’effectue en mode batch.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-147">Similarly, moving to compatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="d1ca8-148">Tout d’abord, les opérations en mode batch ne sont disponibles que si vous avez un index columnstore.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="d1ca8-149">Ensuite, un batch qui représente 900 lignes environ utilise une logique de code optimisée pour un processeur multicœur et un débit de mémoire supérieur. Dans la mesure du possible, il exploite directement les données compressées de l’index columnstore.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages the compressed data of the Column Store whenever possible.</span></span> <span data-ttu-id="d1ca8-150">C’est ainsi que SQL Server 2016 peut traiter environ 900 lignes à la fois, au lieu de 1 ligne à la fois. Par conséquent, le temps système de l’opération est maintenant partagé par l’ensemble du batch, ce qui réduit le coût global par ligne.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at the time, and as a consequence, the overall overhead cost of the operation is now shared by the entire batch, reducing the overall cost by row.</span></span> <span data-ttu-id="d1ca8-151">Cette quantité partagée d’opérations, combinée avec la compression des index columnstore, réduit la latence inhérente d’une opération SELECT en mode batch.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-151">This shared amount of operations combined with the column store compression basically reduces the latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="d1ca8-152">Pour en savoir plus sur l’index columnstore et le mode batch, consultez [Description des index columnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1ca8-152">You can find more details about the column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="d1ca8-153">L’examen des plans de requête côte à côte sur la figure 2 montre que le mode de traitement a changé avec le niveau de compatibilité. Par conséquent, l’exécution des requêtes dans les deux niveaux de compatibilité révèle que le temps de traitement est majoritairement en mode ligne (86 %) avec 14 % seulement en mode batch, où 2 lots ont été traités.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-153">As visible below, by observing the query plans side-by-side on figure 2, we can see that the processing mode has changed with the compatibility level, and as a consequence, when executing the queries in both compatibility level altogether, we can see that most of the processing time is spent in row mode (86%) compared to the batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="d1ca8-154">Plus le jeu de données est volumineux, moins cet avantage est marqué.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-154">Increase the dataset, the benefit will increase.</span></span>

<span data-ttu-id="d1ca8-155">*Figure 2 : passage de l’opération SELECT du mode série au mode parallèle dans le niveau de compatibilité 130.*</span><span class="sxs-lookup"><span data-stu-id="d1ca8-155">*Figure 2: SELECT operation changes from serial to batch mode with compatibility level 130.*</span></span>

![Figure 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="d1ca8-157">Opération SORT en mode batch</span><span class="sxs-lookup"><span data-stu-id="d1ca8-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="d1ca8-158">Cas similaire au précédent mais appliqué à une opération de tri, la transition de mode ligne (niveau de compatibilité 120) au mode batch (niveau de compatibilité 130) améliore les performances de l’opération SORT pour les mêmes raisons.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-158">Similar to the above, but applied to a sort operation, the transition from row mode (compatibility level 120) to batch mode (compatibility level 130) improves the performance of the SORT operation for the same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="d1ca8-159">La figure 3 montre que l’opération SORT en mode ligne représente 81 % du coût, tandis que le mode batch ne représente que 19 % du coût (respectivement 81 et 56 % du tri).</span><span class="sxs-lookup"><span data-stu-id="d1ca8-159">Visible side-by-side on figure 3, we can see that the sort operation in row mode represents 81% of the cost, while the batch mode only represents 19% of the cost (respectively 81% and 56% on the sort itself).</span></span>

<span data-ttu-id="d1ca8-160">*Figure 3 : passage de l’opération SORT du mode série au mode parallèle avec le niveau de compatibilité 130.*</span><span class="sxs-lookup"><span data-stu-id="d1ca8-160">*Figure 3: SORT operation changes from row to batch mode with compatibility level 130.*</span></span>

![Figure 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="d1ca8-162">Bien sûr, ces exemples ne contiennent que des dizaines de milliers de lignes, ce qui n’est rien par rapport aux données disponibles dans la plupart des serveurs SQL aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at the data available in most SQL Servers these days.</span></span> <span data-ttu-id="d1ca8-163">Mais, projetez ces résultats sur plusieurs millions de lignes, et le gain peut se chiffrer en quelques minutes d’exécution par jour, selon la nature de votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending the nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="d1ca8-164">Améliorations de l’estimation de la cardinalité</span><span class="sxs-lookup"><span data-stu-id="d1ca8-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="d1ca8-165">Depuis SQL Server 2014, une base de données exécutée au moins au niveau de compatibilité 120 utilise la nouvelle fonctionnalité d’estimation de la cardinalité.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="d1ca8-166">En fait, l’estimation de la cardinalité désigne la logique utilisée pour déterminer comment SQL Server exécute une requête en fonction de son coût estimé.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-166">Essentially, cardinality estimation is the logic used to determine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="d1ca8-167">Cette estimation est calculée à l’aide de données statistiques associées aux objets impliqués dans cette requête.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-167">The estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="d1ca8-168">En pratique, globalement, les fonctions d’estimation de la cardinalité estiment le nombre de lignes et indiquent la distribution des valeurs, le nombre de valeurs distinctes et les nombres en double dans les tables et objets référencés dans la requête.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about the distribution of the values, distinct value counts, and duplicate counts contained in the tables and objects referenced in the query.</span></span> <span data-ttu-id="d1ca8-169">Toute erreur dans ces estimations peut, entre autres, générer des E/S superflues en raison d’allocations de mémoire insuffisantes (comme des saturations de TempDB) ou faire opter pour le mode d’exécution en série plutôt qu’en parallèle.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-169">Getting these estimates wrong, can lead to unnecessary disk I/O due to insufficient memory grants (i.e. TempDB spills), or to a selection of a serial plan execution over a parallel plan execution, to name a few.</span></span> <span data-ttu-id="d1ca8-170">En conclusion, des estimations fausses peuvent avoir un impact négatif sur les performances d’exécution des requêtes.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-170">Conclusion, incorrect estimates can lead to an overall performance degradation of the query execution.</span></span> <span data-ttu-id="d1ca8-171">Mais, des estimations exactes, plus précises, améliorent l’exécution des requêtes !</span><span class="sxs-lookup"><span data-stu-id="d1ca8-171">On the other side, better estimates, more accurate estimates, leads to better query executions!</span></span>

<span data-ttu-id="d1ca8-172">Comme nous l’avons déjà dit, l’optimisation des requêtes et l’estimation sont un sujet complexe. Mais si vous souhaitez en savoir plus sur les plans de requête et l’estimation de la cardinalité, consultez [Optimiser vos plans de requête avec l’estimation de la cardinalité dans SQL Server 2014](https://msdn.microsoft.com/library/dn673537.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1ca8-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want to learn more about query plans and cardinality estimator, you can refer to the document at [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="d1ca8-173">Quelle estimation de la cardinalité utilisez-vous actuellement ?</span><span class="sxs-lookup"><span data-stu-id="d1ca8-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="d1ca8-174">Pour déterminer l’estimation de la cardinalité sous laquelle vos requêtes sont exécutées, nous allons utiliser les exemples de requête ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-174">To determine under which Cardinality Estimation your queries are running, let’s just use the query samples below.</span></span> <span data-ttu-id="d1ca8-175">Notez que ce premier exemple s’exécutera sous le niveau de compatibilité 110, ce qui implique l’utilisation des anciennes fonctions d’estimation de la cardinalité.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-175">Note that this first example will run under compatibility level 110, implying the use of the old Cardinality Estimation functions.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="d1ca8-176">Une fois l’exécution terminée, cliquez sur le lien XML et examinez les propriétés du premier itérateur indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-176">Once execution is complete, click on the XML link, and look at the properties of the first iterator as shown below.</span></span> <span data-ttu-id="d1ca8-177">Notez que la propriété appelée CardinalityEstimationModelVersion a pour valeur 70.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-177">Note the property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="d1ca8-178">Cela ne signifie pas que le niveau de compatibilité de la base de données est défini pour SQL Server 7.0 (soit 110 comme le montrent les instructions TSQL ci-dessus). La valeur 70 représente simplement la fonctionnalité d’estimation de la cardinalité disponible depuis SQL Server 7.0, qui n’a fait l’objet d’aucune révision majeure jusqu’à SQL Server 2014 (fourni avec le niveau de compatibilité 120).</span><span class="sxs-lookup"><span data-stu-id="d1ca8-178">It does not mean that the database compatibility level is set to the SQL Server 7.0 version (it is set on 110 as visible in the TSQL statements above), but the value 70 simply represents the legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="d1ca8-179">*Figure 4 : la propriété CardinalityEstimationModelVersion est égale à 70 si vous utilisez le niveau de compatibilité 110 ou un niveau antérieur.*</span><span class="sxs-lookup"><span data-stu-id="d1ca8-179">*Figure 4: The CardinalityEstimationModelVersion is set to 70 when using a compatibility level of 110 or below.*</span></span>

![Figure 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="d1ca8-181">Vous pouvez également opter pour le niveau de compatibilité 130 et désactiver l’utilisation de la nouvelle fonction d’estimation de la cardinalité en réglant LEGACY_CARDINALITY_ESTIMATION sur ON avec [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1ca8-181">Alternatively, you can change the compatibility level to 130, and disable the use of the new Cardinality Estimation function by using the LEGACY_CARDINALITY_ESTIMATION set to ON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="d1ca8-182">La situation sera rigoureusement identique au niveau 110 du point de vue de la fonction d’estimation de la cardinalité, si vous utilisez le niveau de compatibilité le plus récent.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-182">This will be exactly the same as using 110 from a Cardinality Estimation function point of view, while using the latest query processing compatibility level.</span></span> <span data-ttu-id="d1ca8-183">Ainsi, vous pouvez tirer parti des nouvelles fonctionnalités de traitement des requêtes offertes par le dernier niveau de compatibilité (c’est-à-dire en mode batch), tout en utilisant l’ancienne fonctionnalité d’estimation de la cardinalité au besoin.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-183">Doing so, you can benefit from the new query processing features coming with the latest compatibility level (i.e. batch mode), but still rely on the old Cardinality Estimation functionality if necessary.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="d1ca8-184">Le passage au niveau de compatibilité 120 ou 130 active la nouvelle fonctionnalité d’estimation de la cardinalité.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-184">Simply moving to the compatibility level 120 or 130 enables the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="d1ca8-185">Dans ce cas, la propriété CardinalityEstimationModelVersion par défaut prend la valeur 120 ou 130, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-185">In such a case, the default CardinalityEstimationModelVersion will be set accordingly to 120 or 130 as visible below.</span></span>

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="d1ca8-186">*Figure 5 : propriété CardinalityEstimationModelVersion égale à 130 en cas d’utilisation du niveau de compatibilité 130.*</span><span class="sxs-lookup"><span data-stu-id="d1ca8-186">*Figure 5: The CardinalityEstimationModelVersion is set to 130 when using a compatibility level of 130.*</span></span>

![Figure 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-the-cardinality-estimation-differences"></a><span data-ttu-id="d1ca8-188">Constatation de différences dans l’estimation de la cardinalité</span><span class="sxs-lookup"><span data-stu-id="d1ca8-188">Witnessing the Cardinality Estimation differences</span></span>
<span data-ttu-id="d1ca8-189">À présent, nous allons exécuter une requête légèrement plus complexe, comprenant une instruction INNER JOIN avec une clause WHERE et des prédicats, et voir le nombre de lignes estimées par l’ancienne fonction d’estimation de la cardinalité.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at the row count estimate from the old Cardinality Estimation function first.</span></span>

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="d1ca8-190">L’exécution de cette requête renvoie 200 704 lignes, alors que la fonctionnalité d’estimation de la cardinalité en avait compté 194 284.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-190">Executing this query effectively returns 200,704 rows, while the row estimate with the old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="d1ca8-191">Bien sûr, comme nous l’avons déjà vu, ces nombres de lignes dépendent également de la fréquence d’exécution des requêtes précédentes, qui augmente la taille des tables à chaque exécution.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-191">Obviously, as said before, these row count results will also depend how often you ran the previous samples, which populates the sample tables over and over again at each run.</span></span> <span data-ttu-id="d1ca8-192">Évidemment, les prédicats de votre requête ont également une influence sur l’estimation, tout comme la forme de la table, les données contenues et leurs corrélations avec les autres types de données.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-192">Obviously, the predicates in your query will also have an influence on the actual estimation aside from the table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="d1ca8-193">*Figure 6 : le nombre de lignes estimé est de 194 284, soit 6 000 de moins que les 200 704 attendues.*</span><span class="sxs-lookup"><span data-stu-id="d1ca8-193">*Figure 6: The row count estimate is 194,284 or 6,000 rows off from the 200,704 rows expected.*</span></span>

![Figure 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="d1ca8-195">Nous allons maintenant exécuter la même requête avec la nouvelle fonctionnalité d’estimation de la cardinalité.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-195">In the same way, let’s now execute the same query with the new Cardinality Estimation functionality.</span></span>

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="d1ca8-196">Comme vous le voyez, le nombre de lignes estimé est de 202 877, une valeur plus proche de la précédente estimation et légèrement supérieure à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-196">Looking at the below, we now see that the row estimate is 202,877, or much closer and higher than the old Cardinality Estimation.</span></span>

<span data-ttu-id="d1ca8-197">*Figure 7 : le nombre de lignes estimé est désormais de 202 877, au lieu de 194 284.*</span><span class="sxs-lookup"><span data-stu-id="d1ca8-197">*Figure 7: The row count estimate is now 202,877, instead of 194,284.*</span></span>

![Figure 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="d1ca8-199">En réalité, le jeu de résultats contient 200 704 lignes. Mais tout dépend de la fréquence selon laquelle vous avez exécuté les requêtes des exemples précédents. Surtout, comme le TSQL utilise l’instruction RAND(), les valeurs réelles renvoyées peuvent varier d’une exécution à l’autre.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-199">In reality, the result set is 200,704 rows (but all of it depends how often you did run the queries of the previous samples, but more importantly, because the TSQL uses the RAND() statement, the actual values returned can vary from one run to the next).</span></span> <span data-ttu-id="d1ca8-200">Par conséquent, dans cet exemple, la nouvelle estimation de la cardinalité est plus précise dans le nombre de lignes calculé, car 202 877 est beaucoup plus proche de 200 704 que 194 284.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-200">Therefore, in this particular example, the new Cardinality Estimation does a better job at estimating the number of rows because 202,877 is much closer to 200,704, than 194,284!</span></span> <span data-ttu-id="d1ca8-201">Enfin, si vous modifiez des prédicats de la clause WHERE en incluant un signe d’égalité (au lieu de « > » par exemple), les estimations entre l’ancienne et nouvelle fonction de cardinalité peuvent diverger encore davantage, selon le nombre de correspondances obtenues.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-201">Last, if you change the WHERE clause predicates to equality (rather than “>” for instance), this could make the estimates between the old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="d1ca8-202">En l’occurrence, une estimation inférieure de 6 000 lignes par rapport au nombre réel ne représente pas une grande quantité de données dans certaines situations.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="d1ca8-203">Maintenant, transposez ce cas de figure à des millions de lignes entre plusieurs tables, avec des requêtes plus complexes. L’estimation peut parfois être inférieure de plusieurs millions de lignes, entraînant le choix d’un mauvais plan d’exécution ou exigeant des allocations de mémoire insuffisantes à l’origine d’une saturation de TempDB et d’une augmentation importante des E/S.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-203">Now, transpose this to millions of rows across several tables and more complex queries, and at times the estimate can be off by millions of rows , and therefore, the risk of picking-up the wrong execution plan, or requesting insufficient memory grants leading to TempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="d1ca8-204">Si vous en avez la possibilité, testez cette comparaison sur vos requêtes et vos jeux de données, et voyez dans quelle mesure les estimations (anciennes et nouvelles) sont affectées. Parfois, le nombre obtenu peut être très inférieur à la réalité ou beaucoup plus proche du nombre renvoyé dans le résultat.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-204">If you have the opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of the old and new estimates are affected, while some could just become more off from the reality, or some others just simply closer to the actual row counts actually returned in the result sets.</span></span> <span data-ttu-id="d1ca8-205">Tout cela dépend de la forme de vos requêtes, des caractéristiques de la base de données SQL Azure, de la nature et de la taille de vos jeux de données, ainsi que des statistiques disponibles sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-205">All of it will depend of the shape of your queries, the Azure SQL database characteristics, the nature and the size of your datasets, and the statistics available about them.</span></span> <span data-ttu-id="d1ca8-206">Si vous venez de créer votre instance Azure SQL Database, l’optimiseur de requête doit partir de zéro et ne peut pas réutiliser les statistiques des exécutions précédentes.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-206">If you just created your Azure SQL Database instance, the query optimizer will have to build its knowledge from scratch instead of reusing statistics made of the previous query runs.</span></span> <span data-ttu-id="d1ca8-207">Les estimations sont donc très contextuelles et souvent propres à chaque serveur et chaque application.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-207">So, the estimates are very contextual and almost specific to every server and application situation.</span></span> <span data-ttu-id="d1ca8-208">C’est un aspect important à prendre en compte.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-208">It is an important aspect to keep in mind!</span></span>

## <a name="some-considerations-to-take-into-account"></a><span data-ttu-id="d1ca8-209">Quelques éléments à prendre en compte</span><span class="sxs-lookup"><span data-stu-id="d1ca8-209">Some considerations to take into account</span></span>
<span data-ttu-id="d1ca8-210">La plupart des charges de travail auraient intérêt à utiliser le niveau de compatibilité 130. Mais, avant d’adopter le niveau de compatibilité approprié à votre environnement de production, vous avez 3 possibilités :</span><span class="sxs-lookup"><span data-stu-id="d1ca8-210">Although most workloads would benefit from the compatibility level 130, before you adopting the compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="d1ca8-211">Vous passez au niveau de compatibilité 130 et vous évaluez la situation.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-211">You move to compatibility level 130, and see how things perform.</span></span> <span data-ttu-id="d1ca8-212">Si vous remarquez des régressions revenez au niveau de compatibilité d’origine ou conservez le niveau 130 et ne restaurez que l’ancien mode de la fonction d’estimation de la cardinalité (comme expliqué ci-avant, cette opération peut, à elle seule, résoudre le problème).</span><span class="sxs-lookup"><span data-stu-id="d1ca8-212">In case you notice some regressions, you just simply set the compatibility level back to its original level, or keep 130, and only reverse the Cardinality Estimation back to the legacy mode (As explained above, this alone could address the issue).</span></span>
2. <span data-ttu-id="d1ca8-213">Vous testez complètement vos applications avec une charge de production similaire, puis vous affinez et validez les performances avant de passer en production.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-213">You thoroughly test your existing applications under similar production load, fine tune, and validate the performance before going to production.</span></span> <span data-ttu-id="d1ca8-214">En cas de problèmes, procédez comme indiqué plus haut : vous pouvez revenir au niveau de compatibilité d’origine ou simplement rétablir l’ancien mode de la fonction d’estimation de la cardinalité.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-214">In case of issues, same as above, you can always go back to the original compatibility level, or simply reverse the Cardinality Estimation back to the legacy mode.</span></span>
3. <span data-ttu-id="d1ca8-215">La dernière possibilité et la plus récente pour résoudre ces problèmes, consiste à utiliser le magasin des requêtes.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-215">As a final option, and the most recent way to address these questions, is to leverage the Query Store.</span></span> <span data-ttu-id="d1ca8-216">Et c’est l’option recommandée aujourd’hui !</span><span class="sxs-lookup"><span data-stu-id="d1ca8-216">That’s today’s recommended option!</span></span> <span data-ttu-id="d1ca8-217">Pour faciliter l’analyse de vos requêtes avec le niveau de compatibilité 120 ou antérieur et le niveau 130, nous vous encourageons vivement à utiliser le magasin des requêtes.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-217">To assist the analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough to use Query Store.</span></span> <span data-ttu-id="d1ca8-218">Disponible dans la dernière version d’Azure SQL Database V12, le magasin des requêtes est conçu pour vous aider à résoudre les problèmes de performance des requêtes.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-218">Query Store is available with the latest version of Azure SQL Database V12, and it’s designed to help you with query performance troubleshooting.</span></span> <span data-ttu-id="d1ca8-219">Considérez-le comme un enregistreur qui collecte et met en forme des informations historiques détaillées sur toutes les requêtes.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-219">Think of the Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="d1ca8-220">Il simplifie considérablement l’analyse des performances en accélérant le diagnostic et la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-220">This greatly simplifies performance forensics by reducing the time to diagnose and resolve issues.</span></span> <span data-ttu-id="d1ca8-221">Pour en savoir plus, consultez [Magasin des requêtes : un enregistreur de données pour votre base de données](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span><span class="sxs-lookup"><span data-stu-id="d1ca8-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="d1ca8-222">Globalement, si vous avez plusieurs bases de données au niveau de compatibilité 120 ou à un niveau antérieur, et que vous prévoyez d’en faire passer certaines au niveau 130, ou si votre charge de travail approvisionne automatiquement les nouvelles bases de données bientôt associées par défaut au niveau 130, prenez en compte les points suivants :</span><span class="sxs-lookup"><span data-stu-id="d1ca8-222">At the high-level, if you already have a set of databases running at compatibility level 120 or below, and plan to move some of them to 130, or because your workload automatically provision new databases that will be soon be set by default to 130, please consider the followings:</span></span>

* <span data-ttu-id="d1ca8-223">Avant de passer au nouveau niveau de compatibilité en production, activez le magasin des requêtes.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-223">Before changing to the new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="d1ca8-224">Pour en savoir plus, consultez [Migrer des plans de requête](https://msdn.microsoft.com/library/bb895281.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d1ca8-224">You can refer to [Change the Database Compatibility Mode and Use the Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="d1ca8-225">Ensuite, testez toutes les charges de travail critiques à l’aide de requêtes et de données représentatives d’un environnement de production et comparez les performances constatées à celles relevées par le magasin des requêtes.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare the performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="d1ca8-226">Si vous rencontrez des régressions, vous pouvez identifier les requêtes concernées à l’aide du magasin des requêtes et utiliser l’option de forçage du plan (également appelée épinglage du plan).</span><span class="sxs-lookup"><span data-stu-id="d1ca8-226">If you experience some regressions, you can identify the regressed queries with the Query Store and use the plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="d1ca8-227">Dans ce cas, vous conservez le niveau de compatibilité 130 et utilisez le plan de requête précédent, comme ce que suggère le magasin des requêtes.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-227">In such a case, you definitively stay with the compatibility level 130, and use the former query plan as suggested by the Query Store.</span></span>
* <span data-ttu-id="d1ca8-228">Si vous souhaitez tirer parti des nouvelles fonctionnalités d’Azure SQL Database (qui exécute SQL Server 2016), mais que vous êtes sensible aux modifications apportées par le niveau de compatibilité 130, vous pouvez en dernier recours envisager de forcer le retour au niveau de compatibilité qui convient à votre charge de travail à l’aide d’une instruction ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-228">If you want to leverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive to changes brought by the compatibility level 130, as a last resort, you could consider forcing the compatibility level back to the level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="d1ca8-229">Mais sachez que l’option de forçage de plan du Magasin des requêtes est votre meilleure option, car ne pas utiliser le niveau 130 revient à rester au niveau fonctionnel d’une ancienne version de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-229">But first, be aware that the Query Store plan pinning option is your best option because not using 130 is basically staying at the functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="d1ca8-230">Si vous avez des applications multilocataires dans plusieurs bases de données, il peut être nécessaire de mettre à jour la logique d’approvisionnement de vos bases de données afin d’assurer un niveau de compatibilité cohérent à toutes les bases de données.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-230">If you have multitenant applications spanning multiple databases, it may be necessary to update the provisioning logic of your databases to ensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="d1ca8-231">Les performances de la charge de travail de votre application peuvent varier lorsque certaines bases de données fonctionnent à des niveaux de compatibilité différents. Par conséquent, l’utilisation d’un niveau de compatibilité cohérent sur toutes les bases de données peut être requise pour offrir la même expérience à l’ensemble de vos clients.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-231">Your application workload performance could be sensitive to the fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order to provide the same experience to your customers all across the board.</span></span> <span data-ttu-id="d1ca8-232">Ceci n’est pas une obligation. Tout dépend de la façon dont votre application est affectée par le niveau de compatibilité.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-232">Note that it is not a mandate, it really depends on how your application is affected by the compatibility level.</span></span>
* <span data-ttu-id="d1ca8-233">Enfin, concernant l’estimation de la cardinalité et comme pour la modification du niveau de compatibilité avant le passage en production, il est recommandé de tester votre charge de travail de production dans les nouvelles conditions pour déterminer si votre application tire parti des améliorations de l’estimation de la cardinalité.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-233">Last, regarding the Cardinality Estimation, and just like changing the compatibility level, before proceeding in production, it is recommended to test your production workload under the new conditions to determine if your application benefits from the Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="d1ca8-234">Conclusion</span><span class="sxs-lookup"><span data-stu-id="d1ca8-234">Conclusion</span></span>
<span data-ttu-id="d1ca8-235">L’utilisation d’Azure SQL Database pour tirer parti de toutes les améliorations de SQL Server 2016 améliore nettement l’exécution des requêtes.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-235">Using Azure SQL Database to benefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="d1ca8-236">C’est vrai !</span><span class="sxs-lookup"><span data-stu-id="d1ca8-236">Just as-is!</span></span> <span data-ttu-id="d1ca8-237">Bien sûr, comme pour toute nouvelle fonctionnalité, il convient d’effectuer une évaluation appropriée afin de déterminer les conditions optimales de la charge de travail de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-237">Of course, like any new feature, a proper evaluation must be done to determine the exact conditions under which your database workload operates the best.</span></span> <span data-ttu-id="d1ca8-238">L’expérience montre que la plupart des charges de travail s’exécutent de manière transparente avec le niveau de compatibilité 130, tout en tirant parti des nouvelles fonctions de traitement des requêtes et de la nouvelle fonctionnalité d’estimation de la cardinalité.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-238">Experience shows that most workload are expected to at least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="d1ca8-239">Ceci dit, en pratique, il existe toujours des exceptions. Une évaluation est donc indispensable pour déterminer dans quelle mesure vous pouvez bénéficier de ces améliorations.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment to determine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="d1ca8-240">Là encore, le magasin des requêtes peut être très utile !</span><span class="sxs-lookup"><span data-stu-id="d1ca8-240">And again, the Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="d1ca8-241">Compte tenu de l’évolution de SQL Azure, vous pouvez espérer un niveau de compatibilité 140 très bientôt.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-241">As SQL Azure evolves, you can expect a compatibility level 140 in the future.</span></span> <span data-ttu-id="d1ca8-242">Le temps venu, nous discuterons des apports de ce niveau de compatibilité 140, comme nous venons d’expliquer brièvement les avantages du niveau 130 aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="d1ca8-243">Pour l’instant, n’oublions pas qu’à partir de juin 2016, Azure SQL Database passe au niveau de compatibilité 130 par défaut pour les bases de données créées.</span><span class="sxs-lookup"><span data-stu-id="d1ca8-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change the default compatibility level from 120 to 130 for newly created databases.</span></span> <span data-ttu-id="d1ca8-244">Prenez date !</span><span class="sxs-lookup"><span data-stu-id="d1ca8-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="d1ca8-245">Références</span><span class="sxs-lookup"><span data-stu-id="d1ca8-245">References</span></span>
* [<span data-ttu-id="d1ca8-246">Nouveautés (moteur de base de données)</span><span class="sxs-lookup"><span data-stu-id="d1ca8-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="d1ca8-247">Blog : Le magasin des requêtes : un enregistreur de données pour votre base de données par Borko Novakovic, 8 juin 2016</span><span class="sxs-lookup"><span data-stu-id="d1ca8-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="d1ca8-248">Niveau de compatibilité ALTER TABLE (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="d1ca8-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="d1ca8-249">ALTER DATABASE SCOPED CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="d1ca8-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="d1ca8-250">Niveau de compatibilité 130 pour Azure SQL Database V12</span><span class="sxs-lookup"><span data-stu-id="d1ca8-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="d1ca8-251">Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator (Optimiser vos plans de requêtes avec l’Estimateur de la cardinalité de SQL Server 2014)</span><span class="sxs-lookup"><span data-stu-id="d1ca8-251">Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="d1ca8-252">Description des index columnstore</span><span class="sxs-lookup"><span data-stu-id="d1ca8-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="d1ca8-253">Blog : Amélioration des performances des requêtes avec le niveau de compatibilité 130 dans Azure SQL Database, par Alain Lissoir, 6 mai 2016</span><span class="sxs-lookup"><span data-stu-id="d1ca8-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
