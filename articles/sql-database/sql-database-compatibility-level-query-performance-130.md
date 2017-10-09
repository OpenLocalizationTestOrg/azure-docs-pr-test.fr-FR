---
title: "niveau de compatibilité aaaDatabase 130 - base de données SQL Azure | Documents Microsoft"
description: "Dans cet article, nous Découvrez les avantages de hello de votre base de données SQL Azure en cours d’exécution au niveau de compatibilité 130 et tirant parti des avantages de hello du nouvel optimiseur de requête hello et interroger les fonctionnalités du processeur. Nous avons également adresser hello possible des effets sur les performances des requêtes hello pour les applications SQL existantes hello."
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
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="e398d-104">Amélioration des performances des requêtes avec le niveau de compatibilité 130 dans Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e398d-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="e398d-105">Base de données SQL Azure est en cours d’exécution en toute transparence des centaines de milliers de bases de données à plusieurs niveaux de compatibilité, ce qui garantit la version correspondante du toohello hello compatibilité descendante de Microsoft SQL Server pour tous ses clients et de conservation !</span><span class="sxs-lookup"><span data-stu-id="e398d-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing hello backward compatibility toohello corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="e398d-106">Dans cet article, nous Découvrez les avantages de hello de votre base de données SQL Azure en cours d’exécution au niveau de compatibilité 130 et tirant parti des avantages de hello du nouvel optimiseur de requête hello et interroger les fonctionnalités du processeur.</span><span class="sxs-lookup"><span data-stu-id="e398d-106">In this article, we explore hello benefits of running your Azure SQL Databse at compatibility level 130, and leveraging hello benefits of hello new query optimizer and query processor features.</span></span> <span data-ttu-id="e398d-107">Nous avons également adresser hello possible des effets sur les performances des requêtes hello pour les applications SQL existantes hello.</span><span class="sxs-lookup"><span data-stu-id="e398d-107">We also address hello possible side-effects on hello query performance for hello existing SQL applications.</span></span>

<span data-ttu-id="e398d-108">En guise de rappel de l’historique, alignement hello de niveaux de compatibilité SQL versions toodefault sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e398d-108">As a reminder of history, hello alignment of SQL versions toodefault compatibility levels are as follows:</span></span>

* <span data-ttu-id="e398d-109">100 : dans SQL Server 2008 et Azure SQL Database V11.</span><span class="sxs-lookup"><span data-stu-id="e398d-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="e398d-110">110 : dans SQL Server 2012 et Azure SQL Database V11.</span><span class="sxs-lookup"><span data-stu-id="e398d-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="e398d-111">120 : dans SQL Server 2014 et Azure SQL Database V12.</span><span class="sxs-lookup"><span data-stu-id="e398d-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="e398d-112">130 : dans SQL Server 2016 et Azure SQL Database V12.</span><span class="sxs-lookup"><span data-stu-id="e398d-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e398d-113">À compter de **mid-juin 2016**, dans la base de données SQL Azure, le niveau de compatibilité par défaut hello sera 130 au lieu de 120 pour **nouvellement créé** bases de données.</span><span class="sxs-lookup"><span data-stu-id="e398d-113">Starting in **mid-June 2016**, in Azure SQL Database, hello default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="e398d-114">Les bases de données créées avant mi-juin 2016 ne sont *pas* concernées et conservent leur niveau de compatibilité actuel (100, 110 ou 120).</span><span class="sxs-lookup"><span data-stu-id="e398d-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="e398d-115">Bases de données migrées à partir de la version de base de données SQL Azure V11 tooV12 aura un niveau de compatibilité de 110 ou 100.</span><span class="sxs-lookup"><span data-stu-id="e398d-115">Databases that migrated from Azure SQL Database version V11 tooV12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="e398d-116">À propos du niveau de compatibilité 130</span><span class="sxs-lookup"><span data-stu-id="e398d-116">About compatibility level 130</span></span>
<span data-ttu-id="e398d-117">Tout d’abord, si vous souhaitez tooknow hello niveau de compatibilité actuel de votre base de données, exécutez hello instruction Transact-SQL suivante.</span><span class="sxs-lookup"><span data-stu-id="e398d-117">First, if you want tooknow hello current compatibility level of your database, execute hello following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="e398d-118">Avant cette modification toolevel 130 se pour **qui vient d’être** créé les bases de données, nous allons examiner cette modification Nouveautés concernant le parcourir des exemples de requête très basique et voir comment tout le monde peut bénéficier à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="e398d-118">Before this change toolevel 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="e398d-119">Le traitement des requêtes dans les bases de données relationnelles peut être très complexe et peut entraîner des toolots de l’ordinateur pour la science et mathématiques toounderstand hello inhérents aux choix de conception et les comportements.</span><span class="sxs-lookup"><span data-stu-id="e398d-119">Query processing in relational databases can be very complex and can lead toolots of computer science and mathematics toounderstand hello inherent design choices and behaviors.</span></span> <span data-ttu-id="e398d-120">Dans ce document, le contenu de hello a été intentionnellement simplifié tooensure que toute personne disposant d’un contexte technique minimal peut comprendre l’impact de hello de modification du niveau de compatibilité hello et déterminer comment il peut bénéficier des applications.</span><span class="sxs-lookup"><span data-stu-id="e398d-120">In this document, hello content has been intentionally simplified tooensure that anyone with some minimum technical background can understand hello impact of hello compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="e398d-121">Nous allons ont un coup de œil rapide à quel niveau de compatibilité 130 hello met dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="e398d-121">Let’s have a quick look at what hello compatibility level 130 brings at hello table.</span></span>  <span data-ttu-id="e398d-122">Vous trouverez plus de détails dans [Niveau de compatibilité ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), mais voici un bref résumé :</span><span class="sxs-lookup"><span data-stu-id="e398d-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="e398d-123">peut être multithread Hello opération d’insertion d’une instruction Insert select ou peut avoir un plan parallèle, alors que cette opération n’était pas monothread.</span><span class="sxs-lookup"><span data-stu-id="e398d-123">hello Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="e398d-124">La table optimisée en mémoire et les requêtes de variables de table peuvent désormais avoir des plans parallèles. Auparavant, cette opération était également monothread.</span><span class="sxs-lookup"><span data-stu-id="e398d-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="e398d-125">Les statistiques de la table optimisée en mémoire peuvent maintenant être échantillonnées et sont mises à jour automatiquement.</span><span class="sxs-lookup"><span data-stu-id="e398d-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="e398d-126">Pour plus d’informations, consultez [Nouveautés : OLTP en mémoire (optimisation en mémoire)](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) .</span><span class="sxs-lookup"><span data-stu-id="e398d-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="e398d-127">Traitement en mode batch ou en mode ligne avec index columnstore</span><span class="sxs-lookup"><span data-stu-id="e398d-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="e398d-128">Les tris sur une table avec un index columnstore s’effectuent maintenant en mode batch.</span><span class="sxs-lookup"><span data-stu-id="e398d-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="e398d-129">Les agrégats de fenêtres fonctionnent maintenant en mode batch, comme les instructions TSQL LAG/LEAD.</span><span class="sxs-lookup"><span data-stu-id="e398d-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="e398d-130">Les requêtes exécutées sur les tables columnstore avec plusieurs clauses distinctes sont traitées en mode batch.</span><span class="sxs-lookup"><span data-stu-id="e398d-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="e398d-131">Les requêtes exécutées sous DOP=1 ou avec un plan série sont également traitées en mode batch.</span><span class="sxs-lookup"><span data-stu-id="e398d-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="e398d-132">Enfin, améliorations de l’Estimation de cardinalité proviennent en fait avec le niveau de compatibilité 120, mais pour ceux en cours d’exécution au niveau de compatibilité inférieure au niveau (par exemple, 100 et 110), hello déplacement toocompatibility niveau 130 sera également mettre ces améliorations et ces sites peuvent également améliorer les performances des requêtes hello de vos applications.</span><span class="sxs-lookup"><span data-stu-id="e398d-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), hello move toocompatibility level 130 will also bring these improvements, and these can also benefit hello query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="e398d-133">Mise en pratique du niveau de compatibilité 130</span><span class="sxs-lookup"><span data-stu-id="e398d-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="e398d-134">Première passons certaines tables, les index et les données aléatoires créées toopractice certaines de ces nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="e398d-134">First let’s get some tables, indexes and random data created toopractice some of these new capabilities.</span></span> <span data-ttu-id="e398d-135">exemples de script TSQL Hello peuvent être exécutées sous SQL Server 2016, ou base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e398d-135">hello TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="e398d-136">Toutefois, lors de la création d’une base de données SQL Azure, assurez-vous que vous choisissez à hello minimale P2 de base de données, car vous devez au moins deux cœurs tooallow de multi-threading et donc tirer parti de ces fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="e398d-136">However, when creating an Azure SQL database, make sure you choose at hello minimum a P2 database because you need at least a couple of cores tooallow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

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


<span data-ttu-id="e398d-137">Maintenant, nous allons ont un toosome détaillée des fonctionnalités de traitement des requêtes hello avec le niveau de compatibilité 130.</span><span class="sxs-lookup"><span data-stu-id="e398d-137">Now, let’s have a look toosome of hello Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="e398d-138">Opération INSERT parallèle</span><span class="sxs-lookup"><span data-stu-id="e398d-138">Parallel INSERT</span></span>
<span data-ttu-id="e398d-139">L’exécution d’instructions de TSQL hello ci-dessous exécute hello l’opération d’insertion au niveau de compatibilité 120 et 130, qui exécute respectivement hello l’opération d’insertion dans un modèle de thread unique (120) et dans un modèle multithread (130).</span><span class="sxs-lookup"><span data-stu-id="e398d-139">Executing hello TSQL statements below executes hello INSERT operation under compatibility level 120 and 130, which respectively executes hello INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="e398d-140">En demandant le plan de requête réel hello hello, examinez sa représentation sous forme de graphique ou de son contenu XML, vous pouvez déterminer quels Estimation de cardinalité fonction est au cœur.</span><span class="sxs-lookup"><span data-stu-id="e398d-140">By requesting hello actual hello query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="e398d-141">En examinant les plans hello côte à côte sur la figure 1, nous pouvons voir clairement que l’exécution du magasin de colonne INSERT hello s’étende de série dans les 120 tooparallel à 130.</span><span class="sxs-lookup"><span data-stu-id="e398d-141">Looking at hello plans side-by-side on figure 1, we can clearly see that hello Column Store INSERT execution goes from serial in 120 tooparallel in 130.</span></span> <span data-ttu-id="e398d-142">En outre, notez cette modification hello d’icône d’itérateur hello dans hello 130 effectifs deux flèches parallèles, illustrant les faits hello qui maintenant hello exécution de l’itérateur est effectivement parallèle.</span><span class="sxs-lookup"><span data-stu-id="e398d-142">Also, note that hello change of hello iterator icon in hello 130 plan showing two parallel arrows, illustrating hello fact that now hello iterator execution is indeed parallel.</span></span> <span data-ttu-id="e398d-143">Si vous avez grand toocomplete d’opérations INSERT, l’exécution parallèle hello, nombre toohello lié du noyau, que vous avez à votre disposition pour la base de données hello, est plus performantes ; en fonction de votre situation des tooa 100 fois plus rapide !</span><span class="sxs-lookup"><span data-stu-id="e398d-143">If you have large INSERT operations toocomplete, hello parallel execution, linked toohello number of core you have at your disposal for hello database, will perform better; up tooa 100 times faster depending your situation!</span></span>

<span data-ttu-id="e398d-144">*Figure 1 : Insérer des modifications de l’opération à partir de la série tooparallel avec le niveau de compatibilité 130.*</span><span class="sxs-lookup"><span data-stu-id="e398d-144">*Figure 1: INSERT operation changes from serial tooparallel with compatibility level 130.*</span></span>

![La figure 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="e398d-146">Mode Batch SÉRIE</span><span class="sxs-lookup"><span data-stu-id="e398d-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="e398d-147">De même, le déplacement toocompatibility niveau 130 lors du traitement des lignes de données active en mode de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="e398d-147">Similarly, moving toocompatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="e398d-148">Tout d’abord, les opérations en mode batch ne sont disponibles que si vous avez un index columnstore.</span><span class="sxs-lookup"><span data-stu-id="e398d-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="e398d-149">En second lieu, un lot généralement représente environ 900 lignes et utilise une logique de code optimisée pour le processeur multicœur, débit de mémoire et directement tire parti hello données compressées de hello banque des colonnes chaque fois que possible.</span><span class="sxs-lookup"><span data-stu-id="e398d-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages hello compressed data of hello Column Store whenever possible.</span></span> <span data-ttu-id="e398d-150">Dans ces conditions, SQL Server 2016 peut traiter environ 900 lignes à la fois, au lieu de 1 ligne au moment de hello, et par conséquent, hello globalement les frais de fonctionnement de hello sont maintenant partagé par lot entier hello, réduisant hello globale des coûts par ligne.</span><span class="sxs-lookup"><span data-stu-id="e398d-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at hello time, and as a consequence, hello overall overhead cost of hello operation is now shared by hello entire batch, reducing hello overall cost by row.</span></span> <span data-ttu-id="e398d-151">Ce montant partagé d’opérations combinées avec compression de la banque de colonne hello fondamentalement réduit la latence de hello impliquée dans une opération en mode de sélection de lot.</span><span class="sxs-lookup"><span data-stu-id="e398d-151">This shared amount of operations combined with hello column store compression basically reduces hello latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="e398d-152">Vous pouvez trouver plus d’informations sur la banque des colonnes hello et mode de traitement par lots [Guide des index Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="e398d-152">You can find more details about hello column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="e398d-153">Comme visible ci-dessous, en observant hello requête plans côte à côte sur la figure 2, nous pouvons voir que le mode de traitement hello a changé avec le niveau de compatibilité hello, et par conséquent, lors de l’exécution des requêtes hello à la fois au niveau de compatibilité complètement, nous constatons que la plupart du temps de traitement hello est passé en mode batch ligne mode (86 %) comparé toohello (14 %), où 2 lots ont été traités.</span><span class="sxs-lookup"><span data-stu-id="e398d-153">As visible below, by observing hello query plans side-by-side on figure 2, we can see that hello processing mode has changed with hello compatibility level, and as a consequence, when executing hello queries in both compatibility level altogether, we can see that most of hello processing time is spent in row mode (86%) compared toohello batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="e398d-154">Augmenter le jeu de données hello, hello avantage augmente.</span><span class="sxs-lookup"><span data-stu-id="e398d-154">Increase hello dataset, hello benefit will increase.</span></span>

<span data-ttu-id="e398d-155">*Figure 2 : Sélectionner les modifications de l’opération à partir du mode toobatch série avec un niveau de compatibilité 130.*</span><span class="sxs-lookup"><span data-stu-id="e398d-155">*Figure 2: SELECT operation changes from serial toobatch mode with compatibility level 130.*</span></span>

![Figure 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="e398d-157">Opération SORT en mode batch</span><span class="sxs-lookup"><span data-stu-id="e398d-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="e398d-158">Transition de hello similaire toohello ci-dessus, mais l’opération de tri appliquée tooa, à partir de la ligne (niveau de compatibilité 120) toobatch modes (niveau de compatibilité 130) améliore les performances de hello Hello l’opération de tri pour hello mêmes raisons.</span><span class="sxs-lookup"><span data-stu-id="e398d-158">Similar toohello above, but applied tooa sort operation, hello transition from row mode (compatibility level 120) toobatch mode (compatibility level 130) improves hello performance of hello SORT operation for hello same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="e398d-159">Visible côte à côte sur la figure 3, nous pouvons voir que l’opération de tri en mode ligne hello représente 81 % Hello coût, tandis que le mode de traitement par lots hello représente uniquement 19 % du coût hello (respectivement 81 et 56 % lors du tri hello lui-même).</span><span class="sxs-lookup"><span data-stu-id="e398d-159">Visible side-by-side on figure 3, we can see that hello sort operation in row mode represents 81% of hello cost, while hello batch mode only represents 19% of hello cost (respectively 81% and 56% on hello sort itself).</span></span>

<span data-ttu-id="e398d-160">*Figure 3 : L’opération de tri change du mode de toobatch de ligne avec le niveau de compatibilité 130.*</span><span class="sxs-lookup"><span data-stu-id="e398d-160">*Figure 3: SORT operation changes from row toobatch mode with compatibility level 130.*</span></span>

![Figure 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="e398d-162">Évidemment, ces exemples contiennent uniquement des dizaines de milliers de lignes, qui a la valeur nothing lorsque vous examinez les données de salutation disponibles dans la plupart des serveurs SQL ces jours.</span><span class="sxs-lookup"><span data-stu-id="e398d-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at hello data available in most SQL Servers these days.</span></span> <span data-ttu-id="e398d-163">Juste de projet ces par rapport à des millions de lignes à la place, et cela peut se traduire en quelques minutes d’exécution neutralisé chaque jour en attente de la nature de hello de votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="e398d-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending hello nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="e398d-164">Améliorations de l’estimation de la cardinalité</span><span class="sxs-lookup"><span data-stu-id="e398d-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="e398d-165">Introduites avec SQL Server 2014, une base de données en cours d’exécution à un niveau de compatibilité 120 ou ci-dessus permettront à utiliser de nouvelles fonctionnalités de cardinalité hello.</span><span class="sxs-lookup"><span data-stu-id="e398d-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="e398d-166">Estimation de la cardinalité est essentiellement une logique hello utilisé toodetermine comment SQL server exécute une requête en fonction de son coût estimé.</span><span class="sxs-lookup"><span data-stu-id="e398d-166">Essentially, cardinality estimation is hello logic used toodetermine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="e398d-167">estimation de Hello est calculée à l’aide de l’entrée à partir des statistiques associées aux objets impliqués dans cette requête.</span><span class="sxs-lookup"><span data-stu-id="e398d-167">hello estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="e398d-168">En pratique, à un niveau élevé, fonctions d’Estimation de cardinalité sont des estimations de nombre de lignes ainsi que des informations sur la distribution de hello de valeurs hello, les nombres de valeur distincte, et les nombres en double contenues dans hello des tables et des objets référencés dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="e398d-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about hello distribution of hello values, distinct value counts, and duplicate counts contained in hello tables and objects referenced in hello query.</span></span> <span data-ttu-id="e398d-169">Obtention de ces estimations incorrect, peut entraîner des e/s de disque toounnecessary en raison des allocations de mémoire tooinsufficient (autrement dit, les vidages de TempDB), ou tooa la sélection d’une exécution de plan en série via une représentation parallèle de planifier l’exécution, tooname quelques.</span><span class="sxs-lookup"><span data-stu-id="e398d-169">Getting these estimates wrong, can lead toounnecessary disk I/O due tooinsufficient memory grants (i.e. TempDB spills), or tooa selection of a serial plan execution over a parallel plan execution, tooname a few.</span></span> <span data-ttu-id="e398d-170">Conclusion, estimations incorrectes peuvent entraîner des tooan une dégradation des performances globales de l’exécution des requêtes hello.</span><span class="sxs-lookup"><span data-stu-id="e398d-170">Conclusion, incorrect estimates can lead tooan overall performance degradation of hello query execution.</span></span> <span data-ttu-id="e398d-171">Sur hello autre côté, mieux estime, estimation plus précise, les exécutions de la requête toobetter prospects !</span><span class="sxs-lookup"><span data-stu-id="e398d-171">On hello other side, better estimates, more accurate estimates, leads toobetter query executions!</span></span>

<span data-ttu-id="e398d-172">Comme mentionné précédemment, les optimisations de requête et les estimations sont quelque chose de complexe, mais si vous souhaitez toolearn plus d’informations sur les plans de requête et estimateur de cardinalité, vous pouvez faire référence document toohello à [optimiser vos Plans de requête avec hello SQL Server 2014 Estimateur de cardinalité](https://msdn.microsoft.com/library/dn673537.aspx) pour une présentation plus approfondie.</span><span class="sxs-lookup"><span data-stu-id="e398d-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want toolearn more about query plans and cardinality estimator, you can refer toohello document at [Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="e398d-173">Quelle estimation de la cardinalité utilisez-vous actuellement ?</span><span class="sxs-lookup"><span data-stu-id="e398d-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="e398d-174">toodetermine sous les Estimation de cardinalité vos requêtes sont en cours d’exécution, nous allons utiliser simplement la requête de hello exemples ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e398d-174">toodetermine under which Cardinality Estimation your queries are running, let’s just use hello query samples below.</span></span> <span data-ttu-id="e398d-175">Notez que ce premier exemple s’exécute sous le niveau de compatibilité est 110, ce qui implique d’utilisation hello de fonctions d’Estimation de cardinalité ancien hello.</span><span class="sxs-lookup"><span data-stu-id="e398d-175">Note that this first example will run under compatibility level 110, implying hello use of hello old Cardinality Estimation functions.</span></span>

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


<span data-ttu-id="e398d-176">Une fois l’exécution terminée, cliquez sur le lien XML hello et examiner les propriétés de hello du premier itérateur de hello comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e398d-176">Once execution is complete, click on hello XML link, and look at hello properties of hello first iterator as shown below.</span></span> <span data-ttu-id="e398d-177">Notez le nom de la propriété hello appelé CardinalityEstimationModelVersion actuellement définie sur 70.</span><span class="sxs-lookup"><span data-stu-id="e398d-177">Note hello property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="e398d-178">Cela ne signifie pas que le niveau de compatibilité de base de données hello a la valeur version de SQL Server 7.0 toohello (il est défini sur 110 comme visible dans les instructions de TSQL hello ci-dessus), mais la valeur de hello 70 représente simplement la fonctionnalité Estimation de cardinalité hello héritée disponible à partir de SQL Serveur 7.0, qui n’avait aucune révision majeure jusqu'à ce que SQL Server 2014 (qui est fourni avec un niveau de compatibilité 120).</span><span class="sxs-lookup"><span data-stu-id="e398d-178">It does not mean that hello database compatibility level is set toohello SQL Server 7.0 version (it is set on 110 as visible in hello TSQL statements above), but hello value 70 simply represents hello legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="e398d-179">*Figure 4 : hello CardinalityEstimationModelVersion a la valeur too70 lors de l’utilisation d’un niveau de compatibilité de 110 ou inférieur.*</span><span class="sxs-lookup"><span data-stu-id="e398d-179">*Figure 4: hello CardinalityEstimationModelVersion is set too70 when using a compatibility level of 110 or below.*</span></span>

![Figure 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="e398d-181">Ou bien, vous pouvez modifier too130 au niveau de compatibilité hello et désactiver l’utilisation de hello de la fonction d’Estimation de cardinalité nouvelle hello à l’aide de hello LEGACY_CARDINALITY_ESTIMATION définir tooON avec [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="e398d-181">Alternatively, you can change hello compatibility level too130, and disable hello use of hello new Cardinality Estimation function by using hello LEGACY_CARDINALITY_ESTIMATION set tooON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="e398d-182">Cela sera être exactement hello identique à l’aide de 110 à partir d’une Estimation de cardinalité fonction point de vue, lors de l’utilisation du niveau de compatibilité de traitement des requêtes plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="e398d-182">This will be exactly hello same as using 110 from a Cardinality Estimation function point of view, while using hello latest query processing compatibility level.</span></span> <span data-ttu-id="e398d-183">Ce faisant, vous pouvez tirer parti de hello nouvelle requête avec le niveau de compatibilité plus récente hello (c'est-à-dire en mode batch) des fonctionnalités de traitement, mais toujours s’appuient sur les fonctionnalités d’Estimation de cardinalité ancien hello si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e398d-183">Doing so, you can benefit from hello new query processing features coming with hello latest compatibility level (i.e. batch mode), but still rely on hello old Cardinality Estimation functionality if necessary.</span></span>

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


<span data-ttu-id="e398d-184">Déplaçant toohello le niveau de compatibilité 120 ou 130 permet de nouvelles fonctionnalités de cardinalité hello.</span><span class="sxs-lookup"><span data-stu-id="e398d-184">Simply moving toohello compatibility level 120 or 130 enables hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="e398d-185">Dans ce cas, la valeur par défaut de hello CardinalityEstimationModelVersion sera définie en conséquence too120 ou 130 comme visible ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e398d-185">In such a case, hello default CardinalityEstimationModelVersion will be set accordingly too120 or 130 as visible below.</span></span>

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


<span data-ttu-id="e398d-186">*Figure 5 : hello CardinalityEstimationModelVersion a la valeur too130 lors de l’utilisation d’un niveau de compatibilité de 130.*</span><span class="sxs-lookup"><span data-stu-id="e398d-186">*Figure 5: hello CardinalityEstimationModelVersion is set too130 when using a compatibility level of 130.*</span></span>

![Figure 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a><span data-ttu-id="e398d-188">Différences d’Estimation de cardinalité hello de contrôleur</span><span class="sxs-lookup"><span data-stu-id="e398d-188">Witnessing hello Cardinality Estimation differences</span></span>
<span data-ttu-id="e398d-189">Maintenant, nous allons exécuter légèrement plus complexe impliquant une jointure interne avec une clause WHERE avec des prédicats de requête et examinons hello estimation du nombre de lignes à partir de la fonction d’Estimation de cardinalité ancien hello tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="e398d-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at hello row count estimate from hello old Cardinality Estimation function first.</span></span>

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


<span data-ttu-id="e398d-190">L’exécution de cette requête efficacement retourne des lignes de 200,704, alors que l’estimation de ligne hello avec la fonctionnalité d’Estimation de cardinalité ancien hello revendications 194,284 lignes.</span><span class="sxs-lookup"><span data-stu-id="e398d-190">Executing this query effectively returns 200,704 rows, while hello row estimate with hello old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="e398d-191">Évidemment, comme indiqué précédemment, ces résultats de nombre de lignes dépendront également la fréquence à laquelle vous avez exécuté hello précédents exemples, qui remplit les tables d’exemple hello indéfiniment à chaque exécution.</span><span class="sxs-lookup"><span data-stu-id="e398d-191">Obviously, as said before, these row count results will also depend how often you ran hello previous samples, which populates hello sample tables over and over again at each run.</span></span> <span data-ttu-id="e398d-192">Évidemment, les prédicats hello dans votre requête aura également une incidence sur l’estimation de réel hello à part la forme de table hello, le contenu de données et comment ces données réellement mettre en corrélation les uns avec les autres.</span><span class="sxs-lookup"><span data-stu-id="e398d-192">Obviously, hello predicates in your query will also have an influence on hello actual estimation aside from hello table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="e398d-193">*Figure 6 : estimation du nombre de lignes hello est 194,284 ou 6 000 lignes désactivé à partir des lignes de 200,704 hello attendus.*</span><span class="sxs-lookup"><span data-stu-id="e398d-193">*Figure 6: hello row count estimate is 194,284 or 6,000 rows off from hello 200,704 rows expected.*</span></span>

![Figure 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="e398d-195">Bonjour même façon, nous allons à présent exécuter hello même requête avec de nouvelles fonctionnalités de cardinalité hello.</span><span class="sxs-lookup"><span data-stu-id="e398d-195">In hello same way, let’s now execute hello same query with hello new Cardinality Estimation functionality.</span></span>

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


<span data-ttu-id="e398d-196">En examinant hello ci-dessous, vous pouvez désormais voir que cette estimation de la ligne hello est 202,877, ou beaucoup plus proche et supérieure hello Estimation de cardinalité ancien.</span><span class="sxs-lookup"><span data-stu-id="e398d-196">Looking at hello below, we now see that hello row estimate is 202,877, or much closer and higher than hello old Cardinality Estimation.</span></span>

<span data-ttu-id="e398d-197">*Figure 7 : estimation du nombre de lignes hello est désormais 202,877, au lieu de 194,284.*</span><span class="sxs-lookup"><span data-stu-id="e398d-197">*Figure 7: hello row count estimate is now 202,877, instead of 194,284.*</span></span>

![Figure 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="e398d-199">En réalité, le jeu de résultats hello est 200,704 lignes (tout dépend de la fréquence à laquelle vous n’avez exécuté les requêtes hello Hello exemples précédents, mais plus important encore, comme hello TSQL utilise l’instruction de RAND() hello, les valeurs réelles hello retournées peuvent varier à partir d’un toohello exécution suivant).</span><span class="sxs-lookup"><span data-stu-id="e398d-199">In reality, hello result set is 200,704 rows (but all of it depends how often you did run hello queries of hello previous samples, but more importantly, because hello TSQL uses hello RAND() statement, hello actual values returned can vary from one run toohello next).</span></span> <span data-ttu-id="e398d-200">Par conséquent, dans cet exemple particulier, hello nouvelle Estimation de cardinalité est plus efficace au niveau de l’estimation de nombre hello de lignes, car 202,877 est beaucoup plus proches too200, 704, que 194,284 !</span><span class="sxs-lookup"><span data-stu-id="e398d-200">Therefore, in this particular example, hello new Cardinality Estimation does a better job at estimating hello number of rows because 202,877 is much closer too200,704, than 194,284!</span></span> <span data-ttu-id="e398d-201">Enfin, si vous modifiez hello tooequality des prédicats de clause WHERE (au lieu de « > » pour l’instance), cela pourrait rendre encore plus différentes estimations hello entre hello ancienne et nouvelle fonction de cardinalité, en fonction du nombre maximal de correspondances, vous pouvez obtenir.</span><span class="sxs-lookup"><span data-stu-id="e398d-201">Last, if you change hello WHERE clause predicates tooequality (rather than “>” for instance), this could make hello estimates between hello old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="e398d-202">En l’occurrence, une estimation inférieure de 6 000 lignes par rapport au nombre réel ne représente pas une grande quantité de données dans certaines situations.</span><span class="sxs-lookup"><span data-stu-id="e398d-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="e398d-203">Maintenant, transposer cette toomillions de lignes sur plusieurs tables et des requêtes plus complexes, et parfois hello estimation peut être désactivé par des millions de lignes et par conséquent, hello risque de hello de prise en charge incorrect de plan d’exécution, ou que la demande de mémoire insuffisante accorde début les vidages de tooTempDB et donc plus d’e/s, sont beaucoup plus important.</span><span class="sxs-lookup"><span data-stu-id="e398d-203">Now, transpose this toomillions of rows across several tables and more complex queries, and at times hello estimate can be off by millions of rows , and therefore, hello risk of picking-up hello wrong execution plan, or requesting insufficient memory grants leading tooTempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="e398d-204">Si vous avez la possibilité de hello, entraîner cette comparaison avec vos requêtes les plus classiques et les jeux de données et voir par vous-même par la quantité des estimations de hello anciennes et nouvelles sont affectés, tandis que certaines pourraient vient d’être plus hors tension à partir de la réalité de hello, ou certaines autres simplement le nombre de lignes de réel toohello proche réellement retournés dans les jeux de résultats hello.</span><span class="sxs-lookup"><span data-stu-id="e398d-204">If you have hello opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of hello old and new estimates are affected, while some could just become more off from hello reality, or some others just simply closer toohello actual row counts actually returned in hello result sets.</span></span> <span data-ttu-id="e398d-205">Tout dépend de forme hello des requêtes, des caractéristiques de base de données SQL Azure hello, nature de hello et taille hello des jeux de données et des statistiques hello disponibles à leur sujet.</span><span class="sxs-lookup"><span data-stu-id="e398d-205">All of it will depend of hello shape of your queries, hello Azure SQL database characteristics, hello nature and hello size of your datasets, and hello statistics available about them.</span></span> <span data-ttu-id="e398d-206">Si vous venez de créer votre instance de base de données SQL Azure, la requête hello optimiseur aura toobuild ses connaissances de toutes pièces au lieu de la réutilisation des statistiques de requête précédente de hello s’exécute.</span><span class="sxs-lookup"><span data-stu-id="e398d-206">If you just created your Azure SQL Database instance, hello query optimizer will have toobuild its knowledge from scratch instead of reusing statistics made of hello previous query runs.</span></span> <span data-ttu-id="e398d-207">Par conséquent, les estimations de hello sont situation de serveur et d’application tooevery très contextuelles et presque spécifiques.</span><span class="sxs-lookup"><span data-stu-id="e398d-207">So, hello estimates are very contextual and almost specific tooevery server and application situation.</span></span> <span data-ttu-id="e398d-208">Il s’agit d’un tookeep aspect important, n’oubliez pas !</span><span class="sxs-lookup"><span data-stu-id="e398d-208">It is an important aspect tookeep in mind!</span></span>

## <a name="some-considerations-tootake-into-account"></a><span data-ttu-id="e398d-209">Certaines tootake de considérations en compte</span><span class="sxs-lookup"><span data-stu-id="e398d-209">Some considerations tootake into account</span></span>
<span data-ttu-id="e398d-210">Bien que la plupart des charges de travail bénéficierait de niveau de compatibilité 130, hello avant d’adopter le niveau de compatibilité hello pour votre environnement de production, vous avez essentiellement 3 options :</span><span class="sxs-lookup"><span data-stu-id="e398d-210">Although most workloads would benefit from hello compatibility level 130, before you adopting hello compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="e398d-211">Vous déplacez toocompatibility niveau 130 et voir les choses.</span><span class="sxs-lookup"><span data-stu-id="e398d-211">You move toocompatibility level 130, and see how things perform.</span></span> <span data-ttu-id="e398d-212">Si vous remarquez des régressions, vous définissez simplement les tooits arrière au niveau de compatibilité hello niveau d’origine, ou conserver 130 et uniquement inverser le mode hérité hello Estimation de cardinalité précédent toohello (comme expliqué ci-dessus, ce seul pourrait résoudre hello).</span><span class="sxs-lookup"><span data-stu-id="e398d-212">In case you notice some regressions, you just simply set hello compatibility level back tooits original level, or keep 130, and only reverse hello Cardinality Estimation back toohello legacy mode (As explained above, this alone could address hello issue).</span></span>
2. <span data-ttu-id="e398d-213">Vous testez vos applications existantes sous la même charge de production, affiner et validez les performances hello avant le cours tooproduction.</span><span class="sxs-lookup"><span data-stu-id="e398d-213">You thoroughly test your existing applications under similar production load, fine tune, and validate hello performance before going tooproduction.</span></span> <span data-ttu-id="e398d-214">En cas de problèmes, même en tant que ci-dessus, vous pouvez toujours revenir au niveau de compatibilité d’origine toohello, ou simplement inverser en mode hérité hello Estimation de cardinalité précédent toohello.</span><span class="sxs-lookup"><span data-stu-id="e398d-214">In case of issues, same as above, you can always go back toohello original compatibility level, or simply reverse hello Cardinality Estimation back toohello legacy mode.</span></span>
3. <span data-ttu-id="e398d-215">En tant qu’option finale, hello tooaddress de façon plus récent ces questions, est le magasin de requêtes tooleverage hello.</span><span class="sxs-lookup"><span data-stu-id="e398d-215">As a final option, and hello most recent way tooaddress these questions, is tooleverage hello Query Store.</span></span> <span data-ttu-id="e398d-216">Et c’est l’option recommandée aujourd’hui !</span><span class="sxs-lookup"><span data-stu-id="e398d-216">That’s today’s recommended option!</span></span> <span data-ttu-id="e398d-217">analyse de hello tooassist de vos requêtes sous compatibilité niveau 120 ou ci-dessous par rapport à 130, nous ne pouvons pas vous encourageons suffisamment toouse magasin de requêtes.</span><span class="sxs-lookup"><span data-stu-id="e398d-217">tooassist hello analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough toouse Query Store.</span></span> <span data-ttu-id="e398d-218">Magasin de requêtes est disponible avec la version la plus récente de la base de données de SQL Azure V12 hello, et il est conçu toohelp vous requête résolution des problèmes de performances.</span><span class="sxs-lookup"><span data-stu-id="e398d-218">Query Store is available with hello latest version of Azure SQL Database V12, and it’s designed toohelp you with query performance troubleshooting.</span></span> <span data-ttu-id="e398d-219">Considérez hello magasin de requêtes comme une boîte noire de données pour votre base de données collecter et présenter des informations historiques détaillées sur toutes les requêtes.</span><span class="sxs-lookup"><span data-stu-id="e398d-219">Think of hello Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="e398d-220">Cela considérablement simplifie l’analyse des performances en réduisant hello temps toodiagnose et résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="e398d-220">This greatly simplifies performance forensics by reducing hello time toodiagnose and resolve issues.</span></span> <span data-ttu-id="e398d-221">Pour en savoir plus, consultez [Magasin des requêtes : un enregistreur de données pour votre base de données](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span><span class="sxs-lookup"><span data-stu-id="e398d-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="e398d-222">À hello de haut niveau, si vous disposez d’un ensemble de bases de données en cours d’exécution au niveau de compatibilité 120 ou en dessous et planifiez toomove certains d'entre eux too130, ou parce que votre charge de travail configurer automatiquement les nouvelles bases de données qui seront bientôt être définis par défaut too130, pensez à qui suit de Hello :</span><span class="sxs-lookup"><span data-stu-id="e398d-222">At hello high-level, if you already have a set of databases running at compatibility level 120 or below, and plan toomove some of them too130, or because your workload automatically provision new databases that will be soon be set by default too130, please consider hello followings:</span></span>

* <span data-ttu-id="e398d-223">Avant de modifier le niveau de compatibilité de toohello en production, activer le magasin de requêtes.</span><span class="sxs-lookup"><span data-stu-id="e398d-223">Before changing toohello new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="e398d-224">Vous pouvez faire référence trop[modifier le magasin de requêtes hello en Mode de compatibilité de base de données et l’utilisation des hello](https://msdn.microsoft.com/library/bb895281.aspx) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="e398d-224">You can refer too[Change hello Database Compatibility Mode and Use hello Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="e398d-225">Ensuite, testez les charges de travail critiques à l’aide de requêtes d’un environnement de production et comparer les performances hello a rencontré et comme signalé par le magasin de requêtes et données représentatif.</span><span class="sxs-lookup"><span data-stu-id="e398d-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare hello performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="e398d-226">Si vous rencontrez des régressions, vous pouvez identifier hello régression des requêtes avec hello magasin de requêtes et utiliser l’option à partir du magasin de requêtes de forçage de plan de hello (également appelé plan épinglage).</span><span class="sxs-lookup"><span data-stu-id="e398d-226">If you experience some regressions, you can identify hello regressed queries with hello Query Store and use hello plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="e398d-227">Dans ce cas, vous définitivement Restez avec le niveau de compatibilité hello 130 et utilisez le plan de requête précédent hello comme suggéré par hello magasin de requêtes.</span><span class="sxs-lookup"><span data-stu-id="e398d-227">In such a case, you definitively stay with hello compatibility level 130, and use hello former query plan as suggested by hello Query Store.</span></span>
* <span data-ttu-id="e398d-228">Si vous souhaitez tooleverage nouvelles fonctionnalités et fonctions de base de données SQL Azure (qui est en cours d’exécution SQL Server 2016), mais sont sensibles toochanges par niveau de compatibilité 130, hello en dernier recours, vous pouvez envisager de forcer le niveau de compatibilité hello précédent niveau toohello adapté à votre charge de travail à l’aide d’une instruction ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="e398d-228">If you want tooleverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive toochanges brought by hello compatibility level 130, as a last resort, you could consider forcing hello compatibility level back toohello level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="e398d-229">Mais tout d’abord, gardez à l’esprit ce plan de requête magasin hello épinglage option est la meilleure option car vous n’utilisez ne pas 130 restent essentiellement au niveau de fonctionnalité hello une ancienne version de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e398d-229">But first, be aware that hello Query Store plan pinning option is your best option because not using 130 is basically staying at hello functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="e398d-230">Si vous avez des applications mutualisées couvrant plusieurs bases de données, il peut être hello tooupdate nécessaires configuration logique de vos bases de données de tooensure un niveau de compatibilité de cohérence sur toutes les bases de données ; ceux ancien et qui vient d’être mis en service.</span><span class="sxs-lookup"><span data-stu-id="e398d-230">If you have multitenant applications spanning multiple databases, it may be necessary tooupdate hello provisioning logic of your databases tooensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="e398d-231">Performances de charge de travail de votre application peut être fait de toohello sensibles que certaines bases de données sont exécutent à des niveaux de compatibilité, et par conséquent, la cohérence au niveau de compatibilité entre les bases de données peut être requise tooprovide hello même ordre expérience tooyour clients tout tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="e398d-231">Your application workload performance could be sensitive toohello fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order tooprovide hello same experience tooyour customers all across hello board.</span></span> <span data-ttu-id="e398d-232">Notez qu’il n’est pas, cela dépend bien sûr comment votre application est affectée par le niveau de compatibilité hello.</span><span class="sxs-lookup"><span data-stu-id="e398d-232">Note that it is not a mandate, it really depends on how your application is affected by hello compatibility level.</span></span>
* <span data-ttu-id="e398d-233">Enfin, concernant l’Estimation de la cardinalité de hello et tout comme la modification du niveau de compatibilité hello, avant de continuer en production, il est recommandé de votre charge de travail de production sous hello nouvelles conditions toodetermine tootest si votre application tire parti de améliorations d’Estimation de cardinalité Hello.</span><span class="sxs-lookup"><span data-stu-id="e398d-233">Last, regarding hello Cardinality Estimation, and just like changing hello compatibility level, before proceeding in production, it is recommended tootest your production workload under hello new conditions toodetermine if your application benefits from hello Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="e398d-234">Conclusion</span><span class="sxs-lookup"><span data-stu-id="e398d-234">Conclusion</span></span>
<span data-ttu-id="e398d-235">À l’aide de la base de données SQL Azure toobenefit à partir de toutes les améliorations de SQL Server 2016 peut améliorer nettement les exécutions de la requête.</span><span class="sxs-lookup"><span data-stu-id="e398d-235">Using Azure SQL Database toobenefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="e398d-236">C’est vrai !</span><span class="sxs-lookup"><span data-stu-id="e398d-236">Just as-is!</span></span> <span data-ttu-id="e398d-237">Bien entendu, comme toute nouvelle fonctionnalité, une évaluation appropriée doit être effectuée les conditions exactes hello toodetermine sous lequel votre charge de travail de base de données opère hello mieux.</span><span class="sxs-lookup"><span data-stu-id="e398d-237">Of course, like any new feature, a proper evaluation must be done toodetermine hello exact conditions under which your database workload operates hello best.</span></span> <span data-ttu-id="e398d-238">L’expérience montre que la plupart des charges de travail sont attendu tooat moins exécuté de façon transparente au niveau de compatibilité 130, tout en tirant parti des nouvelles fonctions et la nouvelle Estimation de cardinalité de traitement des requêtes.</span><span class="sxs-lookup"><span data-stu-id="e398d-238">Experience shows that most workload are expected tooat least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="e398d-239">C'est-à-dire Ceci dit, dans la pratique, il existe toujours des exceptions et procéder à une échéance appropriée diligence un toodetermine évaluation important combien vous pouvez bénéficier de ces améliorations.</span><span class="sxs-lookup"><span data-stu-id="e398d-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment toodetermine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="e398d-240">Et là encore, le magasin de requêtes hello peut être une aide précieuse dans ce travail !</span><span class="sxs-lookup"><span data-stu-id="e398d-240">And again, hello Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="e398d-241">Évolution de SQL Azure, vous pouvez espérer un niveau de compatibilité 140 Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="e398d-241">As SQL Azure evolves, you can expect a compatibility level 140 in hello future.</span></span> <span data-ttu-id="e398d-242">Le temps venu, nous discuterons des apports de ce niveau de compatibilité 140, comme nous venons d’expliquer brièvement les avantages du niveau 130 aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="e398d-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="e398d-243">Pour l’instant, nous allons n'oubliez pas, à partir de juin 2016, base de données SQL Azure ne pourra le niveau de compatibilité par défaut hello too130 120 pour les bases de données nouvellement créées.</span><span class="sxs-lookup"><span data-stu-id="e398d-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change hello default compatibility level from 120 too130 for newly created databases.</span></span> <span data-ttu-id="e398d-244">Prenez date !</span><span class="sxs-lookup"><span data-stu-id="e398d-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="e398d-245">Références</span><span class="sxs-lookup"><span data-stu-id="e398d-245">References</span></span>
* [<span data-ttu-id="e398d-246">Nouveautés (moteur de base de données)</span><span class="sxs-lookup"><span data-stu-id="e398d-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="e398d-247">Blog : Le magasin des requêtes : un enregistreur de données pour votre base de données par Borko Novakovic, 8 juin 2016</span><span class="sxs-lookup"><span data-stu-id="e398d-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="e398d-248">Niveau de compatibilité ALTER TABLE (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="e398d-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="e398d-249">ALTER DATABASE SCOPED CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="e398d-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="e398d-250">Niveau de compatibilité 130 pour Azure SQL Database V12</span><span class="sxs-lookup"><span data-stu-id="e398d-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="e398d-251">Optimisation de votre requête de Plans par hello estimateur de cardinalité SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="e398d-251">Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="e398d-252">Description des index columnstore</span><span class="sxs-lookup"><span data-stu-id="e398d-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="e398d-253">Blog : Amélioration des performances des requêtes avec le niveau de compatibilité 130 dans Azure SQL Database, par Alain Lissoir, 6 mai 2016</span><span class="sxs-lookup"><span data-stu-id="e398d-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

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
