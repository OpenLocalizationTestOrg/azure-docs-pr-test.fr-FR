---
title: tables aaaDistributing SQL Data Warehouse | Documents Microsoft
description: Prise en main de la distribution de tables dans Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="4e4ea-103">Distribution de tables dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4e4ea-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="4e4ea-104">[Vue d’ensemble][Overview]</span><span class="sxs-lookup"><span data-stu-id="4e4ea-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="4e4ea-105">[Types de données][Data Types]</span><span class="sxs-lookup"><span data-stu-id="4e4ea-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="4e4ea-106">[Distribuer][Distribute]</span><span class="sxs-lookup"><span data-stu-id="4e4ea-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="4e4ea-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="4e4ea-107">[Index][Index]</span></span>
> * <span data-ttu-id="4e4ea-108">[Partition][Partition]</span><span class="sxs-lookup"><span data-stu-id="4e4ea-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="4e4ea-109">[Statistiques][Statistics]</span><span class="sxs-lookup"><span data-stu-id="4e4ea-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="4e4ea-110">[Temporaire][Temporary]</span><span class="sxs-lookup"><span data-stu-id="4e4ea-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="4e4ea-111">SQL Data Warehouse est un système de base de données distribuée à traitement massivement parallèle.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="4e4ea-112">En répartissant les données et les fonctions de traitement sur plusieurs nœuds, SQL Data Warehouse propose une évolutivité immense, bien supérieure à ce qu’offre n’importe quel système unique.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="4e4ea-113">Décider comment toodistribute vos données dans votre entrepôt de données SQL sont une des plus importantes de hello facteurs tooachieving des performances optimales.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-113">Deciding how toodistribute your data within your SQL Data Warehouse is one of hello most important factors tooachieving optimal performance.</span></span>   <span data-ttu-id="4e4ea-114">performances de clé toooptimal Hello est de minimiser le déplacement des données et à son tour le déplacement des données de hello toominimizing clé consiste à sélectionner la stratégie de distribution droite hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-114">hello key toooptimal performance is minimizing data movement and in turn hello key toominimizing data movement is selecting hello right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="4e4ea-115">Présentation du déplacement des données</span><span class="sxs-lookup"><span data-stu-id="4e4ea-115">Understanding data movement</span></span>
<span data-ttu-id="4e4ea-116">Dans un système MPP, données hello de chaque table sont réparties sur plusieurs bases de données sous-jacentes.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-116">In an MPP system, hello data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="4e4ea-117">requêtes Hello plus optimisée sur un système MPP peuvent simplement être transmises via tooexecute hello des bases de données distribuées sans aucune interaction hello entre les autres bases de données.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-117">hello most optimized queries on an MPP system can simply be passed through tooexecute on hello individual distributed databases with no interaction between hello other databases.</span></span>  <span data-ttu-id="4e4ea-118">Par exemple, supposons que vous disposez d’une base de données avec des données de ventes, qui contient deux tables, ventes et clients.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="4e4ea-119">Si vous disposez d’une requête qui doit toojoin votre table des clients de la table sales tooyour et que vous divisez une vos ventes et les tables du client par numéro de client, le placement de chaque client dans une base de données distincte, toutes les requêtes qui relient les ventes et les clients peuvent être résolus dans chaque Aucune base de connaissances de base de données hello autres bases de données.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-119">If you have a query that needs toojoin your sales table tooyour customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of hello other databases.</span></span>  <span data-ttu-id="4e4ea-120">En revanche, si vos données de ventes que vous divisé par numéro de commande et les données de votre client par numéro de client, puis chaque base de données n’a pas les données correspondantes hello pour chaque client et par conséquent, si vous souhaitiez toojoin vos données de client tooyour les données de ventes, vous devez tooget hello de données pour chaque client à partir de hello autres bases de données.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have hello corresponding data for each customer and thus if you wanted toojoin your sales data tooyour customer data, you would need tooget hello data for each customer from hello other databases.</span></span>  <span data-ttu-id="4e4ea-121">Dans ce deuxième exemple, le déplacement des données besoin toooccur toomove hello les données toohello données de ventes, afin que hello deux tables peuvent être jointes.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-121">In this second example, data movement would need toooccur toomove hello customer data toohello sales data, so that hello two tables can be joined.</span></span>  

<span data-ttu-id="4e4ea-122">Le déplacement des données n’est pas toujours une mauvaise chose, il est parfois nécessaire toosolve une requête.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-122">Data movement isn't always a bad thing, sometimes it's necessary toosolve a query.</span></span>  <span data-ttu-id="4e4ea-123">Mais quand cette étape supplémentaire peut être évitée, votre requête s’exécute naturellement plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="4e4ea-124">Le déplacement des données se produit généralement en cas de jointure ou d’agrégation de tables.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="4e4ea-125">Fréquence à laquelle vous devez toodo à la fois, tandis que vous pourrez toooptimize pour un scénario comme une jointure, vous toujours besoin toohelp de déplacement des données vous résolvez hello autre scénario, comme une agrégation.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-125">Often you need toodo both, so while you may be able toooptimize for one scenario, like a join, you still need data movement toohelp you solve for hello other scenario, like an aggregation.</span></span>  <span data-ttu-id="4e4ea-126">Astuce de Hello est de savoir qui est moins de travail.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-126">hello trick is figuring out which is less work.</span></span>  <span data-ttu-id="4e4ea-127">Dans la plupart des cas, la distribution de grandes tables de faits sur une colonne jointe communément est hello méthode la plus efficace pour réduire hello la plupart des mouvements de données.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-127">In most cases, distributing large fact tables on a commonly joined column is hello most effective method for reducing hello most data movement.</span></span>  <span data-ttu-id="4e4ea-128">Distribution des données sur les colonnes de jointure est un beaucoup plus courantes méthode tooreduce le déplacement des données à la distribution des données sur des colonnes impliquées dans une agrégation.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-128">Distributing data on join columns is a much more common method tooreduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="4e4ea-129">Sélectionner la méthode de distribution</span><span class="sxs-lookup"><span data-stu-id="4e4ea-129">Select distribution method</span></span>
<span data-ttu-id="4e4ea-130">Coulisses de hello, SQL Data Warehouse divise vos données dans les bases de données de 60.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-130">Behind hello scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="4e4ea-131">Chaque base de données est référencé tooas un **distribution**.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-131">Each individual database is referred tooas a **distribution**.</span></span>  <span data-ttu-id="4e4ea-132">Lorsque les données sont chargées dans chaque table, l’entrepôt de données SQL a tooknow comment toodivide vos données sur ces 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-132">When data is loaded into each table, SQL Data Warehouse has tooknow how toodivide your data across these 60 distributions.</span></span>  

<span data-ttu-id="4e4ea-133">méthode de distribution Hello est définie au niveau de table hello et actuellement, il existe deux possibilités :</span><span class="sxs-lookup"><span data-stu-id="4e4ea-133">hello distribution method is defined at hello table level and currently there are two choices:</span></span>

1. <span data-ttu-id="4e4ea-134">**Tourniquet (round robin)** , qui distribue les données de manière équitable mais aléatoire.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="4e4ea-135">**distribution par hachage** , qui distribue les données en fonction des valeurs de hachage d’une colonne unique.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="4e4ea-136">Par défaut, lorsque vous ne définissez pas une méthode de distribution de données, votre table sera distribuée à l’aide de hello **tourniquet (Round Robin)** méthode de distribution.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-136">By default, when you do not define a data distribution method, your table will be distributed using hello **round robin** distribution method.</span></span>  <span data-ttu-id="4e4ea-137">Toutefois, lorsque vous serez plus sophistiquées dans votre implémentation, vous pouvez à l’aide de tooconsider **hachage distribué** toominimize le déplacement des données qui vous permettra d’optimiser les performances des requêtes à son tour les tables.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-137">However, as you become more sophisticated in your implementation, you will want tooconsider using **hash distributed** tables toominimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="4e4ea-138">Tables avec distribution par tourniquet (round robin)</span><span class="sxs-lookup"><span data-stu-id="4e4ea-138">Round Robin Tables</span></span>
<span data-ttu-id="4e4ea-139">À l’aide de la méthode tourniquet (Round Robin) pour distribuer des données de hello est très bien comment il semble.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-139">Using hello Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="4e4ea-140">Lors du chargement de vos données, chaque ligne est envoyée simplement toohello prochaine distribution.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-140">As your data is loaded, each row is simply sent toohello next distribution.</span></span>  <span data-ttu-id="4e4ea-141">Cette méthode pour distribuer les données de salutation toujours répartira les données de salutation très uniformément sur toutes les distributions de hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-141">This method of distributing hello data will always randomly distribute hello data very evenly across all of hello distributions.</span></span>  <span data-ttu-id="4e4ea-142">Autrement dit, il n’est aucun tri terminé pendant hello round (Round Robin) les processus qui le place vos données.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-142">That is, there is no sorting done during hello round robin process which places your data.</span></span>  <span data-ttu-id="4e4ea-143">C’est pour cette raison que ce type de distribution est parfois appelé « hachage aléatoire ».</span><span class="sxs-lookup"><span data-stu-id="4e4ea-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="4e4ea-144">Avec une table distribuée alternée aucune donnée nécessaire toounderstand hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-144">With a round-robin distributed table there is no need toounderstand hello data.</span></span>  <span data-ttu-id="4e4ea-145">Pour cette raison, ce type de table représente souvent une cible de chargement adéquate.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="4e4ea-146">Par défaut, si aucune méthode de distribution n’est choisie, hello méthode de distribution alternée servira.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-146">By default, if no distribution method is chosen, hello round robin distribution method will be used.</span></span>  <span data-ttu-id="4e4ea-147">Toutefois, alors que les tables de tourniquet (Round Robin) sont toouse facile, car les données sont réparties au hasard sur système hello que cela signifie que le système de hello ne peut pas garantir la distribution chaque ligne est sur.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-147">However, while round robin tables are easy toouse, because data is randomly distributed across hello system it means that hello system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="4e4ea-148">En conséquence, système hello parfois des besoins tooinvoke un toobetter d’opération de déplacement des données organiser vos données avant qu’il peut résoudre une requête.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-148">As a result, hello system sometimes needs tooinvoke a data movement operation toobetter organize your data before it can resolve a query.</span></span>  <span data-ttu-id="4e4ea-149">Cette étape supplémentaire peut ralentir vos requêtes.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="4e4ea-150">Envisagez d’utiliser la distribution de tourniquet (Round Robin) pour votre table Bonjour les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="4e4ea-150">Consider using Round Robin distribution for your table in hello following scenarios:</span></span>

* <span data-ttu-id="4e4ea-151">lors de la mise en route sous forme de point de départ simple ;</span><span class="sxs-lookup"><span data-stu-id="4e4ea-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="4e4ea-152">s’il n’existe aucune clé de jointure évidente ;</span><span class="sxs-lookup"><span data-stu-id="4e4ea-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="4e4ea-153">S’il n’est pas colonne bon candidat pour la distribution de table de hello de hachage</span><span class="sxs-lookup"><span data-stu-id="4e4ea-153">If there is not good candidate column for hash distributing hello table</span></span>
* <span data-ttu-id="4e4ea-154">Si hello table ne partage pas d’une clé de jointure commune avec d’autres tables</span><span class="sxs-lookup"><span data-stu-id="4e4ea-154">If hello table does not share a common join key with other tables</span></span>
* <span data-ttu-id="4e4ea-155">Si la jointure de hello est moins importante que les autres jointures dans la requête de hello</span><span class="sxs-lookup"><span data-stu-id="4e4ea-155">If hello join is less significant than other joins in hello query</span></span>
* <span data-ttu-id="4e4ea-156">Lorsque hello est une table intermédiaire temporaire</span><span class="sxs-lookup"><span data-stu-id="4e4ea-156">When hello table is a temporary staging table</span></span>

<span data-ttu-id="4e4ea-157">Ces exemples créent une table à distribution par tourniquet (round robin) :</span><span class="sxs-lookup"><span data-stu-id="4e4ea-157">Both of these examples will create a Round Robin Table:</span></span>

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> <span data-ttu-id="4e4ea-158">Alors que le tourniquet (Round Robin) est le type de table par défaut hello soient explicites dans votre commande DDL est considéré comme une meilleure pratique afin que les intentions hello de votre disposition de table soient tooothers clair.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-158">While round robin is hello default table type being explicit in your DDL is considered a best practice so that hello intentions of your table layout are clear tooothers.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="4e4ea-159">Tables à distribution par hachage</span><span class="sxs-lookup"><span data-stu-id="4e4ea-159">Hash Distributed Tables</span></span>
<span data-ttu-id="4e4ea-160">À l’aide un **hachage distribué** algorithme toodistribute vos tables peuvent améliorer les performances dans de nombreux scénarios en réduisant le déplacement des données au moment de la requête.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-160">Using a **Hash distributed** algorithm toodistribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="4e4ea-161">Hachage distribuées sont des tables qui sont répartis entre hello distribuées de bases de données à l’aide d’un algorithme de hachage sur une seule colonne que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-161">Hash distributed tables are tables which are divided between hello distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="4e4ea-162">colonne de distribution Hello est ce qui détermine la façon dont les données de salutation sont réparties sur vos bases de données distribuées.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-162">hello distribution column is what determines how hello data is divided across your distributed databases.</span></span>  <span data-ttu-id="4e4ea-163">fonction de hachage Hello utilise hello distribution colonne tooassign lignes toodistributions.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-163">hello hash function uses hello distribution column tooassign rows toodistributions.</span></span>  <span data-ttu-id="4e4ea-164">Hello d’algorithme de hachage et de distribution qui en résulte est déterministe.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-164">hello hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="4e4ea-165">Autrement dit hello même valeur avec le même type de données sera toujours de hello a toohello distribution même.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-165">That is hello same value with hello same data type will always has toohello same distribution.</span></span>    

<span data-ttu-id="4e4ea-166">Cet exemple crée une table distribuée en fonction de l’ID :</span><span class="sxs-lookup"><span data-stu-id="4e4ea-166">This example will create a table distributed on id:</span></span>

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
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
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a><span data-ttu-id="4e4ea-167">Sélectionner la colonne de distribution</span><span class="sxs-lookup"><span data-stu-id="4e4ea-167">Select distribution column</span></span>
<span data-ttu-id="4e4ea-168">Lorsque vous choisissez trop**hachage distribuer** une table, vous devez tooselect une colonne de distribution unique.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-168">When you choose too**hash distribute** a table, you will need tooselect a single distribution column.</span></span>  <span data-ttu-id="4e4ea-169">Lorsque vous sélectionnez une colonne de distribution, il existe trois principaux facteurs tooconsider.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-169">When selecting a distribution column, there are three major factors tooconsider.</span></span>  

<span data-ttu-id="4e4ea-170">Sélectionnez une colonne unique qui :</span><span class="sxs-lookup"><span data-stu-id="4e4ea-170">Select a single column which will:</span></span>

1. <span data-ttu-id="4e4ea-171">ne sera pas mise à jour ;</span><span class="sxs-lookup"><span data-stu-id="4e4ea-171">Not be updated</span></span>
2. <span data-ttu-id="4e4ea-172">distribuera les données de manière uniforme en évitant le décalage des données ;</span><span class="sxs-lookup"><span data-stu-id="4e4ea-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="4e4ea-173">réduira le nombre de déplacements des données.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="4e4ea-174">Sélectionner la colonne de distribution qui ne sera pas mise à jour</span><span class="sxs-lookup"><span data-stu-id="4e4ea-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="4e4ea-175">Les colonnes de distribution ne peuvent pas être mises à jour, par conséquent, sélectionnez une colonne avec des valeurs statiques.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="4e4ea-176">Si une colonne a besoin toobe mis à jour, il n’est généralement pas un candidat de distribution correct.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-176">If a column will need toobe updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="4e4ea-177">S’il existe un cas où vous devez mettre à jour une colonne de distribution, il est possible par tout d’abord supprimer les lignes hello, puis d’insérer une nouvelle ligne.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-177">If there is a case where you must update a distribution column, this can be done by first deleting hello row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="4e4ea-178">Sélectionner la colonne de distribution qui distribuera les données de manière uniforme</span><span class="sxs-lookup"><span data-stu-id="4e4ea-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="4e4ea-179">Depuis un système distribué effectue aussi vite que sa distribution les plus lents, il est important toodivide hello travail uniformément entre les distributions de hello dans l’exécution de commande tooachieve équilibrée dans tout hello système.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-179">Since a distributed system performs only as fast as its slowest distribution, it is important toodivide hello work evenly across hello distributions in order tooachieve balanced execution across hello system.</span></span>  <span data-ttu-id="4e4ea-180">moyen Hello travail de hello est divisée en un système distribué est basée sur l’emplacement réel des données hello pour chaque point de distribution.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-180">hello way hello work is divided on a distributed system is based on where hello data for each distribution lives.</span></span>  <span data-ttu-id="4e4ea-181">Cela permet de colonne de droite distribution hello tooselect très important pour la distribution des données de salutation afin que chaque point de distribution a le même travail, et sera take hello même temps toocomplete sa partie du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-181">This makes it very important tooselect hello right distribution column for distributing hello data so that each distribution has equal work and will take hello same time toocomplete its portion of hello work.</span></span>  <span data-ttu-id="4e4ea-182">Lorsque le travail est bien réparti sur système de hello, les données de salutation sont équilibrées entre les distributions de hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-182">When work is well divided across hello system, hello data is balanced across hello distributions.</span></span>  <span data-ttu-id="4e4ea-183">Lorsque les données ne sont pas équilibrées, c’est ce que nous appelons le **décalage des données**.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="4e4ea-184">les données toodivide uniformément et éviter que les données de décalage, envisagez de suivant de hello lors de la sélection de votre colonne de distribution :</span><span class="sxs-lookup"><span data-stu-id="4e4ea-184">toodivide data evenly and avoid data skew, consider hello following when selecting your distribution column:</span></span>

1. <span data-ttu-id="4e4ea-185">Sélectionnez une colonne contenant un nombre important de valeurs distinctes.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="4e4ea-186">Évitez la distribution des données sur des colonnes avec peu de valeurs distinctes.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="4e4ea-187">Évitez de distribuer les données sur des colonnes dont la fréquence de valeurs NULL est élevée.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="4e4ea-188">Évitez de distribuer les données sur des colonnes de date.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="4e4ea-189">Étant donné que chaque valeur est haché too1 60 distributions, répartition tooachieve vous devez tooselect une colonne qui est hautement unique et contient plus de 60 valeurs uniques.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-189">Since each value is hashed too1 of 60 distributions, tooachieve even distribution you will want tooselect a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="4e4ea-190">tooillustrate, considérez un cas où une colonne contient seulement des valeurs uniques 40.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-190">tooillustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="4e4ea-191">Si cette colonne a été sélectionnée en tant que clé de répartition hello, données hello pour cette table seraient arriver sur 40 distributions au maximum, en laissant les 20 distributions avec aucune donnée et aucun toodo de traitement.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-191">If this column was selected as hello distribution key, hello data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing toodo.</span></span>  <span data-ttu-id="4e4ea-192">À l’inverse, hello autres 40 distributions aurait plus toodo de travail que si hello données a été réparties de façon plus de 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-192">Conversely, hello other 40 distributions would have more work toodo that if hello data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="4e4ea-193">Ce scénario est un exemple de décalage de données.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="4e4ea-194">Dans le système MPP, chaque étape de requête attend que toutes les distributions toocomplete leur part les travaux hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-194">In MPP system, each query step waits for all distributions toocomplete their share of hello work.</span></span>  <span data-ttu-id="4e4ea-195">Si une distribution est effectuant plus de travail pour d’autres hello : hello ressource Hello autres distributions sont essentiellement un inutile simplement en attente de distribution à l’activité hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-195">If one distribution is doing more work than hello others, then hello resource of hello other distributions are essentially wasted just waiting on hello busy distribution.</span></span>  <span data-ttu-id="4e4ea-196">Lorsque le travail n’est pas réparti uniformément sur toutes les distributions, c’est ce que nous appelons le **décalage de traitement**.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="4e4ea-197">Traitement inclinaison entraîne toorun requêtes plus lente que si la charge de travail hello peut être répartie uniformément entre les distributions de hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-197">Processing skew will cause queries toorun slower than if hello workload can be evenly spread across hello distributions.</span></span>  <span data-ttu-id="4e4ea-198">Décalage de données entraînent tooprocessing inclinaison.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-198">Data skew will lead tooprocessing skew.</span></span>

<span data-ttu-id="4e4ea-199">Éviter la distribution sur hautement n’acceptant que les valeurs null hello tous arrive ensuite sur hello même distribution.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-199">Avoid distributing on highly nullable column as hello null values will all land on hello same distribution.</span></span> <span data-ttu-id="4e4ea-200">Distribution sur une colonne de date peut également provoquer le décalage de traitement, car toutes les données d’une date donnée arrive ensuite sur hello même distribution.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-200">Distributing on a date column can also cause processing skew because all data for a given date will land on hello same distribution.</span></span> <span data-ttu-id="4e4ea-201">Si plusieurs utilisateurs exécutent des requêtes tout filtrage sur hello même date, puis uniquement 1 de distributions de 60 hello va faire tout travail de hello depuis une date donnée seront uniquement sur une distribution.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-201">If several users are executing queries all filtering on hello same date, then only 1 of hello 60 distributions will be doing all of hello work since a given date will only be on one distribution.</span></span> <span data-ttu-id="4e4ea-202">Dans ce scénario, les requêtes de hello s’exécuteront probablement de 60 fois plus lents que si les données de salutation ont été également réparties sur toutes les distributions de hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-202">In this scenario, hello queries will likely run 60 times slower than if hello data were equally spread over all of hello distributions.</span></span>

<span data-ttu-id="4e4ea-203">Lorsque aucune colonne bon candidat n’existe, envisagez d’utiliser le tourniquet (Round Robin) comme méthode de distribution hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-203">When no good candidate columns exist, then consider using round robin as hello distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="4e4ea-204">Sélectionner la colonne de distribution qui réduira le déplacement des données</span><span class="sxs-lookup"><span data-stu-id="4e4ea-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="4e4ea-205">En réduisant le déplacement des données en sélectionnant la colonne de droite distribution hello est une des stratégies plus importantes de hello pour optimiser les performances de votre entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-205">Minimizing data movement by selecting hello right distribution column is one of hello most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="4e4ea-206">Le déplacement des données se produit généralement en cas de jointure ou d’agrégation de tables.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="4e4ea-207">Les colonnes utilisées dans les clauses `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` et `HAVING` sont toutes **adéquates** pour une distribution par hachage.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="4e4ea-208">Hello de d’autre part, les colonnes de hello `WHERE` clause **pas** d’apporter les candidats de colonne hachage adéquate, car ils limitent les distributions participent requête hello, à l’origine de traitement inclinaison.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-208">On hello other hand, columns in hello `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in hello query, causing processing skew.</span></span>  <span data-ttu-id="4e4ea-209">Un bon exemple d’une colonne qui peut être tentant de toodistribute sur, mais souvent risque de ce traitement inclinaison est une colonne de date.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-209">A good example of a column which might be tempting toodistribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="4e4ea-210">En règle générale, si vous avez deux tables de faits volumineuse souvent impliquées dans une jointure, vous bénéficierez hello la plupart des performances en distribuant les deux tables sur l’une des colonnes de jointure hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain hello most performance by distributing both tables on one of hello join columns.</span></span>  <span data-ttu-id="4e4ea-211">Si vous avez une table qui n’est jamais tooanother jointes grande table de faits, puis recherchez toocolumns sont souvent Bonjour `GROUP BY` clause.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-211">If you have a table that is never joined tooanother large fact table, then look toocolumns that are frequently in hello `GROUP BY` clause.</span></span>

<span data-ttu-id="4e4ea-212">Il existe quelques critères clés qui doivent être rempli tooavoid déplacement des données au cours d’une jointure :</span><span class="sxs-lookup"><span data-stu-id="4e4ea-212">There are a few key criteria which must be met tooavoid data movement during a join:</span></span>

1. <span data-ttu-id="4e4ea-213">Hello tables impliquées dans la jointure de hello doivent être distribué sur hachage **un** de colonnes hello participant à la jointure de hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-213">hello tables involved in hello join must be hash distributed on **one** of hello columns participating in hello join.</span></span>
2. <span data-ttu-id="4e4ea-214">types de données Hello hello de colonnes de jointure doivent correspondre entre les deux tables.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-214">hello data types of hello join columns must match between both tables.</span></span>
3. <span data-ttu-id="4e4ea-215">les colonnes Hello doivent être joint avec un opérateur d’égalité.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-215">hello columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="4e4ea-216">Hello type de jointure est peut-être pas un `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-216">hello join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="4e4ea-217">Résolution des problèmes de décalage de données</span><span class="sxs-lookup"><span data-stu-id="4e4ea-217">Troubleshooting data skew</span></span>
<span data-ttu-id="4e4ea-218">Lorsque les données de la table sont distribuées à l’aide de la méthode de distribution de hachage hello est possible que certaines distributions sera rétrécie toohave disproportionnellement davantage de données que d’autres.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-218">When table data is distributed using hello hash distribution method there is a chance that some distributions will be skewed toohave disproportionately more data than others.</span></span> <span data-ttu-id="4e4ea-219">Décalage trop de données peut affecter les performances de requête, car le résultat final de hello d’une requête distribuée doit attendre toofinish de distribution en cours d’exécution plus longue hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-219">Excessive data skew can impact query performance because hello final result of a distributed query must wait for hello longest running distribution toofinish.</span></span> <span data-ttu-id="4e4ea-220">En fonction du degré de hello de données hello inclinaison, que vous devrez peut-être tooaddress il.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-220">Depending on hello degree of hello data skew you might need tooaddress it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="4e4ea-221">Identification du décalage</span><span class="sxs-lookup"><span data-stu-id="4e4ea-221">Identifying skew</span></span>
<span data-ttu-id="4e4ea-222">Un moyen simple de tooidentify une table comme rétrécie est toouse `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-222">A simple way tooidentify a table as skewed is toouse `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="4e4ea-223">Il s’agit d’un moyen très simple et rapide de toosee hello du nombre de lignes de table qui sont stockées dans chacun des distributions hello 60 de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-223">This is a very quick and simple way toosee hello number of table rows that are stored in each of hello 60 distributions of your database.</span></span>  <span data-ttu-id="4e4ea-224">N’oubliez pas que pour des performances hello plus équilibrée, lignes hello dans votre table distribuée doivent être répartis uniformément sur toutes les distributions de hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-224">Remember that for hello most balanced performance, hello rows in your distributed table should be spread evenly across all hello distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="4e4ea-225">Toutefois, si vous interrogez les vues de gestion dynamique hello Azure SQL Data Warehouse (DMV), vous pouvez effectuer une analyse plus détaillée.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-225">However, if you query hello Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="4e4ea-226">toostart, créer hello vue [dbo.vTableSizes] [ dbo.vTableSizes] afficher à l’aide de SQL à partir de hello [vue d’ensemble de la Table] [ Overview] article.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-226">toostart, create hello view [dbo.vTableSizes][dbo.vTableSizes] view using hello SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="4e4ea-227">Une fois que la vue de hello est créée, exécutez cette tooidentify requête les tables d’avoir plus de 10 % de données inclinaison.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-227">Once hello view is created, run this query tooidentify which tables have more than 10% data skew.</span></span>

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a><span data-ttu-id="4e4ea-228">Résolution du décalage des données</span><span class="sxs-lookup"><span data-stu-id="4e4ea-228">Resolving data skew</span></span>
<span data-ttu-id="4e4ea-229">Pas tout décalage est suffisamment toowarrant.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-229">Not all skew is enough toowarrant a fix.</span></span>  <span data-ttu-id="4e4ea-230">Dans certains cas, les performances hello d’une table dans des requêtes peut annuler tout effet nuisible hello de décalage des données.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-230">In some cases, hello performance of a table in some queries can outweigh hello harm of data skew.</span></span>  <span data-ttu-id="4e4ea-231">l’inclinaison toodecide si vous devez résoudre des données dans une table, vous devez comprendre autant que possible sur les volumes de données hello et requêtes dans votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-231">toodecide if you should resolve data skew in a table, you should understand as much as possible about hello data volumes and queries in your workload.</span></span>   <span data-ttu-id="4e4ea-232">Toolook unidirectionnel à l’impact de hello d’inclinaison est toouse les étapes de hello Bonjour [requête analyse] [ Query Monitoring] impact de hello toomonitor d’inclinaison sur les performances des requêtes de l’article et hello plus précisément les requêtes longues de toohow impact Prenez toocomplete sur les distributions individuelles hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-232">One way toolook at hello impact of skew is toouse hello steps in hello [Query Monitoring][Query Monitoring] article toomonitor hello impact of skew on query performance and specifically hello impact toohow long queries take toocomplete on hello individual distributions.</span></span>

<span data-ttu-id="4e4ea-233">Distribution des données consiste à recherche hello juste équilibre entre en réduisant le décalage des données et en réduisant le déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-233">Distributing data is a matter of finding hello right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="4e4ea-234">Ceux-ci peuvent être opposées objectifs, et vous pouvez tookeep données dans le déplacement des données de commande tooreduce.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-234">These can be opposing goals, and sometimes you will want tookeep data skew in order tooreduce data movement.</span></span> <span data-ttu-id="4e4ea-235">Par exemple, lors de la colonne de distribution hello est fréquemment hello partagé colonne dans les jointures et agrégations, vous serez minimiser le déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-235">For example, when hello distribution column is frequently hello shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="4e4ea-236">Hello avantage de disposer de déplacement de données minimale hello peut-être dépasser impact hello d’avoir des données d’inclinaison.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-236">hello benefit of having hello minimal data movement might outweigh hello impact of having data skew.</span></span>

<span data-ttu-id="4e4ea-237">décalage de données tooresolve est toore typique Hello-créer de table de hello avec une colonne de distribution différent.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-237">hello typical way tooresolve data skew is toore-create hello table with a different distribution column.</span></span> <span data-ttu-id="4e4ea-238">Comme il n’existe aucun moyen de colonne de distribution toochange hello sur un tableau, distribution de hello toochange hello moyen d’une table il toorecreate avec un [] [SACT].</span><span class="sxs-lookup"><span data-stu-id="4e4ea-238">Since there is no way toochange hello distribution column on an existing table, hello way toochange hello distribution of a table it toorecreate it with a [CTAS][].</span></span>  <span data-ttu-id="4e4ea-239">Voici deux exemples illustrant comment résoudre le décalage de données :</span><span class="sxs-lookup"><span data-stu-id="4e4ea-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a><span data-ttu-id="4e4ea-240">Exemple 1 : Recréez la table hello avec une nouvelle colonne de distribution</span><span class="sxs-lookup"><span data-stu-id="4e4ea-240">Example 1: Re-create hello table with a new distribution column</span></span>
<span data-ttu-id="4e4ea-241">Cet exemple utilise [SACT] [] toore-créer une table avec une colonne de distribution de hachage différent.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-241">This example uses [CTAS][] toore-create a table with a different hash distribution column.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a><span data-ttu-id="4e4ea-242">Exemple 2 : Recréez la table hello à l’aide de la distribution de tourniquet (Round Robin)</span><span class="sxs-lookup"><span data-stu-id="4e4ea-242">Example 2: Re-create hello table using round robin distribution</span></span>
<span data-ttu-id="4e4ea-243">Cet exemple utilise [SACT] [] toore-créer une table avec tourniquet au lieu d’une distribution de hachage.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-243">This example uses [CTAS][] toore-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="4e4ea-244">Cette modification produira une distribution des données de même coût de hello du déplacement des données accrue.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-244">This change will produce even data distribution at hello cost of increased data movement.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="4e4ea-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e4ea-245">Next steps</span></span>
<span data-ttu-id="4e4ea-246">toolearn en savoir plus sur la création de table, consultez hello [distribuer][Distribute], [Index][Index], [Partition] [ Partition], [Des Types de données][Data Types], [statistiques] [ Statistics] et [des Tables temporaires] [ Temporary] articles.</span><span class="sxs-lookup"><span data-stu-id="4e4ea-246">toolearn more about table design, see hello [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="4e4ea-247">Pour obtenir une vue d’ensemble des bonnes pratiques, consultez [Bonnes pratiques pour Azure SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="4e4ea-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
