---
title: "glossaire d’outils de base de données aaaElastic | Documents Microsoft"
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
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="43ed6-103">Glossaire des outils de base de données élastique</span><span class="sxs-lookup"><span data-stu-id="43ed6-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="43ed6-104">Hello termes suivants sont définis pour hello [outils de base de données élastique](sql-database-elastic-scale-introduction.md), une fonctionnalité de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="43ed6-104">hello following terms are defined for hello [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="43ed6-105">outils Hello sont utilisée toomanage [mappe les partitions](sql-database-elastic-scale-shard-map-management.md)et inclure hello [bibliothèque cliente](sql-database-elastic-database-client-library.md), hello [outil de fusion et fractionnement](sql-database-elastic-scale-overview-split-and-merge.md), [pools élastiques](sql-database-elastic-pool.md), et [requêtes](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43ed6-105">hello tools are used toomanage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include hello [client library](sql-database-elastic-database-client-library.md), hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="43ed6-106">Ces termes sont utilisés dans [Ajout d’une partition à l’aide des outils de base de données élastique](sql-database-elastic-scale-add-a-shard.md) et [à l’aide des problèmes du mappage de partitions hello RecoveryManager classe toofix](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="43ed6-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Termes liés ç l’infrastructure flexible][1]

<span data-ttu-id="43ed6-108">**Base de données**: une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="43ed6-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="43ed6-109">**Routage dépendant des données**: hello fonctionnalité qui permet à une partition de tooa application tooconnect une clé de partitionnement spécifique.</span><span class="sxs-lookup"><span data-stu-id="43ed6-109">**Data dependent routing**: hello functionality that enables an application tooconnect tooa shard given a specific sharding key.</span></span> <span data-ttu-id="43ed6-110">Consultez [Routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="43ed6-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="43ed6-111">Comparer trop**[requête de plusieurs partitions](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="43ed6-111">Compare too**[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="43ed6-112">**Carte de partitions globales**: mappage hello entre les clés de partitionnement et de leurs partitions respectifs dans un **ensemble de partitions**.</span><span class="sxs-lookup"><span data-stu-id="43ed6-112">**Global shard map**: hello map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="43ed6-113">carte de partitions globales de Hello est stocké dans hello **Gestionnaire de carte de partitions**.</span><span class="sxs-lookup"><span data-stu-id="43ed6-113">hello global shard map is stored in hello **shard map manager**.</span></span> <span data-ttu-id="43ed6-114">Comparer trop**carte de partitions local**.</span><span class="sxs-lookup"><span data-stu-id="43ed6-114">Compare too**local shard map**.</span></span>

<span data-ttu-id="43ed6-115">**Carte de partitions de liste**: carte de partitions dans laquelle les clés de partitionnement sont mappées individuellement.</span><span class="sxs-lookup"><span data-stu-id="43ed6-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="43ed6-116">Comparer trop**carte de partitions plage**.</span><span class="sxs-lookup"><span data-stu-id="43ed6-116">Compare too**Range Shard Map**.</span></span>   

<span data-ttu-id="43ed6-117">**Carte de partitions local**: stockés sur une partition, carte de partitions local de hello contient les mappages de shardlets hello qui se trouvent sur les partitions hello.</span><span class="sxs-lookup"><span data-stu-id="43ed6-117">**Local shard map**: Stored on a shard, hello local shard map contains mappings for hello shardlets that reside on hello shard.</span></span>

<span data-ttu-id="43ed6-118">**Requête de plusieurs partition**: hello capacité tooissue une requête sur plusieurs partitions ; les jeux de résultats sont retournées à l’aide de la sémantique de UNION ALL (également appelée « requête distribution ramifiée »).</span><span class="sxs-lookup"><span data-stu-id="43ed6-118">**Multi-shard query**: hello ability tooissue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="43ed6-119">Comparer trop**routage dépendant des données**.</span><span class="sxs-lookup"><span data-stu-id="43ed6-119">Compare too**data dependent routing**.</span></span>

<span data-ttu-id="43ed6-120">**Mutualisée** et **mono-utilisateur** : montre une base de données à un seul utilisateur et une base de données à architecture mutualisée :</span><span class="sxs-lookup"><span data-stu-id="43ed6-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Bases de données mono-utilisateur et mutualisée](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="43ed6-122">Voici une représentation de bases de données **partitionnées** de type mono-utilisateur et mutualisée.</span><span class="sxs-lookup"><span data-stu-id="43ed6-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Bases de données mono-utilisateur et mutualisée](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="43ed6-124">**Carte de partitions plage**: une carte de partitions dans le hello stratégie de distribution de partition est basée sur plusieurs plages de valeurs contiguës.</span><span class="sxs-lookup"><span data-stu-id="43ed6-124">**Range shard map**: A shard map in which hello shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="43ed6-125">**Tables de référence**: tables qui ne sont pas partitionnées, mais qui sont répliquées sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="43ed6-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="43ed6-126">Par exemple, les codes postaux peuvent être stockés dans une table de référence.</span><span class="sxs-lookup"><span data-stu-id="43ed6-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="43ed6-127">**Partition**: base de données SQL Azure qui stocke les données provenant d'un jeu de données partitionnées.</span><span class="sxs-lookup"><span data-stu-id="43ed6-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="43ed6-128">**Élasticité de la partition**: hello tooperform capacité deux **mise à l’échelle horizontale** et **mise à l’échelle verticale**.</span><span class="sxs-lookup"><span data-stu-id="43ed6-128">**Shard elasticity**: hello ability tooperform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="43ed6-129">**Tables partitionnées**: tables qui sont partitionnées, c'est-à-dire dont les données sont distribuées entre des partitions en fonction de la valeur de leur clé de partitionnement.</span><span class="sxs-lookup"><span data-stu-id="43ed6-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="43ed6-130">**Clé de partitionnement**: valeur de colonne qui détermine comment les données sont réparties entre les partitions.</span><span class="sxs-lookup"><span data-stu-id="43ed6-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="43ed6-131">Hello type valeur peut être un des éléments suivants de hello : **int**, **bigint**, **varbinary**, ou **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="43ed6-131">hello value type can be one of hello following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="43ed6-132">**Ensemble de partitions**: hello collection de partitions qui sont attribué toohello même carte de partitions dans le Gestionnaire de carte de partitions hello.</span><span class="sxs-lookup"><span data-stu-id="43ed6-132">**Shard set**: hello collection of shards that are attributed toohello same shard map in hello shard map manager.</span></span>  

<span data-ttu-id="43ed6-133">**Shardlet**: toutes les données hello associées à une seule valeur d’une clé de partitionnement sur une partition.</span><span class="sxs-lookup"><span data-stu-id="43ed6-133">**Shardlet**: All of hello data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="43ed6-134">Un shardlet est hello plus petite unité de déplacement de données possible lors de la redistribution des tables partitionnées.</span><span class="sxs-lookup"><span data-stu-id="43ed6-134">A shardlet is hello smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="43ed6-135">**Carte de partitions**: hello ensemble de mappages entre les clés de partitionnement et de leurs partitions respectifs.</span><span class="sxs-lookup"><span data-stu-id="43ed6-135">**Shard map**: hello set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="43ed6-136">**Gestionnaire de cartes de partitions**: un magasin de données et l’objet d’administration qui contient l’ou les tables précèdent hello partitions, des emplacements de partition et des mappages pour un ou plusieurs ensembles de partitions.</span><span class="sxs-lookup"><span data-stu-id="43ed6-136">**Shard map manager**: A management object and data store that contains hello shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Mappages][2]

## <a name="verbs"></a><span data-ttu-id="43ed6-138">Verbes et adverbes</span><span class="sxs-lookup"><span data-stu-id="43ed6-138">Verbs</span></span>
<span data-ttu-id="43ed6-139">**Mise à l’échelle horizontale**: act hello de mise à l’échelle (ou) une collection de partitions en ajoutant ou supprimant la carte de partitions partitions tooa, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="43ed6-139">**Horizontal scaling**: hello act of scaling out (or in) a collection of shards by adding or removing shards tooa shard map, as shown below.</span></span>

![Mise à l’échelle horizontale et verticale][3]

<span data-ttu-id="43ed6-141">**Fusion**: act hello de déplacement de shardlets à partir de la partition de tooone deux partitions et de mise à jour de carte de partitions hello en conséquence.</span><span class="sxs-lookup"><span data-stu-id="43ed6-141">**Merge**: hello act of moving shardlets from two shards tooone shard and updating hello shard map accordingly.</span></span>

<span data-ttu-id="43ed6-142">**Déplacement de Shardlets**: act hello de déplacement d’une seul shardlet tooa autre partition.</span><span class="sxs-lookup"><span data-stu-id="43ed6-142">**Shardlet move**: hello act of moving a single shardlet tooa different shard.</span></span> 

<span data-ttu-id="43ed6-143">**Partition**: act hello de partitionnement horizontal identique des données structurées entre plusieurs bases de données basées sur une clé de partitionnement.</span><span class="sxs-lookup"><span data-stu-id="43ed6-143">**Shard**: hello act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="43ed6-144">**Fractionnement**: act hello du déplacement de plusieurs shardlets à partir de la partition (en général nouveau) de tooanother une seule partition.</span><span class="sxs-lookup"><span data-stu-id="43ed6-144">**Split**: hello act of moving several shardlets from one shard tooanother (typically new) shard.</span></span> <span data-ttu-id="43ed6-145">Une clé de partitionnement est fournie par l’utilisateur de hello comme point de fractionnement hello.</span><span class="sxs-lookup"><span data-stu-id="43ed6-145">A sharding key is provided by hello user as hello split point.</span></span>

<span data-ttu-id="43ed6-146">**Mise à l’échelle verticale**: act hello de mise à l’échelle des (ou vers le bas) hello du niveau de performance d’une partition.</span><span class="sxs-lookup"><span data-stu-id="43ed6-146">**Vertical Scaling**: hello act of scaling up (or down) hello performance level of an individual shard.</span></span> <span data-ttu-id="43ed6-147">Par exemple, remplacer une partition à partir de tooPremium Standard (ce qui entraîne davantage de ressources informatiques).</span><span class="sxs-lookup"><span data-stu-id="43ed6-147">For example, changing a shard from Standard tooPremium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

