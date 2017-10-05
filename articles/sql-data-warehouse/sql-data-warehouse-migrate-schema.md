---
title: "Migration de votre schéma vers SQL Data Warehouse | Microsoft Docs"
description: "Conseils relatifs à la migration de votre schéma vers Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 07ca2321852e276502187e768177e7e82bdfd080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-schemas-to-sql-data-warehouse"></a><span data-ttu-id="14116-103">Migration de votre schéma vers SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="14116-103">Migrate your schemas to SQL Data Warehouse</span></span>
<span data-ttu-id="14116-104">Conseils pour la migration de vos schémas SQL vers SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="14116-104">Guidance for migrating your SQL schemas to SQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="14116-105">Planification de la migration du schéma</span><span class="sxs-lookup"><span data-stu-id="14116-105">Plan your schema migration</span></span>

<span data-ttu-id="14116-106">Lorsque vous planifiez une migration, consultez la [vue d’ensemble des tables][table overview] pour vous familiariser avec les considérations relatives à la conception des tables tels que les statistiques, la distribution, le partitionnement et l’indexation.</span><span class="sxs-lookup"><span data-stu-id="14116-106">As you plan a migration, see the [table overview][table overview] to become familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="14116-107">Elle dresse également la liste de certaines [fonctionnalités de table non prises en charge][unsupported table features] et leurs solutions de contournement.</span><span class="sxs-lookup"><span data-stu-id="14116-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-to-consolidate-databases"></a><span data-ttu-id="14116-108">Utilisation des schémas définis par l’utilisateur pour consolider la base de données</span><span class="sxs-lookup"><span data-stu-id="14116-108">Use user-defined schemas to consolidate databases</span></span>

<span data-ttu-id="14116-109">Votre charge de travail existante a probablement plusieurs bases de données.</span><span class="sxs-lookup"><span data-stu-id="14116-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="14116-110">Par exemple, un entrepôt de données SQL Server peut inclure une base de données de la zone de transit, une base de données de l’entrepôt de données et quelques bases de données de mini-Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="14116-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="14116-111">Dans cette topologie, chaque base de données s’exécute comme une charge de travail distincte avec des stratégies de sécurité distinctes.</span><span class="sxs-lookup"><span data-stu-id="14116-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="14116-112">À l’inverse, SQL Data Warehouse exécute l’intégralité de la charge de travail des entrepôts de données au sein d’une seule et même base de données.</span><span class="sxs-lookup"><span data-stu-id="14116-112">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="14116-113">Les jointures entre plusieurs bases de données ne sont pas autorisées.</span><span class="sxs-lookup"><span data-stu-id="14116-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="14116-114">Par conséquent, SQL Data Warehouse s’attend que l’ensemble des tables utilisées par l’entrepôt de données soient stockées au sein d’une seule et même base de données.</span><span class="sxs-lookup"><span data-stu-id="14116-114">Therefore, SQL Data Warehouse expects all tables used by the data warehouse to be stored within the one database.</span></span>

<span data-ttu-id="14116-115">Nous vous recommandons d’utiliser des schémas définis par l’utilisateur pour consolider votre charge de travail existante dans une seule base de données.</span><span class="sxs-lookup"><span data-stu-id="14116-115">We recommend using user-defined schemas to consolidate your existing workload into one database.</span></span> <span data-ttu-id="14116-116">Pour obtenir des exemples, consultez [Schémas définis par l’utilisateur](sql-data-warehouse-develop-user-defined-schemas.md)</span><span class="sxs-lookup"><span data-stu-id="14116-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="14116-117">Utilisation des types de données compatibles</span><span class="sxs-lookup"><span data-stu-id="14116-117">Use compatible data types</span></span>
<span data-ttu-id="14116-118">Modifiez vos types de données pour être compatible avec SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="14116-118">Modify your data types to be compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="14116-119">Consultez l’article sur les [types de données][data types] pour obtenir la liste des types de données non pris en charge et pris en charge.</span><span class="sxs-lookup"><span data-stu-id="14116-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="14116-120">Cette rubrique fournit des solutions de contournement pour les types non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="14116-120">That topic gives workarounds for the unsupported types.</span></span> <span data-ttu-id="14116-121">Il fournit également une requête pour identifier les types existants qui ne sont pas pris en charge par SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="14116-121">It also provides a query to identify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="14116-122">Réduction de la taille de ligne</span><span class="sxs-lookup"><span data-stu-id="14116-122">Minimize row size</span></span>
<span data-ttu-id="14116-123">Pour de meilleures performances, réduisez la longueur de ligne de vos tables.</span><span class="sxs-lookup"><span data-stu-id="14116-123">For best performance, minimize the row length of your tables.</span></span> <span data-ttu-id="14116-124">Étant donné qu’une longueur de ligne plus courte permet de meilleures performances, utilisez les types de données les plus courts.</span><span class="sxs-lookup"><span data-stu-id="14116-124">Since shorter row lengths lead to better performance, use the smallest data types that work for your data.</span></span> 

<span data-ttu-id="14116-125">Pour la largeur de ligne de table, PolyBase a une limite de 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="14116-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="14116-126">Si vous envisagez de charger des données sur SQL Data Warehouse avec PolyBase, mettez à jour vos tables pour vous assurer que la largeur de ligne maximale ne dépasse pas 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="14116-126">If you plan to load data into SQL Data Warehouse with PolyBase, update your tables to have maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but the largest possible size of the row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and the defined row width is less than one MB. When loading rows, PolyBase allocates the full length of the variable-length data. The full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-the-distribution-option"></a><span data-ttu-id="14116-127">Spécification de l’option de distribution</span><span class="sxs-lookup"><span data-stu-id="14116-127">Specify the distribution option</span></span>
<span data-ttu-id="14116-128">SQL Data Warehouse est un système de base de données distribuées.</span><span class="sxs-lookup"><span data-stu-id="14116-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="14116-129">Chaque table est distribuée ou répliquée sur les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="14116-129">Each table is distributed or replicated across the Compute nodes.</span></span> <span data-ttu-id="14116-130">Il existe une option de table qui vous permet de spécifier comment distribuer les données.</span><span class="sxs-lookup"><span data-stu-id="14116-130">There's a table option that lets you specify how to distribute the data.</span></span> <span data-ttu-id="14116-131">Les options disponibles sont : tourniquet (Round Robin), répliquée, ou hachage distribué.</span><span class="sxs-lookup"><span data-stu-id="14116-131">The choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="14116-132">Chaque option a ses avantages et inconvénients.</span><span class="sxs-lookup"><span data-stu-id="14116-132">Each has pros and cons.</span></span> <span data-ttu-id="14116-133">Si vous ne spécifiez pas l’option de distribution, SQL Data Warehouse utilisera le tourniquet en tant que la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="14116-133">If you don't specify the distribution option, SQL Data Warehouse will use round-robin as the default.</span></span>

- <span data-ttu-id="14116-134">Tourniquet est la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="14116-134">Round-robin is the default.</span></span> <span data-ttu-id="14116-135">Il est le plus simple à utiliser, et charge les données aussi rapidement que possible, mais les jointures nécessiteront le déplacement de données, causant un ralentissement des performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="14116-135">It is the simplest to use, and loads the data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="14116-136">Les répliquées enregistrent une copie de la table dans chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="14116-136">Replicated stores a copy of the table on each Compute node.</span></span> <span data-ttu-id="14116-137">Les tables répliquées sont performantes, car elles ne nécessitent pas le déplacement des données pour les jointures et les agrégations.</span><span class="sxs-lookup"><span data-stu-id="14116-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="14116-138">Elles requièrent cependant un stockage supplémentaire et sont par conséquent mieux adaptées à des tables plus petites.</span><span class="sxs-lookup"><span data-stu-id="14116-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="14116-139">Le hachage distribué distribue les lignes sur tous les nœuds via une fonction de hachage.</span><span class="sxs-lookup"><span data-stu-id="14116-139">Hash distributed distributes the rows across all the nodes via a hash function.</span></span> <span data-ttu-id="14116-140">Les tables de hachage distribué sont au cœur de SQL Data Warehouse car elles sont conçues pour fournir d’excellentes performances de requête sur des tables volumineuses.</span><span class="sxs-lookup"><span data-stu-id="14116-140">Hash distributed tables are the heart of SQL Data Warehouse since they are designed to provide high query performance on large tables.</span></span> <span data-ttu-id="14116-141">Cette option nécessite une bonne planification afin de sélectionner la meilleure colonne sur laquelle distribuer les données.</span><span class="sxs-lookup"><span data-stu-id="14116-141">This option requires some planning to select the best column on which to distribute the data.</span></span> <span data-ttu-id="14116-142">Toutefois, si vous ne choisissez pas la meilleure colonne la première fois, vous pouvez facilement redistribuer les données sur une autre colonne.</span><span class="sxs-lookup"><span data-stu-id="14116-142">However, if you don't choose the best column the first time, you can easily re-distribute the data on a different column.</span></span> 

<span data-ttu-id="14116-143">Pour choisir la meilleure option de distribution pour chaque table, consultez [Tables distribuées](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="14116-143">To choose the best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="14116-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="14116-144">Next steps</span></span>
<span data-ttu-id="14116-145">Après avoir avez correctement migré votre schéma de base de données vers SQL Data Warehouse, passez à l’un des articles suivants :</span><span class="sxs-lookup"><span data-stu-id="14116-145">Once you have successfully migrated your database schema to SQL Data Warehouse, proceed to one of the following articles:</span></span>

* <span data-ttu-id="14116-146">[Migration de vos données][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="14116-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="14116-147">[Migration de votre code][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="14116-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="14116-148">Pour en savoir plus sur les bonnes pratiques relatives à SQL Data Warehouse, consultez l’article sur les [bonnes pratiques][best practices].</span><span class="sxs-lookup"><span data-stu-id="14116-148">For more about SQL Data Warehouse best practices, see the [best practices][best practices] article.</span></span>

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
