---
title: "Glossaire des outils des bases de données élastiques | Microsoft Docs"
description: "Explication des termes utilisés pour les outils de base de données élastique"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0fda4bb948bbed1c14d468519ba67cce9bc4e6c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="7fead-103">Glossaire des outils de base de données élastique</span><span class="sxs-lookup"><span data-stu-id="7fead-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="7fead-104">Les termes suivants sont définis pour les [outils des bases de données élastiques](sql-database-elastic-scale-introduction.md), une fonction de Base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7fead-104">The following terms are defined for the [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="7fead-105">Les outils permettent de gérer les [cartes de partition](sql-database-elastic-scale-shard-map-management.md) et incluent la [bibliothèque cliente](sql-database-elastic-database-client-library.md), [l’outil de fusion et de fractionnement](sql-database-elastic-scale-overview-split-and-merge.md), les [pools élastiques](sql-database-elastic-pool.md) et les [requêtes](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7fead-105">The tools are used to manage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include the [client library](sql-database-elastic-database-client-library.md), the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="7fead-106">Ces termes sont utilisés dans [Ajout d’une partition à l’aide des outils de base de données élastique](sql-database-elastic-scale-add-a-shard.md) et [Utiliser la classe RecoveryManager pour résoudre les problèmes de carte de partition](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7fead-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Termes liés ç l’infrastructure flexible][1]

<span data-ttu-id="7fead-108">**Base de données**: une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7fead-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="7fead-109">**Routage dépendant des données**: fonctionnalité qui permet à une application de se connecter à une partition en fonction d’une clé de partitionnement spécifique.</span><span class="sxs-lookup"><span data-stu-id="7fead-109">**Data dependent routing**: The functionality that enables an application to connect to a shard given a specific sharding key.</span></span> <span data-ttu-id="7fead-110">Consultez [Routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="7fead-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="7fead-111">Comparer à la **[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="7fead-111">Compare to **[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="7fead-112">**Carte de partitions globale** : la carte correspondant aux clés de partitionnement et à leurs partitions respectives au sein d’un **jeu de partitions**.</span><span class="sxs-lookup"><span data-stu-id="7fead-112">**Global shard map**: The map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="7fead-113">La carte de partitions globale est stockée dans le **gestionnaire des cartes de partitions**.</span><span class="sxs-lookup"><span data-stu-id="7fead-113">The global shard map is stored in the **shard map manager**.</span></span> <span data-ttu-id="7fead-114">Comparer à la **carte de partitions locale**.</span><span class="sxs-lookup"><span data-stu-id="7fead-114">Compare to **local shard map**.</span></span>

<span data-ttu-id="7fead-115">**Carte de partitions de liste**: carte de partitions dans laquelle les clés de partitionnement sont mappées individuellement.</span><span class="sxs-lookup"><span data-stu-id="7fead-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="7fead-116">Comparer à la **carte de partitions de plage**.</span><span class="sxs-lookup"><span data-stu-id="7fead-116">Compare to **Range Shard Map**.</span></span>   

<span data-ttu-id="7fead-117">**Carte de partitions locale**: stockée sur une partition, la carte de partitions locale contient des mappages pour les shardlets se trouvant sur la partition.</span><span class="sxs-lookup"><span data-stu-id="7fead-117">**Local shard map**: Stored on a shard, the local shard map contains mappings for the shardlets that reside on the shard.</span></span>

<span data-ttu-id="7fead-118">**Requête sur plusieurs partitions**: possibilité d'émettre une requête sur plusieurs partitions ; les ensembles de résultats sont retournés à l'aide de la sémantique UNION ALL (également appelée « requête de distribution ramifiée »).</span><span class="sxs-lookup"><span data-stu-id="7fead-118">**Multi-shard query**: The ability to issue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="7fead-119">Comparer au **routage dépendant des données**.</span><span class="sxs-lookup"><span data-stu-id="7fead-119">Compare to **data dependent routing**.</span></span>

<span data-ttu-id="7fead-120">**Mutualisée** et **mono-utilisateur** : montre une base de données à un seul utilisateur et une base de données à architecture mutualisée :</span><span class="sxs-lookup"><span data-stu-id="7fead-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Bases de données mono-utilisateur et mutualisée](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="7fead-122">Voici une représentation de bases de données **partitionnées** de type mono-utilisateur et mutualisée.</span><span class="sxs-lookup"><span data-stu-id="7fead-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Bases de données mono-utilisateur et mutualisée](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="7fead-124">**Carte de partitions de plage**: carte de partitions dans laquelle la stratégie de distribution des partitions est basée sur plusieurs plages de valeurs contiguës.</span><span class="sxs-lookup"><span data-stu-id="7fead-124">**Range shard map**: A shard map in which the shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="7fead-125">**Tables de référence**: tables qui ne sont pas partitionnées, mais qui sont répliquées sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="7fead-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="7fead-126">Par exemple, les codes postaux peuvent être stockés dans une table de référence.</span><span class="sxs-lookup"><span data-stu-id="7fead-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="7fead-127">**Partition**: base de données SQL Azure qui stocke les données provenant d'un jeu de données partitionnées.</span><span class="sxs-lookup"><span data-stu-id="7fead-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="7fead-128">**Élasticité des partitions** : capacité à effectuer une **mise à l’échelle horizontale** et une **mise à l’échelle verticale**.</span><span class="sxs-lookup"><span data-stu-id="7fead-128">**Shard elasticity**: The ability to perform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="7fead-129">**Tables partitionnées**: tables qui sont partitionnées, c'est-à-dire dont les données sont distribuées entre des partitions en fonction de la valeur de leur clé de partitionnement.</span><span class="sxs-lookup"><span data-stu-id="7fead-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="7fead-130">**Clé de partitionnement**: valeur de colonne qui détermine comment les données sont réparties entre les partitions.</span><span class="sxs-lookup"><span data-stu-id="7fead-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="7fead-131">Les types de valeur disponibles sont les suivants : **int**, **bigint**, **varbinary** ou **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="7fead-131">The value type can be one of the following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="7fead-132">**Ensemble de partitions**: collection de partitions qui sont attribuées à la même carte de partitions dans le gestionnaire des cartes de partitions.</span><span class="sxs-lookup"><span data-stu-id="7fead-132">**Shard set**: The collection of shards that are attributed to the same shard map in the shard map manager.</span></span>  

<span data-ttu-id="7fead-133">**Shardlet**: toutes les données associées à la valeur unique d’une clé de partitionnement sur une partition.</span><span class="sxs-lookup"><span data-stu-id="7fead-133">**Shardlet**: All of the data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="7fead-134">Un shardlet est la plus petite unité de transfert de données possible lors de la redistribution des tables partitionnées.</span><span class="sxs-lookup"><span data-stu-id="7fead-134">A shardlet is the smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="7fead-135">**Carte de partitions**: jeu de mappages composé de clés de partitionnement et de leurs partitions respectives.</span><span class="sxs-lookup"><span data-stu-id="7fead-135">**Shard map**: The set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="7fead-136">**Gestionnaire des cartes de partitions**: objet de gestion et magasin de données qui comporte les cartes de partitions, les emplacements des partitions et les mappages pour un ou plusieurs ensembles de partitions.</span><span class="sxs-lookup"><span data-stu-id="7fead-136">**Shard map manager**: A management object and data store that contains the shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Mappages][2]

## <a name="verbs"></a><span data-ttu-id="7fead-138">Verbes et adverbes</span><span class="sxs-lookup"><span data-stu-id="7fead-138">Verbs</span></span>
<span data-ttu-id="7fead-139">**Mise à l'échelle horizontale**: montée en charge (augmentation ou réduction) d'une collection de partitions en ajoutant ou supprimant des partitions dans une carte de partitions, comme dans l'exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7fead-139">**Horizontal scaling**: The act of scaling out (or in) a collection of shards by adding or removing shards to a shard map, as shown below.</span></span>

![Mise à l’échelle horizontale et verticale][3]

<span data-ttu-id="7fead-141">**Fusionner**: action de déplacer les shardlets de deux partitions vers une seule partition et de mettre à jour la carte de partitions en conséquence.</span><span class="sxs-lookup"><span data-stu-id="7fead-141">**Merge**: The act of moving shardlets from two shards to one shard and updating the shard map accordingly.</span></span>

<span data-ttu-id="7fead-142">**Déplacement de shardlet**: action de déplacer un shardlet unique vers une autre partition.</span><span class="sxs-lookup"><span data-stu-id="7fead-142">**Shardlet move**: The act of moving a single shardlet to a different shard.</span></span> 

<span data-ttu-id="7fead-143">**Partitionner**: action qui consiste à partitionner horizontalement des données structurées de façon identique sur plusieurs bases de données en fonction d’une clé de partitionnement.</span><span class="sxs-lookup"><span data-stu-id="7fead-143">**Shard**: The act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="7fead-144">**Fractionner**: action de déplacer plusieurs shardlets d'une partition vers une autre (généralement nouvelle).</span><span class="sxs-lookup"><span data-stu-id="7fead-144">**Split**: The act of moving several shardlets from one shard to another (typically new) shard.</span></span> <span data-ttu-id="7fead-145">Une clé de partitionnement est fournie par l'utilisateur comme point de fractionnement.</span><span class="sxs-lookup"><span data-stu-id="7fead-145">A sharding key is provided by the user as the split point.</span></span>

<span data-ttu-id="7fead-146">**Mise à l'échelle verticale**: mise à l'échelle (augmentation ou réduction) du niveau de performances d'une partition individuelle.</span><span class="sxs-lookup"><span data-stu-id="7fead-146">**Vertical Scaling**: The act of scaling up (or down) the performance level of an individual shard.</span></span> <span data-ttu-id="7fead-147">Par exemple, modifier une partition standard vers l’édition Premium (qui génère plus de ressources informatiques).</span><span class="sxs-lookup"><span data-stu-id="7fead-147">For example, changing a shard from Standard to Premium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

