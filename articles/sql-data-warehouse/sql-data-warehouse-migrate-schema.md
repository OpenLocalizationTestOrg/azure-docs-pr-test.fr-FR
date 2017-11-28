---
title: "aaaMigrate votre entrepôt de données de tooSQL schéma | Documents Microsoft"
description: "Conseils pour migrer votre tooAzure de schéma SQL Data Warehouse pour développer des solutions."
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
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a><span data-ttu-id="df347-103">Migrer votre tooSQL schémas l’entrepôt de données</span><span class="sxs-lookup"><span data-stu-id="df347-103">Migrate your schemas tooSQL Data Warehouse</span></span>
<span data-ttu-id="df347-104">Conseils pour la migration de votre tooSQL de schémas SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="df347-104">Guidance for migrating your SQL schemas tooSQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="df347-105">Planification de la migration du schéma</span><span class="sxs-lookup"><span data-stu-id="df347-105">Plan your schema migration</span></span>

<span data-ttu-id="df347-106">Lorsque vous planifiez une migration, consultez hello [vue d’ensemble de la table] [ table overview] toobecome familiarisé avec les considérations de conception de table tels que les statistiques de distribution, le partitionnement et l’indexation.</span><span class="sxs-lookup"><span data-stu-id="df347-106">As you plan a migration, see hello [table overview][table overview] toobecome familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="df347-107">Elle dresse également la liste de certaines [fonctionnalités de table non prises en charge][unsupported table features] et leurs solutions de contournement.</span><span class="sxs-lookup"><span data-stu-id="df347-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a><span data-ttu-id="df347-108">Utiliser des bases de données de schémas définis par l’utilisateur tooconsolidate</span><span class="sxs-lookup"><span data-stu-id="df347-108">Use user-defined schemas tooconsolidate databases</span></span>

<span data-ttu-id="df347-109">Votre charge de travail existante a probablement plusieurs bases de données.</span><span class="sxs-lookup"><span data-stu-id="df347-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="df347-110">Par exemple, un entrepôt de données SQL Server peut inclure une base de données de la zone de transit, une base de données de l’entrepôt de données et quelques bases de données de mini-Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="df347-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="df347-111">Dans cette topologie, chaque base de données s’exécute comme une charge de travail distincte avec des stratégies de sécurité distinctes.</span><span class="sxs-lookup"><span data-stu-id="df347-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="df347-112">En revanche, SQL Data Warehouse exécute la charge de travail entrepôt de données entière hello au sein d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="df347-112">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="df347-113">Les jointures entre plusieurs bases de données ne sont pas autorisées.</span><span class="sxs-lookup"><span data-stu-id="df347-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="df347-114">Par conséquent, l’entrepôt de données SQL attend que toutes les tables utilisées par toobe de l’entrepôt de données hello stockée dans une base de données hello.</span><span class="sxs-lookup"><span data-stu-id="df347-114">Therefore, SQL Data Warehouse expects all tables used by hello data warehouse toobe stored within hello one database.</span></span>

<span data-ttu-id="df347-115">Nous recommandons l’utilisation de schémas définis par l’utilisateur tooconsolidate votre charge de travail existante dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="df347-115">We recommend using user-defined schemas tooconsolidate your existing workload into one database.</span></span> <span data-ttu-id="df347-116">Pour obtenir des exemples, consultez [Schémas définis par l’utilisateur](sql-data-warehouse-develop-user-defined-schemas.md)</span><span class="sxs-lookup"><span data-stu-id="df347-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="df347-117">Utilisation des types de données compatibles</span><span class="sxs-lookup"><span data-stu-id="df347-117">Use compatible data types</span></span>
<span data-ttu-id="df347-118">Modifiez votre toobe de types de données compatible avec l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="df347-118">Modify your data types toobe compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="df347-119">Consultez l’article sur les [types de données][data types] pour obtenir la liste des types de données non pris en charge et pris en charge.</span><span class="sxs-lookup"><span data-stu-id="df347-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="df347-120">Cette rubrique fournit des solutions de contournement pour les types de hello non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="df347-120">That topic gives workarounds for hello unsupported types.</span></span> <span data-ttu-id="df347-121">Il fournit également une requête tooidentify des types existants qui ne sont pas pris en charge dans l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="df347-121">It also provides a query tooidentify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="df347-122">Réduction de la taille de ligne</span><span class="sxs-lookup"><span data-stu-id="df347-122">Minimize row size</span></span>
<span data-ttu-id="df347-123">Pour de meilleures performances, réduisez la longueur de la ligne hello de vos tables.</span><span class="sxs-lookup"><span data-stu-id="df347-123">For best performance, minimize hello row length of your tables.</span></span> <span data-ttu-id="df347-124">Car plus courtes ligne entraîner des performances de toobetter, utilisez hello plus petit types de données qui fonctionnent pour vos données.</span><span class="sxs-lookup"><span data-stu-id="df347-124">Since shorter row lengths lead toobetter performance, use hello smallest data types that work for your data.</span></span> 

<span data-ttu-id="df347-125">Pour la largeur de ligne de table, PolyBase a une limite de 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="df347-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="df347-126">Si vous envisagez de données de tooload dans SQL Data Warehouse avec PolyBase, mettre à jour vos tableaux toohave des largeurs de ligne maximale de moins de 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="df347-126">If you plan tooload data into SQL Data Warehouse with PolyBase, update your tables toohave maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a><span data-ttu-id="df347-127">Spécifiez l’option de distribution hello</span><span class="sxs-lookup"><span data-stu-id="df347-127">Specify hello distribution option</span></span>
<span data-ttu-id="df347-128">SQL Data Warehouse est un système de base de données distribuées.</span><span class="sxs-lookup"><span data-stu-id="df347-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="df347-129">Chaque table est distribué ou répliquée sur les nœuds de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="df347-129">Each table is distributed or replicated across hello Compute nodes.</span></span> <span data-ttu-id="df347-130">Il existe une option de table qui vous permet de spécifier comment toodistribute hello des données.</span><span class="sxs-lookup"><span data-stu-id="df347-130">There's a table option that lets you specify how toodistribute hello data.</span></span> <span data-ttu-id="df347-131">choix de Hello est tourniquet (Round Robin) répliquées, ou hachage distribué.</span><span class="sxs-lookup"><span data-stu-id="df347-131">hello choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="df347-132">Chaque option a ses avantages et inconvénients.</span><span class="sxs-lookup"><span data-stu-id="df347-132">Each has pros and cons.</span></span> <span data-ttu-id="df347-133">Si vous ne spécifiez l’option de distribution hello, SQL Data Warehouse utilisera alternée comme valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="df347-133">If you don't specify hello distribution option, SQL Data Warehouse will use round-robin as hello default.</span></span>

- <span data-ttu-id="df347-134">Tourniquet est par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="df347-134">Round-robin is hello default.</span></span> <span data-ttu-id="df347-135">Il est toouse la plus simple de hello et charge les données de hello aussi rapides que possible, mais les jointures nécessitera le déplacement des données, ce qui ralentissent les performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="df347-135">It is hello simplest toouse, and loads hello data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="df347-136">Magasins répliquées une copie de la table hello sur chaque nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="df347-136">Replicated stores a copy of hello table on each Compute node.</span></span> <span data-ttu-id="df347-137">Les tables répliquées sont performantes, car elles ne nécessitent pas le déplacement des données pour les jointures et les agrégations.</span><span class="sxs-lookup"><span data-stu-id="df347-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="df347-138">Elles requièrent cependant un stockage supplémentaire et sont par conséquent mieux adaptées à des tables plus petites.</span><span class="sxs-lookup"><span data-stu-id="df347-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="df347-139">Hachage distribué distribue les lignes hello sur tous les nœuds hello via une fonction de hachage.</span><span class="sxs-lookup"><span data-stu-id="df347-139">Hash distributed distributes hello rows across all hello nodes via a hash function.</span></span> <span data-ttu-id="df347-140">Tables de hachage distribuée sont cœur hello d’entrepôt de données SQL, car elles sont conçues tooprovide les performances de requête sur des tables volumineuses.</span><span class="sxs-lookup"><span data-stu-id="df347-140">Hash distributed tables are hello heart of SQL Data Warehouse since they are designed tooprovide high query performance on large tables.</span></span> <span data-ttu-id="df347-141">Cette option requiert une planification tooselect hello meilleure colonne sur les données de hello toodistribute.</span><span class="sxs-lookup"><span data-stu-id="df347-141">This option requires some planning tooselect hello best column on which toodistribute hello data.</span></span> <span data-ttu-id="df347-142">Toutefois, si vous n’en choisissez hello de colonne meilleures hello première fois, vous pouvez distribuer facilement nouveau hello des données sur une autre colonne.</span><span class="sxs-lookup"><span data-stu-id="df347-142">However, if you don't choose hello best column hello first time, you can easily re-distribute hello data on a different column.</span></span> 

<span data-ttu-id="df347-143">toochoose hello meilleure option de distribution pour chaque table, consultez [Distributed tables](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="df347-143">toochoose hello best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="df347-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="df347-144">Next steps</span></span>
<span data-ttu-id="df347-145">Une fois que vous avez migré votre tooSQL de schéma de base de données Data Warehouse, passez tooone Hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="df347-145">Once you have successfully migrated your database schema tooSQL Data Warehouse, proceed tooone of hello following articles:</span></span>

* <span data-ttu-id="df347-146">[Migration de vos données][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="df347-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="df347-147">[Migration de votre code][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="df347-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="df347-148">Pour plus d’informations sur les meilleures pratiques de l’entrepôt de données SQL, consultez hello [meilleures pratiques] [ best practices] l’article.</span><span class="sxs-lookup"><span data-stu-id="df347-148">For more about SQL Data Warehouse best practices, see hello [best practices][best practices] article.</span></span>

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
