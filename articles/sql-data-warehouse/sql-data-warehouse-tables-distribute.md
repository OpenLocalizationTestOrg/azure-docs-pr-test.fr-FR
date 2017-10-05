---
title: Distribution de tables dans SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: d0e12bf821a81826a20b8db84e76c48fa60ad9b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="3f738-103">Distribution de tables dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3f738-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="3f738-104">[Vue d’ensemble][Overview]</span><span class="sxs-lookup"><span data-stu-id="3f738-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="3f738-105">[Types de données][Data Types]</span><span class="sxs-lookup"><span data-stu-id="3f738-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="3f738-106">[Distribuer][Distribute]</span><span class="sxs-lookup"><span data-stu-id="3f738-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="3f738-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="3f738-107">[Index][Index]</span></span>
> * <span data-ttu-id="3f738-108">[Partition][Partition]</span><span class="sxs-lookup"><span data-stu-id="3f738-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="3f738-109">[Statistiques][Statistics]</span><span class="sxs-lookup"><span data-stu-id="3f738-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="3f738-110">[Temporaire][Temporary]</span><span class="sxs-lookup"><span data-stu-id="3f738-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="3f738-111">SQL Data Warehouse est un système de base de données distribuée à traitement massivement parallèle.</span><span class="sxs-lookup"><span data-stu-id="3f738-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="3f738-112">En répartissant les données et les fonctions de traitement sur plusieurs nœuds, SQL Data Warehouse propose une évolutivité immense, bien supérieure à ce qu’offre n’importe quel système unique.</span><span class="sxs-lookup"><span data-stu-id="3f738-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="3f738-113">Le fait de décider comment distribuer vos données dans votre SQL Data Warehouse est un des facteurs les plus importants pour obtenir des performances optimales.</span><span class="sxs-lookup"><span data-stu-id="3f738-113">Deciding how to distribute your data within your SQL Data Warehouse is one of the most important factors to achieving optimal performance.</span></span>   <span data-ttu-id="3f738-114">L’élément clé permettant d’optimiser les performances est de réduire le déplacement des données et celui permettant de réduire le déplacement des données est de sélectionner la stratégie de distribution appropriée.</span><span class="sxs-lookup"><span data-stu-id="3f738-114">The key to optimal performance is minimizing data movement and in turn the key to minimizing data movement is selecting the right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="3f738-115">Présentation du déplacement des données</span><span class="sxs-lookup"><span data-stu-id="3f738-115">Understanding data movement</span></span>
<span data-ttu-id="3f738-116">Dans un système MPP, les données de chaque table sont réparties dans plusieurs bases de données sous-jacentes.</span><span class="sxs-lookup"><span data-stu-id="3f738-116">In an MPP system, the data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="3f738-117">Les requêtes les plus optimisées sur un système MPP peuvent simplement être passées pour s’exécuter sur les différentes bases de données distribuées sans aucune interaction entre les autres bases de données.</span><span class="sxs-lookup"><span data-stu-id="3f738-117">The most optimized queries on an MPP system can simply be passed through to execute on the individual distributed databases with no interaction between the other databases.</span></span>  <span data-ttu-id="3f738-118">Par exemple, supposons que vous disposez d’une base de données avec des données de ventes, qui contient deux tables, ventes et clients.</span><span class="sxs-lookup"><span data-stu-id="3f738-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="3f738-119">Si vous avez une requête qui doit joindre votre table de ventes à votre table de clients, et que vous divisez ces deux tables par numéro de client, en plaçant chaque client dans une base de données distincte, toutes les requêtes qui joignent des ventes à des clients peuvent être résolues dans chaque base de données sans connaissance des autres bases de données.</span><span class="sxs-lookup"><span data-stu-id="3f738-119">If you have a query that needs to join your sales table to your customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of the other databases.</span></span>  <span data-ttu-id="3f738-120">En revanche, si vous avez divisé vos données de vente par numéro de commande et vos données de clients par numéro de client, les bases de données ne disposeront pas des données correspondantes pour chaque client. Ainsi, si vous souhaitez joindre vos données de ventes à vos données de clients, vous devez obtenir les données relatives à chaque client à partir des autres bases de données.</span><span class="sxs-lookup"><span data-stu-id="3f738-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have the corresponding data for each customer and thus if you wanted to join your sales data to your customer data, you would need to get the data for each customer from the other databases.</span></span>  <span data-ttu-id="3f738-121">Dans ce second exemple, un déplacement des données devra se produire pour déplacer les données des clients vers les données de ventes, afin que les deux tables puissent être jointes.</span><span class="sxs-lookup"><span data-stu-id="3f738-121">In this second example, data movement would need to occur to move the customer data to the sales data, so that the two tables can be joined.</span></span>  

<span data-ttu-id="3f738-122">Le déplacement des données n’est pas toujours une mauvaise chose. Il est parfois nécessaire pour résoudre une requête.</span><span class="sxs-lookup"><span data-stu-id="3f738-122">Data movement isn't always a bad thing, sometimes it's necessary to solve a query.</span></span>  <span data-ttu-id="3f738-123">Mais quand cette étape supplémentaire peut être évitée, votre requête s’exécute naturellement plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="3f738-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="3f738-124">Le déplacement des données se produit généralement en cas de jointure ou d’agrégation de tables.</span><span class="sxs-lookup"><span data-stu-id="3f738-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="3f738-125">Il arrive souvent que vous deviez effectuer ces deux opérations à la fois. Ainsi, même si vous pouvez optimiser pour un scénario (par exemple une jointure), vous devrez quand même déplacer des données pour vous aider à remplir les conditions de l’autre scénario (par exemple une agrégation).</span><span class="sxs-lookup"><span data-stu-id="3f738-125">Often you need to do both, so while you may be able to optimize for one scenario, like a join, you still need data movement to help you solve for the other scenario, like an aggregation.</span></span>  <span data-ttu-id="3f738-126">L’astuce est de déterminer ce qui nécessite le moins de travail.</span><span class="sxs-lookup"><span data-stu-id="3f738-126">The trick is figuring out which is less work.</span></span>  <span data-ttu-id="3f738-127">Dans la plupart des cas, la distribution de grandes tables de faits sur une colonne de jointure commune est la méthode la plus efficace pour réduire le déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="3f738-127">In most cases, distributing large fact tables on a commonly joined column is the most effective method for reducing the most data movement.</span></span>  <span data-ttu-id="3f738-128">La distribution de données sur des colonnes de jointure est une méthode de réduction du déplacement des données beaucoup plus courante que la distribution de données sur des colonnes impliquées dans une agrégation.</span><span class="sxs-lookup"><span data-stu-id="3f738-128">Distributing data on join columns is a much more common method to reduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="3f738-129">Sélectionner la méthode de distribution</span><span class="sxs-lookup"><span data-stu-id="3f738-129">Select distribution method</span></span>
<span data-ttu-id="3f738-130">En arrière-plan, SQL Data Warehouse divise vos données en 60 bases de données.</span><span class="sxs-lookup"><span data-stu-id="3f738-130">Behind the scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="3f738-131">Chaque base de données est considérée comme une **distribution**.</span><span class="sxs-lookup"><span data-stu-id="3f738-131">Each individual database is referred to as a **distribution**.</span></span>  <span data-ttu-id="3f738-132">Lorsque les données sont chargées dans chaque table, SQL Data Warehouse doit savoir comment répartir vos données parmi ces 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="3f738-132">When data is loaded into each table, SQL Data Warehouse has to know how to divide your data across these 60 distributions.</span></span>  

<span data-ttu-id="3f738-133">La méthode de distribution est définie au niveau de la table et actuellement, il existe deux possibilités :</span><span class="sxs-lookup"><span data-stu-id="3f738-133">The distribution method is defined at the table level and currently there are two choices:</span></span>

1. <span data-ttu-id="3f738-134">**Tourniquet (round robin)** , qui distribue les données de manière équitable mais aléatoire.</span><span class="sxs-lookup"><span data-stu-id="3f738-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="3f738-135">**distribution par hachage** , qui distribue les données en fonction des valeurs de hachage d’une colonne unique.</span><span class="sxs-lookup"><span data-stu-id="3f738-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="3f738-136">Par défaut, quand vous ne définissez pas de méthode de distribution de données, votre table est distribuée à l’aide de la méthode de distribution du **tourniquet (round robin)** .</span><span class="sxs-lookup"><span data-stu-id="3f738-136">By default, when you do not define a data distribution method, your table will be distributed using the **round robin** distribution method.</span></span>  <span data-ttu-id="3f738-137">Toutefois, à mesure que vous affinez votre implémentation, vous voudrez peut-être utiliser des tables à **distribution par hachage** afin de réduire le déplacement des données, ce qui optimise les performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="3f738-137">However, as you become more sophisticated in your implementation, you will want to consider using **hash distributed** tables to minimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="3f738-138">Tables avec distribution par tourniquet (round robin)</span><span class="sxs-lookup"><span data-stu-id="3f738-138">Round Robin Tables</span></span>
<span data-ttu-id="3f738-139">L’utilisation de la méthode du tourniquet (round Robin) pour la distribution des données fonctionne comme suit :</span><span class="sxs-lookup"><span data-stu-id="3f738-139">Using the Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="3f738-140">Lors du chargement de vos données, chaque ligne est simplement envoyée à la distribution suivante.</span><span class="sxs-lookup"><span data-stu-id="3f738-140">As your data is loaded, each row is simply sent to the next distribution.</span></span>  <span data-ttu-id="3f738-141">Cette méthode distribue toujours aléatoirement les données de manière très uniforme sur toutes les distributions.</span><span class="sxs-lookup"><span data-stu-id="3f738-141">This method of distributing the data will always randomly distribute the data very evenly across all of the distributions.</span></span>  <span data-ttu-id="3f738-142">Autrement dit, aucun tri n’est effectué pendant le processus de tourniquet (round robin) qui place vos données.</span><span class="sxs-lookup"><span data-stu-id="3f738-142">That is, there is no sorting done during the round robin process which places your data.</span></span>  <span data-ttu-id="3f738-143">C’est pour cette raison que ce type de distribution est parfois appelé « hachage aléatoire ».</span><span class="sxs-lookup"><span data-stu-id="3f738-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="3f738-144">Dans le cas d’une table avec distribution par tourniquet (round robin), il n’est pas nécessaire de comprendre la nature des données.</span><span class="sxs-lookup"><span data-stu-id="3f738-144">With a round-robin distributed table there is no need to understand the data.</span></span>  <span data-ttu-id="3f738-145">Pour cette raison, ce type de table représente souvent une cible de chargement adéquate.</span><span class="sxs-lookup"><span data-stu-id="3f738-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="3f738-146">Par défaut, si aucune méthode de distribution n’est choisie, la méthode de distribution par tourniquet (round robin) sera utilisée.</span><span class="sxs-lookup"><span data-stu-id="3f738-146">By default, if no distribution method is chosen, the round robin distribution method will be used.</span></span>  <span data-ttu-id="3f738-147">Toutefois, alors que les tables avec distribution par tourniquet (round robin) sont faciles à utiliser, dans la mesure où les données sont distribuées de manière aléatoire sur le système, cela signifie que le système ne peut pas garantir sur quelle distribution se trouve chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="3f738-147">However, while round robin tables are easy to use, because data is randomly distributed across the system it means that the system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="3f738-148">Par conséquent, le système doit parfois appeler une opération de déplacement des données pour mieux organiser vos données avant de pouvoir résoudre une requête.</span><span class="sxs-lookup"><span data-stu-id="3f738-148">As a result, the system sometimes needs to invoke a data movement operation to better organize your data before it can resolve a query.</span></span>  <span data-ttu-id="3f738-149">Cette étape supplémentaire peut ralentir vos requêtes.</span><span class="sxs-lookup"><span data-stu-id="3f738-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="3f738-150">Vous pouvez envisager une distribution par tourniquet (round robin) des données de votre table dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="3f738-150">Consider using Round Robin distribution for your table in the following scenarios:</span></span>

* <span data-ttu-id="3f738-151">lors de la mise en route sous forme de point de départ simple ;</span><span class="sxs-lookup"><span data-stu-id="3f738-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="3f738-152">s’il n’existe aucune clé de jointure évidente ;</span><span class="sxs-lookup"><span data-stu-id="3f738-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="3f738-153">s’il n’existe aucune colonne adaptée à la distribution par hachage de la table ;</span><span class="sxs-lookup"><span data-stu-id="3f738-153">If there is not good candidate column for hash distributing the table</span></span>
* <span data-ttu-id="3f738-154">si la table ne partage aucune clé de jointure avec d’autres tables ;</span><span class="sxs-lookup"><span data-stu-id="3f738-154">If the table does not share a common join key with other tables</span></span>
* <span data-ttu-id="3f738-155">si la jointure est moins importante que d’autres dans la requête ;</span><span class="sxs-lookup"><span data-stu-id="3f738-155">If the join is less significant than other joins in the query</span></span>
* <span data-ttu-id="3f738-156">lorsque la table est une table temporaire intermédiaire ;</span><span class="sxs-lookup"><span data-stu-id="3f738-156">When the table is a temporary staging table</span></span>

<span data-ttu-id="3f738-157">Ces exemples créent une table à distribution par tourniquet (round robin) :</span><span class="sxs-lookup"><span data-stu-id="3f738-157">Both of these examples will create a Round Robin Table:</span></span>

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
> <span data-ttu-id="3f738-158">Bien que le tourniquet (round robin) soit le type de table par défaut, le fait qu’il soit explicite dans votre DDL est considéré comme étant une bonne pratique afin que les intentions de disposition de votre table soient claires pour les autres.</span><span class="sxs-lookup"><span data-stu-id="3f738-158">While round robin is the default table type being explicit in your DDL is considered a best practice so that the intentions of your table layout are clear to others.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="3f738-159">Tables à distribution par hachage</span><span class="sxs-lookup"><span data-stu-id="3f738-159">Hash Distributed Tables</span></span>
<span data-ttu-id="3f738-160">Le fait d’utiliser un algorithme de **distribution par hachage** pour distribuer vos tables peut améliorer les performances pour de nombreux scénarios en réduisant le déplacement des données au moment de la requête.</span><span class="sxs-lookup"><span data-stu-id="3f738-160">Using a **Hash distributed** algorithm to distribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="3f738-161">Ces tables sont réparties entre les bases de données distribuées à l’aide d’un algorithme de hachage portant sur une colonne unique que vous avez sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="3f738-161">Hash distributed tables are tables which are divided between the distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="3f738-162">La colonne de distribution détermine comment les données sont réparties sur vos bases de données distribuées.</span><span class="sxs-lookup"><span data-stu-id="3f738-162">The distribution column is what determines how the data is divided across your distributed databases.</span></span>  <span data-ttu-id="3f738-163">La fonction de hachage utilise la colonne de distribution pour affecter des lignes aux distributions.</span><span class="sxs-lookup"><span data-stu-id="3f738-163">The hash function uses the distribution column to assign rows to distributions.</span></span>  <span data-ttu-id="3f738-164">L’algorithme de hachage et la distribution qui en résulte sont déterministes.</span><span class="sxs-lookup"><span data-stu-id="3f738-164">The hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="3f738-165">Autrement dit, la même valeur avec le même type de données aura toujours la même distribution.</span><span class="sxs-lookup"><span data-stu-id="3f738-165">That is the same value with the same data type will always has to the same distribution.</span></span>    

<span data-ttu-id="3f738-166">Cet exemple crée une table distribuée en fonction de l’ID :</span><span class="sxs-lookup"><span data-stu-id="3f738-166">This example will create a table distributed on id:</span></span>

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

## <a name="select-distribution-column"></a><span data-ttu-id="3f738-167">Sélectionner la colonne de distribution</span><span class="sxs-lookup"><span data-stu-id="3f738-167">Select distribution column</span></span>
<span data-ttu-id="3f738-168">Quand vous choisissez de **distribuer une table par hachage** , vous devez sélectionner une seule colonne de distribution.</span><span class="sxs-lookup"><span data-stu-id="3f738-168">When you choose to **hash distribute** a table, you will need to select a single distribution column.</span></span>  <span data-ttu-id="3f738-169">Lorsque vous sélectionnez une colonne de distribution, vous devez prendre en compte trois facteurs essentiels.</span><span class="sxs-lookup"><span data-stu-id="3f738-169">When selecting a distribution column, there are three major factors to consider.</span></span>  

<span data-ttu-id="3f738-170">Sélectionnez une colonne unique qui :</span><span class="sxs-lookup"><span data-stu-id="3f738-170">Select a single column which will:</span></span>

1. <span data-ttu-id="3f738-171">ne sera pas mise à jour ;</span><span class="sxs-lookup"><span data-stu-id="3f738-171">Not be updated</span></span>
2. <span data-ttu-id="3f738-172">distribuera les données de manière uniforme en évitant le décalage des données ;</span><span class="sxs-lookup"><span data-stu-id="3f738-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="3f738-173">réduira le nombre de déplacements des données.</span><span class="sxs-lookup"><span data-stu-id="3f738-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="3f738-174">Sélectionner la colonne de distribution qui ne sera pas mise à jour</span><span class="sxs-lookup"><span data-stu-id="3f738-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="3f738-175">Les colonnes de distribution ne peuvent pas être mises à jour, par conséquent, sélectionnez une colonne avec des valeurs statiques.</span><span class="sxs-lookup"><span data-stu-id="3f738-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="3f738-176">Si une colonne doit être mise à jour, celle-ci n’est généralement pas une bonne candidate pour la distribution.</span><span class="sxs-lookup"><span data-stu-id="3f738-176">If a column will need to be updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="3f738-177">Si vous devez mettre à jour une colonne de distribution, il est possible d’effectuer cette opération en commençant par la suppression de la ligne et l’insertion d’une nouvelle.</span><span class="sxs-lookup"><span data-stu-id="3f738-177">If there is a case where you must update a distribution column, this can be done by first deleting the row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="3f738-178">Sélectionner la colonne de distribution qui distribuera les données de manière uniforme</span><span class="sxs-lookup"><span data-stu-id="3f738-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="3f738-179">Dans la mesure où un système distribué s’exécute à la vitesse de sa distribution la plus lente, il est important de travailler uniformément sur les distributions afin d’équilibrer l’exécution sur le système.</span><span class="sxs-lookup"><span data-stu-id="3f738-179">Since a distributed system performs only as fast as its slowest distribution, it is important to divide the work evenly across the distributions in order to achieve balanced execution across the system.</span></span>  <span data-ttu-id="3f738-180">La manière dont le travail est réparti sur le système distribué repose sur l’endroit où résident les données de chaque distribution.</span><span class="sxs-lookup"><span data-stu-id="3f738-180">The way the work is divided on a distributed system is based on where the data for each distribution lives.</span></span>  <span data-ttu-id="3f738-181">Il est donc très important de sélectionner la colonne de distribution de droite pour la distribution des données afin que chaque point de distribution ait la même quantité de travail et qu’il mette le même temps pour effectuer cette dernière.</span><span class="sxs-lookup"><span data-stu-id="3f738-181">This makes it very important to select the right distribution column for distributing the data so that each distribution has equal work and will take the same time to complete its portion of the work.</span></span>  <span data-ttu-id="3f738-182">Lorsque le travail est réparti sur le système, les données sont équilibrées entre les distributions.</span><span class="sxs-lookup"><span data-stu-id="3f738-182">When work is well divided across the system, the data is balanced across the distributions.</span></span>  <span data-ttu-id="3f738-183">Lorsque les données ne sont pas équilibrées, c’est ce que nous appelons le **décalage des données**.</span><span class="sxs-lookup"><span data-stu-id="3f738-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="3f738-184">Pour procéder à une répartition uniforme et éviter le décalage des données, tenez compte des éléments suivants lors de la sélection de votre colonne de distribution :</span><span class="sxs-lookup"><span data-stu-id="3f738-184">To divide data evenly and avoid data skew, consider the following when selecting your distribution column:</span></span>

1. <span data-ttu-id="3f738-185">Sélectionnez une colonne contenant un nombre important de valeurs distinctes.</span><span class="sxs-lookup"><span data-stu-id="3f738-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="3f738-186">Évitez la distribution des données sur des colonnes avec peu de valeurs distinctes.</span><span class="sxs-lookup"><span data-stu-id="3f738-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="3f738-187">Évitez de distribuer les données sur des colonnes dont la fréquence de valeurs NULL est élevée.</span><span class="sxs-lookup"><span data-stu-id="3f738-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="3f738-188">Évitez de distribuer les données sur des colonnes de date.</span><span class="sxs-lookup"><span data-stu-id="3f738-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="3f738-189">Étant donné que chaque valeur est hachée sur 1 à 60 distributions, vous devez sélectionner une colonne particulièrement unique contenant plus de 60 valeurs uniques pour obtenir une distribution uniforme.</span><span class="sxs-lookup"><span data-stu-id="3f738-189">Since each value is hashed to 1 of 60 distributions, to achieve even distribution you will want to select a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="3f738-190">Pour illustrer cela, prenons un cas où une colonne contient seulement 40 valeurs uniques.</span><span class="sxs-lookup"><span data-stu-id="3f738-190">To illustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="3f738-191">Si cette colonne a été sélectionnée en tant que clé de répartition, les données de cette table seraient réparties sur 40 distributions au plus, avec 20 distributions sans aucune donnée et aucun traitement à effectuer.</span><span class="sxs-lookup"><span data-stu-id="3f738-191">If this column was selected as the distribution key, the data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing to do.</span></span>  <span data-ttu-id="3f738-192">À l’inverse, les 40 autres distributions auraient plus de travail à effectuer si les données étaient réparties de manière uniforme sur plus de 60 distributions.</span><span class="sxs-lookup"><span data-stu-id="3f738-192">Conversely, the other 40 distributions would have more work to do that if the data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="3f738-193">Ce scénario est un exemple de décalage de données.</span><span class="sxs-lookup"><span data-stu-id="3f738-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="3f738-194">Dans un système MPP, chaque étape de requête attend que toutes les distributions terminent leur part du travail.</span><span class="sxs-lookup"><span data-stu-id="3f738-194">In MPP system, each query step waits for all distributions to complete their share of the work.</span></span>  <span data-ttu-id="3f738-195">Si une distribution effectue plus de travail que les autres, les ressources des autres distributions sont gaspillées à attendre la distribution occupée.</span><span class="sxs-lookup"><span data-stu-id="3f738-195">If one distribution is doing more work than the others, then the resource of the other distributions are essentially wasted just waiting on the busy distribution.</span></span>  <span data-ttu-id="3f738-196">Lorsque le travail n’est pas réparti uniformément sur toutes les distributions, c’est ce que nous appelons le **décalage de traitement**.</span><span class="sxs-lookup"><span data-stu-id="3f738-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="3f738-197">Le décalage de traitement entraîne une exécution plus lente des requêtes par rapport à une répartition uniforme de la charge de travail sur les distributions.</span><span class="sxs-lookup"><span data-stu-id="3f738-197">Processing skew will cause queries to run slower than if the workload can be evenly spread across the distributions.</span></span>  <span data-ttu-id="3f738-198">Un décalage de données entraîne un décalage de traitement.</span><span class="sxs-lookup"><span data-stu-id="3f738-198">Data skew will lead to processing skew.</span></span>

<span data-ttu-id="3f738-199">Évitez une distribution sur des colonnes contenant de nombreuses valeurs Null, car elles sont placées sur la même distribution.</span><span class="sxs-lookup"><span data-stu-id="3f738-199">Avoid distributing on highly nullable column as the null values will all land on the same distribution.</span></span> <span data-ttu-id="3f738-200">La distribution sur une colonne de date peut également entraîner un décalage de traitement, car toutes les données d’une date donnée sont placées sur la même distribution.</span><span class="sxs-lookup"><span data-stu-id="3f738-200">Distributing on a date column can also cause processing skew because all data for a given date will land on the same distribution.</span></span> <span data-ttu-id="3f738-201">Si plusieurs utilisateurs exécutent des requêtes toutes filtrées à la même date, seule 1 des 60 distributions réalise tout le travail, car une date donnée ne se trouvera que sur une seule distribution.</span><span class="sxs-lookup"><span data-stu-id="3f738-201">If several users are executing queries all filtering on the same date, then only 1 of the 60 distributions will be doing all of the work since a given date will only be on one distribution.</span></span> <span data-ttu-id="3f738-202">Dans ce scénario, les requêtes s’exécuteront probablement 60 fois plus lentement que si les données avaient été réparties équitablement sur toutes les distributions.</span><span class="sxs-lookup"><span data-stu-id="3f738-202">In this scenario, the queries will likely run 60 times slower than if the data were equally spread over all of the distributions.</span></span>

<span data-ttu-id="3f738-203">Lorsqu’il n’existe aucune colonne appropriée, envisagez d’utiliser la méthode de distribution du tourniquet (round robin).</span><span class="sxs-lookup"><span data-stu-id="3f738-203">When no good candidate columns exist, then consider using round robin as the distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="3f738-204">Sélectionner la colonne de distribution qui réduira le déplacement des données</span><span class="sxs-lookup"><span data-stu-id="3f738-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="3f738-205">La réduction du déplacement des données par la sélection de la colonne de distribution adaptée est une des stratégies les plus importantes pour optimiser les performances de votre SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3f738-205">Minimizing data movement by selecting the right distribution column is one of the most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="3f738-206">Le déplacement des données se produit généralement en cas de jointure ou d’agrégation de tables.</span><span class="sxs-lookup"><span data-stu-id="3f738-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="3f738-207">Les colonnes utilisées dans les clauses `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` et `HAVING` sont toutes **adéquates** pour une distribution par hachage.</span><span class="sxs-lookup"><span data-stu-id="3f738-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="3f738-208">En revanche, les colonnes de la clause `WHERE` ne sont **pas** adéquates pour une distribution par hachage, car elles limitent les distributions pouvant participer à la requête, ce qui entraîne un décalage de traitement.</span><span class="sxs-lookup"><span data-stu-id="3f738-208">On the other hand, columns in the `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in the query, causing processing skew.</span></span>  <span data-ttu-id="3f738-209">Une colonne de date est un bon exemple d’une colonne pouvant être utilisée pour la distribution, mais qui peut entraîner ce décalage de traitement.</span><span class="sxs-lookup"><span data-stu-id="3f738-209">A good example of a column which might be tempting to distribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="3f738-210">En règle générale, si deux grandes tables de faits sont souvent impliquées dans une jointure, la distribution des deux tables sur l’une des colonnes de jointure permet d’obtenir les meilleures performances.</span><span class="sxs-lookup"><span data-stu-id="3f738-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain the most performance by distributing both tables on one of the join columns.</span></span>  <span data-ttu-id="3f738-211">Si vous disposez d’une table qui n’est jamais jointe à une autre grande table de faits, examinez les colonnes se trouvant fréquemment dans la clause `GROUP BY` .</span><span class="sxs-lookup"><span data-stu-id="3f738-211">If you have a table that is never joined to another large fact table, then look to columns that are frequently in the `GROUP BY` clause.</span></span>

<span data-ttu-id="3f738-212">Quelques critères clés doivent être remplis pour éviter le déplacement des données lors d’une jointure :</span><span class="sxs-lookup"><span data-stu-id="3f738-212">There are a few key criteria which must be met to avoid data movement during a join:</span></span>

1. <span data-ttu-id="3f738-213">Les tables impliquées dans la jointure doivent être distribuées par hachage sur **l’une** des colonnes participant à la jointure.</span><span class="sxs-lookup"><span data-stu-id="3f738-213">The tables involved in the join must be hash distributed on **one** of the columns participating in the join.</span></span>
2. <span data-ttu-id="3f738-214">Les types de données des colonnes de jointure doivent être identiques dans les deux tables.</span><span class="sxs-lookup"><span data-stu-id="3f738-214">The data types of the join columns must match between both tables.</span></span>
3. <span data-ttu-id="3f738-215">Les colonnes doivent être jointes avec un opérateur d’égalité.</span><span class="sxs-lookup"><span data-stu-id="3f738-215">The columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="3f738-216">Le type de jointure ne peut pas être `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="3f738-216">The join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="3f738-217">Résolution des problèmes de décalage de données</span><span class="sxs-lookup"><span data-stu-id="3f738-217">Troubleshooting data skew</span></span>
<span data-ttu-id="3f738-218">Quand les données de la table sont distribuées à l’aide de la méthode de distribution par hachage, il est probable que certaines distributions seront décalées pour avoir proportionnellement plus de données que d’autres.</span><span class="sxs-lookup"><span data-stu-id="3f738-218">When table data is distributed using the hash distribution method there is a chance that some distributions will be skewed to have disproportionately more data than others.</span></span> <span data-ttu-id="3f738-219">Un décalage excessif des données peut avoir un impact sur les performances des requêtes, car le résultat final d’une requête distribuée doit attendre la fin de la distribution dont l’exécution est la plus longue.</span><span class="sxs-lookup"><span data-stu-id="3f738-219">Excessive data skew can impact query performance because the final result of a distributed query must wait for the longest running distribution to finish.</span></span> <span data-ttu-id="3f738-220">En fonction du degré de décalage des données, vous devrez peut-être le résoudre.</span><span class="sxs-lookup"><span data-stu-id="3f738-220">Depending on the degree of the data skew you might need to address it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="3f738-221">Identification du décalage</span><span class="sxs-lookup"><span data-stu-id="3f738-221">Identifying skew</span></span>
<span data-ttu-id="3f738-222">Un moyen simple d’identifier une table ayant subi un décalage consiste à utiliser `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="3f738-222">A simple way to identify a table as skewed is to use `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="3f738-223">Il s’agit d’une solution simple et rapide pour afficher le nombre de lignes de la table stockées dans chacune des 60 distributions de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="3f738-223">This is a very quick and simple way to see the number of table rows that are stored in each of the 60 distributions of your database.</span></span>  <span data-ttu-id="3f738-224">N’oubliez que pour obtenir les performances les plus équilibrées, les lignes de votre table distribuée doivent être partagées uniformément entre toutes les distributions.</span><span class="sxs-lookup"><span data-stu-id="3f738-224">Remember that for the most balanced performance, the rows in your distributed table should be spread evenly across all the distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="3f738-225">Toutefois, si vous interrogez les vues de gestion dynamique (DMV) Azure SQL Data Warehouse, vous pouvez effectuer une analyse plus détaillée.</span><span class="sxs-lookup"><span data-stu-id="3f738-225">However, if you query the Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="3f738-226">Pour commencer, créez la vue [dbo.vTableSizes][dbo.vTableSizes] en utilisant le SQL de l’article [Vue d’ensemble des tables][Overview].</span><span class="sxs-lookup"><span data-stu-id="3f738-226">To start, create the view [dbo.vTableSizes][dbo.vTableSizes] view using the SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="3f738-227">Une fois la vue créée, exécutez cette requête pour identifier les tables dont le décalage des données est supérieur à 10 %.</span><span class="sxs-lookup"><span data-stu-id="3f738-227">Once the view is created, run this query to identify which tables have more than 10% data skew.</span></span>

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

### <a name="resolving-data-skew"></a><span data-ttu-id="3f738-228">Résolution du décalage des données</span><span class="sxs-lookup"><span data-stu-id="3f738-228">Resolving data skew</span></span>
<span data-ttu-id="3f738-229">Tous les décalages ne sont pas suffisants pour garantir un correctif.</span><span class="sxs-lookup"><span data-stu-id="3f738-229">Not all skew is enough to warrant a fix.</span></span>  <span data-ttu-id="3f738-230">Dans certains cas, les performances d’une table dans certaines requêtes peuvent annuler les dommages liés au décalage des données.</span><span class="sxs-lookup"><span data-stu-id="3f738-230">In some cases, the performance of a table in some queries can outweigh the harm of data skew.</span></span>  <span data-ttu-id="3f738-231">Pour déterminer si vous devez résoudre un décalage des données dans une table, vous devez comprendre au mieux les volumes de données et les requêtes dans votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="3f738-231">To decide if you should resolve data skew in a table, you should understand as much as possible about the data volumes and queries in your workload.</span></span>   <span data-ttu-id="3f738-232">Vous pouvez suivre les étapes de l’article relatif à la [surveillance des requêtes][Query Monitoring] pour analyser l’impact du décalage sur les performances des requêtes, en particulier sur leur durée d’exécution sur chaque distribution.</span><span class="sxs-lookup"><span data-stu-id="3f738-232">One way to look at the impact of skew is to use the steps in the [Query Monitoring][Query Monitoring] article to monitor the impact of skew on query performance and specifically the impact to how long queries take to complete on the individual distributions.</span></span>

<span data-ttu-id="3f738-233">La distribution de données consiste à trouver le juste équilibre entre la réduction du décalage des données et la réduction du déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="3f738-233">Distributing data is a matter of finding the right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="3f738-234">Ces buts peuvent s’opposer, et parfois, vous pouvez conserver le décalage des données afin de réduire le déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="3f738-234">These can be opposing goals, and sometimes you will want to keep data skew in order to reduce data movement.</span></span> <span data-ttu-id="3f738-235">Par exemple, quand la colonne de distribution est souvent la colonne partagée dans les jointures et les agrégations, vous devez minimiser le déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="3f738-235">For example, when the distribution column is frequently the shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="3f738-236">L’avantage d’un déplacement minimal des données peut compenser l’impact d’un décalage des données.</span><span class="sxs-lookup"><span data-stu-id="3f738-236">The benefit of having the minimal data movement might outweigh the impact of having data skew.</span></span>

<span data-ttu-id="3f738-237">La méthode classique permettant de résoudre un décalage des données consiste à recréer la table avec une colonne de distribution différente.</span><span class="sxs-lookup"><span data-stu-id="3f738-237">The typical way to resolve data skew is to re-create the table with a different distribution column.</span></span> <span data-ttu-id="3f738-238">Dans la mesure où il n’existe aucun moyen de modifier la colonne de distribution d’une table existante, vous devez recréer la distribution d’une table avec un [CTAS][].</span><span class="sxs-lookup"><span data-stu-id="3f738-238">Since there is no way to change the distribution column on an existing table, the way to change the distribution of a table it to recreate it with a [CTAS][].</span></span>  <span data-ttu-id="3f738-239">Voici deux exemples illustrant comment résoudre le décalage de données :</span><span class="sxs-lookup"><span data-stu-id="3f738-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-the-table-with-a-new-distribution-column"></a><span data-ttu-id="3f738-240">Exemple 1 : Recréer la table avec une nouvelle colonne de distribution</span><span class="sxs-lookup"><span data-stu-id="3f738-240">Example 1: Re-create the table with a new distribution column</span></span>
<span data-ttu-id="3f738-241">Cet exemple utilise [CTAS][] pour recréer une table avec une colonne de distribution par hachage différente.</span><span class="sxs-lookup"><span data-stu-id="3f738-241">This example uses [CTAS][] to re-create a table with a different hash distribution column.</span></span>

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

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] TO [FactInternetSales];
```

### <a name="example-2-re-create-the-table-using-round-robin-distribution"></a><span data-ttu-id="3f738-242">Exemple 2 : Recréer la table à l’aide de la distribution par tourniquet (round robin)</span><span class="sxs-lookup"><span data-stu-id="3f738-242">Example 2: Re-create the table using round robin distribution</span></span>
<span data-ttu-id="3f738-243">Cet exemple utilise [CTAS][] pour recréer une table avec une distribution par tourniquet (round robin) et non par hachage.</span><span class="sxs-lookup"><span data-stu-id="3f738-243">This example uses [CTAS][] to re-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="3f738-244">Cette modification génère une répartition uniforme des données au prix d’un déplacement des données plus important.</span><span class="sxs-lookup"><span data-stu-id="3f738-244">This change will produce even data distribution at the cost of increased data movement.</span></span>

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

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] TO [FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="3f738-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3f738-245">Next steps</span></span>
<span data-ttu-id="3f738-246">Pour en savoir plus sur la conception des tables, consultez les articles [Distribuer][Distribute], [Index][Index], [Partition][Partition], [Types de données][Data Types], [Statistiques][Statistics] et [Tables temporaires][Temporary].</span><span class="sxs-lookup"><span data-stu-id="3f738-246">To learn more about table design, see the [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="3f738-247">Pour obtenir une vue d’ensemble des bonnes pratiques, consultez [Bonnes pratiques pour Azure SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="3f738-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
