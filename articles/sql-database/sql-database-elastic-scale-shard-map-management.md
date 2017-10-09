---
title: "aaaScale une base de données SQL Azure | Documents Microsoft"
description: "Comment toouse hello ShardMapManager, la bibliothèque cliente de base de données élastique"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a><span data-ttu-id="dc7f0-103">Montée en charge des bases de données avec le Gestionnaire de carte de partitions hello</span><span class="sxs-lookup"><span data-stu-id="dc7f0-103">Scale out databases with hello shard map manager</span></span>
<span data-ttu-id="dc7f0-104">tooeasily montée de bases de données sur SQL Azure, utilisez un gestionnaire de carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-104">tooeasily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="dc7f0-105">Gestionnaire de cartes de partitions Hello est une base de données spécial qui gère les informations de mappage global sur toutes les partitions (bases de données) dans un ensemble de partitions.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-105">hello shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="dc7f0-106">Hello métadonnées permettent à une application tooconnect toohello base de données appropriée en fonction de valeur hello Hello **clé de partitionnement**.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-106">hello metadata allows an application tooconnect toohello correct database based upon hello value of hello **sharding key**.</span></span> <span data-ttu-id="dc7f0-107">En outre, chaque partition dans l’ensemble de hello contient les cartes qui effectuent le suivi des données de partition locale hello (appelé **shardlets**).</span><span class="sxs-lookup"><span data-stu-id="dc7f0-107">In addition, every shard in hello set contains maps that track hello local shard data (known as **shardlets**).</span></span> 

![Gestion des cartes de partitions](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="dc7f0-109">Comprendre comment ces mappages sont construites est la gestion de carte tooshard essentielles.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-109">Understanding how these maps are constructed is essential tooshard map management.</span></span> <span data-ttu-id="dc7f0-110">Cette opération est effectuée à l’aide de hello [ShardMapManager classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), située dans hello [bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md) toomanage partition est associée.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-110">This is done using hello [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in hello [Elastic Database client library](sql-database-elastic-database-client-library.md) toomanage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="dc7f0-111">Cartes de partitions et mappages de partitions</span><span class="sxs-lookup"><span data-stu-id="dc7f0-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="dc7f0-112">Pour chaque partition, vous devez sélectionner le type hello de toocreate de carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-112">For each shard, you must select hello type of shard map toocreate.</span></span> <span data-ttu-id="dc7f0-113">choix de Hello dépend de l’architecture de base de données hello :</span><span class="sxs-lookup"><span data-stu-id="dc7f0-113">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="dc7f0-114">Client unique par base de données</span><span class="sxs-lookup"><span data-stu-id="dc7f0-114">Single tenant per database</span></span>  
2. <span data-ttu-id="dc7f0-115">Plusieurs clients par base de données (deux types) :</span><span class="sxs-lookup"><span data-stu-id="dc7f0-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="dc7f0-116">Mappage de liste</span><span class="sxs-lookup"><span data-stu-id="dc7f0-116">List mapping</span></span>
   2. <span data-ttu-id="dc7f0-117">Mappage de plage</span><span class="sxs-lookup"><span data-stu-id="dc7f0-117">Range mapping</span></span>

<span data-ttu-id="dc7f0-118">Pour un modèle de client unique, créez une carte de partitions de **mappage de liste** .</span><span class="sxs-lookup"><span data-stu-id="dc7f0-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="dc7f0-119">modèle de locataire unique Hello assigne une base de données par client.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-119">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="dc7f0-120">Il s’agit d’un modèle efficace pour les développeurs SaaS, car il simplifie la gestion.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Mappage de liste][1]

<span data-ttu-id="dc7f0-122">modèle d’architecture mutualisée Hello affecte plusieurs clients tooa une seule base de données (et vous pouvez distribuer des groupes de clients sur plusieurs bases de données).</span><span class="sxs-lookup"><span data-stu-id="dc7f0-122">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="dc7f0-123">Utilisez ce modèle lorsque vous attendez que chaque données de petite taille toohave client a besoin.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-123">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="dc7f0-124">Dans ce modèle, nous affectons une plage d’utilisation de base de données clients tooa **mappage de plage**.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-124">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Mappage de plage][2]

<span data-ttu-id="dc7f0-126">Ou vous pouvez implémenter un modèle de base de données à l’aide un *mappage de liste* tooassign plusieurs locataires tooa base de données unique.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-126">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="dc7f0-127">Par exemple, DB1 est toostore utilisé plus d’informations sur l’id de client 1 et 5, et DB2 stocke des données pour les locataires 7 et client 10.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-127">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Plusieurs clients sur une base de données unique][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="dc7f0-129">Types .Net pris en charge pour les clés de partitionnement</span><span class="sxs-lookup"><span data-stu-id="dc7f0-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="dc7f0-130">Hello de prise en charge de l’échelle élastique suivant .net Framework des types en tant que clés de partitionnement :</span><span class="sxs-lookup"><span data-stu-id="dc7f0-130">Elastic Scale support hello following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="dc7f0-131">integer</span><span class="sxs-lookup"><span data-stu-id="dc7f0-131">integer</span></span>
* <span data-ttu-id="dc7f0-132">long</span><span class="sxs-lookup"><span data-stu-id="dc7f0-132">long</span></span>
* <span data-ttu-id="dc7f0-133">guid</span><span class="sxs-lookup"><span data-stu-id="dc7f0-133">guid</span></span>
* <span data-ttu-id="dc7f0-134">byte[]</span><span class="sxs-lookup"><span data-stu-id="dc7f0-134">byte[]</span></span>  
* <span data-ttu-id="dc7f0-135">datetime</span><span class="sxs-lookup"><span data-stu-id="dc7f0-135">datetime</span></span>
* <span data-ttu-id="dc7f0-136">timespan</span><span class="sxs-lookup"><span data-stu-id="dc7f0-136">timespan</span></span>
* <span data-ttu-id="dc7f0-137">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="dc7f0-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="dc7f0-138">Liste et cartes de partitions de plage</span><span class="sxs-lookup"><span data-stu-id="dc7f0-138">List and range shard maps</span></span>
<span data-ttu-id="dc7f0-139">Vous pouvez construire des cartes de partition en utilisant des **listes de valeurs de clés de partitionnement individuelles** ou des **plages de valeurs de clés de partitionnement**.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="dc7f0-140">Cartes de partition de liste</span><span class="sxs-lookup"><span data-stu-id="dc7f0-140">List shard maps</span></span>
<span data-ttu-id="dc7f0-141">**Partitions** contiennent **shardlets** et mappage hello de shardlets tooshards est gérée par une carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-141">**Shards** contain **shardlets** and hello mapping of shardlets tooshards is maintained by a shard map.</span></span> <span data-ttu-id="dc7f0-142">A **carte de partitions liste** est une association entre les bases de données hello qui font Office de partitions et de hello des valeurs de clés qui identifient les shardlets hello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-142">A **list shard map** is an association between hello individual key values that identify hello shardlets and hello databases that serve as shards.</span></span>  <span data-ttu-id="dc7f0-143">**Liste des mappages** sont explicites et différentes valeurs de clé peuvent être mappé toohello même base de données.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-143">**List mappings** are explicit and different key values can be mapped toohello same database.</span></span> <span data-ttu-id="dc7f0-144">Par exemple, la clé 1 mappe tooDatabase A, et faire référence à des valeurs de clé 3 et 6 B. la base de données</span><span class="sxs-lookup"><span data-stu-id="dc7f0-144">For example, key 1 maps tooDatabase A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="dc7f0-145">Clé</span><span class="sxs-lookup"><span data-stu-id="dc7f0-145">Key</span></span> | <span data-ttu-id="dc7f0-146">Emplacement de partition</span><span class="sxs-lookup"><span data-stu-id="dc7f0-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="dc7f0-147">1</span><span class="sxs-lookup"><span data-stu-id="dc7f0-147">1</span></span> |<span data-ttu-id="dc7f0-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="dc7f0-148">Database_A</span></span> |
| <span data-ttu-id="dc7f0-149">3</span><span class="sxs-lookup"><span data-stu-id="dc7f0-149">3</span></span> |<span data-ttu-id="dc7f0-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="dc7f0-150">Database_B</span></span> |
| <span data-ttu-id="dc7f0-151">4</span><span class="sxs-lookup"><span data-stu-id="dc7f0-151">4</span></span> |<span data-ttu-id="dc7f0-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="dc7f0-152">Database_C</span></span> |
| <span data-ttu-id="dc7f0-153">6</span><span class="sxs-lookup"><span data-stu-id="dc7f0-153">6</span></span> |<span data-ttu-id="dc7f0-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="dc7f0-154">Database_B</span></span> |
| <span data-ttu-id="dc7f0-155">...</span><span class="sxs-lookup"><span data-stu-id="dc7f0-155">...</span></span> |<span data-ttu-id="dc7f0-156">...</span><span class="sxs-lookup"><span data-stu-id="dc7f0-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="dc7f0-157">Cartes de partitions de plage</span><span class="sxs-lookup"><span data-stu-id="dc7f0-157">Range shard maps</span></span>
<span data-ttu-id="dc7f0-158">Dans un **carte de partitions plage**, plage de clés hello est décrit par une paire **[faible valeur, la valeur élevée)** où hello *faible valeur* est hello de clé minimale dans la plage de hello et hello *Valeur élevée* est la première valeur hello plus élevé que hello plage.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-158">In a **range shard map**, hello key range is described by a pair **[Low Value, High Value)** where hello *Low Value* is hello minimum key in hello range, and hello *High Value* is hello first value higher than hello range.</span></span> 

<span data-ttu-id="dc7f0-159">Par exemple, **[0, 100)** inclut tous les entiers égaux ou supérieurs à 0 et inférieurs à 100.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="dc7f0-160">Notez que plusieurs plages peut point toohello de base de données et disjoints plages sont pris en charge (par exemple, [100,200) et [400,600) à la fois C point tooDatabase dans l’exemple hello ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="dc7f0-160">Note that multiple ranges can point toohello same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point tooDatabase C in hello example below.)</span></span>

| <span data-ttu-id="dc7f0-161">Clé</span><span class="sxs-lookup"><span data-stu-id="dc7f0-161">Key</span></span> | <span data-ttu-id="dc7f0-162">Emplacement de partition</span><span class="sxs-lookup"><span data-stu-id="dc7f0-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="dc7f0-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="dc7f0-163">[1,50)</span></span> |<span data-ttu-id="dc7f0-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="dc7f0-164">Database_A</span></span> |
| <span data-ttu-id="dc7f0-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="dc7f0-165">[50,100)</span></span> |<span data-ttu-id="dc7f0-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="dc7f0-166">Database_B</span></span> |
| <span data-ttu-id="dc7f0-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="dc7f0-167">[100,200)</span></span> |<span data-ttu-id="dc7f0-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="dc7f0-168">Database_C</span></span> |
| <span data-ttu-id="dc7f0-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="dc7f0-169">[400,600)</span></span> |<span data-ttu-id="dc7f0-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="dc7f0-170">Database_C</span></span> |
| <span data-ttu-id="dc7f0-171">...</span><span class="sxs-lookup"><span data-stu-id="dc7f0-171">...</span></span> |<span data-ttu-id="dc7f0-172">...</span><span class="sxs-lookup"><span data-stu-id="dc7f0-172">...</span></span> |

<span data-ttu-id="dc7f0-173">Chacune des tables hello ci-dessus est un exemple conceptuel d’un **ShardMap** objet.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-173">Each of hello tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="dc7f0-174">Chaque ligne est un exemple simplifié d’un individu **PointMapping** (pour la carte de partitions liste hello) ou **RangeMapping** (pour la carte de partitions de plage hello) objet.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-174">Each row is a simplified example of an individual **PointMapping** (for hello list shard map) or **RangeMapping** (for hello range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="dc7f0-175">Gestionnaire des cartes de partitions</span><span class="sxs-lookup"><span data-stu-id="dc7f0-175">Shard map manager</span></span>
<span data-ttu-id="dc7f0-176">Dans la bibliothèque cliente de hello, Gestionnaire de carte de partitions hello est une collection de cartes de partitions.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-176">In hello client library, hello shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="dc7f0-177">Hello les données gérées par un **ShardMapManager** instance est conservée dans trois emplacements :</span><span class="sxs-lookup"><span data-stu-id="dc7f0-177">hello data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="dc7f0-178">**Carte de partitions globales (GSM)**: vous spécifiez une tooserve de base de données en tant que référentiel hello pour les cartes de partitions et les mappages.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-178">**Global Shard Map (GSM)**: You specify a database tooserve as hello repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="dc7f0-179">Tables spéciales et les procédures stockées sont créées automatiquement des informations toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-179">Special tables and stored procedures are automatically created toomanage hello information.</span></span> <span data-ttu-id="dc7f0-180">Cela est généralement une petite base de données et accéder à la légère, et ne doit pas être utilisé pour d’autres besoins de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-180">This is typically a small database and lightly accessed, and it should not be used for other needs of hello application.</span></span> <span data-ttu-id="dc7f0-181">Hello tables se trouvent dans un schéma spécial appelé **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-181">hello tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="dc7f0-182">**Carte de partitions local (LSM)**: chaque base de données que vous spécifiez toobe une partition est modifié toocontain plusieurs petites tables et des procédures stockées spéciales qui contiennent et gérer des partitions de partitions carte informations toothat spécifique.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-182">**Local Shard Map (LSM)**: Every database that you specify toobe a shard is modified toocontain several small tables and special stored procedures that contain and manage shard map information specific toothat shard.</span></span> <span data-ttu-id="dc7f0-183">Ces informations sont redondantes avec informations hello Bonjour GSM, et il permet des informations de mappage des partitions hello application toovalidate mis en cache sans imposer aucune charge sur hello GSM ; application Hello utilise hello LSM toodetermine si un mappage de mise en cache est toujours valide.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-183">This information is redundant with hello information in hello GSM, and it allows hello application toovalidate cached shard map information without placing any load on hello GSM; hello application uses hello LSM toodetermine if a cached mapping is still valid.</span></span> <span data-ttu-id="dc7f0-184">Hello tables correspondante toohello LSM sur chaque partition sont également dans le schéma de hello **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-184">hello tables corresponding toohello LSM on each shard are also in hello schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="dc7f0-185">**Cache d’application** : chaque instance d’application accédant à un objet **ShardMapManager** conserve un cache local en mémoire de ses mappages.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="dc7f0-186">Elle stocke les informations de routage récupérées récemment.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="dc7f0-187">Construction d'un objet ShardMapManager</span><span class="sxs-lookup"><span data-stu-id="dc7f0-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="dc7f0-188">Un objet **ShardMapManager** est construit à l’aide d’un modèle [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) .</span><span class="sxs-lookup"><span data-stu-id="dc7f0-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="dc7f0-189">Hello  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  méthode utilise les informations d’identification (y compris le nom du serveur hello et le nom de base de données contenant hello GSM) sous forme de hello d’un  **ConnectionString** et retourne une instance d’un **ShardMapManager**.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-189">hello **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including hello server name and database name holding hello GSM) in hello form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="dc7f0-190">**Remarque :** hello **ShardMapManager** doit être instancié une seule fois par domaine d’application, dans le code d’initialisation hello pour une application.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-190">**Please Note:** hello **ShardMapManager** should be instantiated only once per app domain, within hello initialization code for an application.</span></span> <span data-ttu-id="dc7f0-191">La création d’instances supplémentaires de ShardMapManager Bonjour même appdomain, entraîne accrue de la mémoire et l’utilisation du processeur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-191">Creation of additional instances of ShardMapManager in hello same appdomain, will result in increased memory and CPU utilization of hello application.</span></span> <span data-ttu-id="dc7f0-192">Un **ShardMapManager** peut contenir n’importe quel nombre de cartes de partitions.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="dc7f0-193">Si une carte de partitions peut suffire à de nombreuses applications, il arrive que différents ensembles de bases de données soient utilisés pour différents schémas ou pour des objectifs uniques. Lorsque cela se produit, il est préférable d'employer plusieurs cartes de partitions.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="dc7f0-194">Dans ce code, une application essaie tooopen existant **ShardMapManager** avec hello [TryGetSqlShardMapManager méthode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc7f0-194">In this code, an application tries tooopen an existing **ShardMapManager** with hello [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="dc7f0-195">Si les objets représentant un Global **ShardMapManager** (GSM) ne le faites pas encore exister à l’intérieur de la base de données hello, bibliothèque cliente de hello crée les il à l’aide de hello [CreateSqlShardMapManager méthode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc7f0-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside hello database, hello client library creates them there using hello [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

<span data-ttu-id="dc7f0-196">En guise d’alternative, vous pouvez utiliser Powershell toocreate un nouveau gestionnaire de carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-196">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="dc7f0-197">Un exemple est disponible [ici](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="dc7f0-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="dc7f0-198">Obtenir un objet RangeShardMap ou ListShardMap</span><span class="sxs-lookup"><span data-stu-id="dc7f0-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="dc7f0-199">Après avoir créé une partition de gestionnaire de cartes, vous pouvez obtenir hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) ou [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) à l’aide de hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), ou hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) (méthode).</span><span class="sxs-lookup"><span data-stu-id="dc7f0-199">After creating a shard map manager, you can get hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="dc7f0-200">Informations d'identification de l'administration de carte de partitions</span><span class="sxs-lookup"><span data-stu-id="dc7f0-200">Shard map administration credentials</span></span>
<span data-ttu-id="dc7f0-201">Applications administrent et de manipulent des cartes de partitions sont différentes de celles qui utilisent des connexions de tooroute de cartes de partitions hello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-201">Applications that administer and manipulate shard maps are different from those that use hello shard maps tooroute connections.</span></span> 

<span data-ttu-id="dc7f0-202">mappe les partitions de tooadminister (ajouter ou modifier des partitions, les cartes de partitions, les mappages de partition, etc.), vous devez instancier hello **ShardMapManager** à l’aide de **en lecture/écriture d’informations d’identification disposant des droits sur les deux bases de données GSM de hello et sur chaque base de données qui sert d’une partition**.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-202">tooadminister shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate hello **ShardMapManager** using **credentials that have read/write privileges on both hello GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="dc7f0-203">informations d’identification Hello doivent autoriser pour l’écriture de tables hello dans les deux hello GSM et LSM comme informations de mappage de partitions sont entrées ou modifiées, ainsi que pour la création de tables LSM sur les nouvelles partitions.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-203">hello credentials must allow for writes against hello tables in both hello GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="dc7f0-204">Consultez [informations d’identification utilisées bibliothèque du client de base de données élastique tooaccess hello](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="dc7f0-204">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="dc7f0-205">Seules les métadonnées sont affectées</span><span class="sxs-lookup"><span data-stu-id="dc7f0-205">Only metadata affected</span></span>
<span data-ttu-id="dc7f0-206">Méthodes utilisées pour le remplissage ou de la modification de hello **ShardMapManager** données ne modifient pas les données utilisateur hello sont stockées dans des partitions hello eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-206">Methods used for populating or changing hello **ShardMapManager** data do not alter hello user data stored in hello shards themselves.</span></span> <span data-ttu-id="dc7f0-207">Par exemple, les méthodes telles que **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affectent uniquement les métadonnées de mappage partition hello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect hello shard map metadata only.</span></span> <span data-ttu-id="dc7f0-208">Ils ne pas suppriment, ajouter ou modifier les données utilisateur contenues dans les partitions hello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-208">They do not remove, add, or alter user data contained in hello shards.</span></span> <span data-ttu-id="dc7f0-209">Au lieu de cela, ces méthodes sont conçue toobe utilisé conjointement avec des opérations distinctes vous effectuez toocreate ou supprimez des bases de données réelles ou déplacer les lignes à partir d’une seule partition tooanother toorebalance un environnement partitionné.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-209">Instead, these methods are designed toobe used in conjunction with separate operations you perform toocreate or remove actual databases, or that move rows from one shard tooanother toorebalance a sharded environment.</span></span>  <span data-ttu-id="dc7f0-210">(hello **fusion et fractionnement** outil fourni avec les outils de base de données élastique se sert de ces API, ainsi que d’orchestrer le déplacement des données réelles entre les partitions.) Consultez [mise à l’échelle à l’aide d’outil de hello fractionnement de base de données élastique-fusion](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="dc7f0-210">(hello **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using hello Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="dc7f0-211">Exemple de remplissage d'une carte de partitions</span><span class="sxs-lookup"><span data-stu-id="dc7f0-211">Populating a shard map example</span></span>
<span data-ttu-id="dc7f0-212">Vous trouverez ci-dessous un exemple de séquence d’opérations toopopulate une carte de partitions spécifiques.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-212">An example sequence of operations toopopulate a specific shard map is shown below.</span></span> <span data-ttu-id="dc7f0-213">code de Hello procède comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc7f0-213">hello code performs these steps:</span></span> 

1. <span data-ttu-id="dc7f0-214">Une carte de partitions est créée dans un gestionnaire des cartes de partitions.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="dc7f0-215">métadonnées Hello pour deux partitions différentes sont ajoutée de carte de partitions toohello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-215">hello metadata for two different shards is added toohello shard map.</span></span> 
3. <span data-ttu-id="dc7f0-216">Une variété de mappages de la plage de clés sont ajoutées, et hello contenu globale de la carte de partitions hello est affichés.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-216">A variety of key range mappings are added, and hello overall contents of hello shard map are displayed.</span></span> 

<span data-ttu-id="dc7f0-217">code de Hello est écrite afin que la méthode hello peut être réexécutée si une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-217">hello code is written so that hello method can be rerun if an error occurs.</span></span> <span data-ttu-id="dc7f0-218">Chaque requête teste si une partition ou le mappage existe déjà, avant de tenter de toocreate il.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-218">Each request tests whether a shard or mapping already exists, before attempting toocreate it.</span></span> <span data-ttu-id="dc7f0-219">Hello code part du principe que les bases de données nommée **sample_shard_0**, **sample_shard_1** et **sample_shard_2** ont déjà été créés dans le serveur hello référencé par la chaîne **shardServer**.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-219">hello code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in hello server referenced by string **shardServer**.</span></span> 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

<span data-ttu-id="dc7f0-220">Comme alternative, vous pouvez utiliser PowerShell scripts tooachieve hello même résultat.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-220">As an alternative you can use PowerShell scripts tooachieve hello same result.</span></span> <span data-ttu-id="dc7f0-221">Certains exemples de hello exemple PowerShell sont disponibles [ici](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="dc7f0-221">Some of hello sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="dc7f0-222">Une fois que les cartes de partitions ont été remplies, les applications d’accès aux données peuvent être créées ou adapté toowork avec des cartes de hello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-222">Once shard maps have been populated, data access applications can be created or adapted toowork with hello maps.</span></span> <span data-ttu-id="dc7f0-223">Remplissage ou de la manipulation des mappages de hello ne doit pas avoir lieu à nouveau tant que **mise en page de mappage** doit toochange.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-223">Populating or manipulating hello maps need not occur again until **map layout** needs toochange.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="dc7f0-224">Routage dépendant des données</span><span class="sxs-lookup"><span data-stu-id="dc7f0-224">Data dependent routing</span></span>
<span data-ttu-id="dc7f0-225">Gestionnaire de cartes de partitions Hello est plus utilisé dans les applications qui nécessitent des opérations de données spécifiques à l’application de base de données connexions tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-225">hello shard map manager will be most used in applications that require database connections tooperform hello app-specific data operations.</span></span> <span data-ttu-id="dc7f0-226">Ces connexions doivent être associées avec la base de données correcte hello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-226">Those connections must be associated with hello correct database.</span></span> <span data-ttu-id="dc7f0-227">Cette opération est nommée **Routage dépendant des données**.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="dc7f0-228">Pour ces applications, instanciez un objet de gestionnaire de mappage de partitions à partir de la fabrique de hello à l’aide des informations d’identification qui ont un accès en lecture seule sur la base de données GSM hello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-228">For these applications, instantiate a shard map manager object from hello factory using credentials that have read-only access on hello GSM database.</span></span> <span data-ttu-id="dc7f0-229">Les requêtes individuelles pour les connexions ultérieures fournissent des informations d’identification nécessaires pour la connexion de base de données de la partition appropriée toohello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-229">Individual requests for later connections supply credentials necessary for connecting toohello appropriate shard database.</span></span>

<span data-ttu-id="dc7f0-230">Notez que ces applications (à l’aide de **ShardMapManager** ouverte avec des informations d’identification en lecture seule) ne peuvent pas apporter des modifications toohello mappages ou des mappages.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes toohello maps or mappings.</span></span> <span data-ttu-id="dc7f0-231">Pour cela, vous devez créer des applications d'administration ou des scripts PowerShell qui fourniront des informations d'identification dotées de privilèges élevés comme indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="dc7f0-232">Consultez [informations d’identification utilisées bibliothèque du client de base de données élastique tooaccess hello](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="dc7f0-232">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="dc7f0-233">Pour plus d'informations, consultez [Routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="dc7f0-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="dc7f0-234">Modification d'une carte de partitions</span><span class="sxs-lookup"><span data-stu-id="dc7f0-234">Modifying a shard map</span></span>
<span data-ttu-id="dc7f0-235">Vous disposez de plusieurs méthodes pour modifier une carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="dc7f0-236">Toutes les méthodes suivantes de hello modifier les métadonnées de hello décrivant les partitions hello et leurs mappages, mais ils ne modifient pas physiquement les données dans les partitions hello, ni qu’ils créer ou supprimer des bases de données réelles hello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-236">All of hello following methods modify hello metadata describing hello shards and their mappings, but they do not physically modify data within hello shards, nor do they create or delete hello actual databases.</span></span>  <span data-ttu-id="dc7f0-237">Certaines opérations hello sur la carte de partitions hello décrite ci-dessous peut-être toobe coordonné avec des actions administratives que déplacer physiquement les données ou qui ajouter et supprimer des bases de données servant de partitions.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-237">Some of hello operations on hello shard map described below may need toobe coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="dc7f0-238">Ces méthodes fonctionnent ensemble comme disponible pour la modification de blocs de construction hello hello distribution globale des données dans votre environnement de base de données partitionnée.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-238">These methods work together as hello building blocks available for modifying hello overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="dc7f0-239">tooadd ou supprimer des partitions : utilisez  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  et  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  Hello [Shardmap classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc7f0-239">tooadd or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of hello [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="dc7f0-240">Hello serveur et base de données qui représente la partition cible de hello doivent déjà exister pour tooexecute de ces opérations.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-240">hello server and database representing hello target shard must already exist for these operations tooexecute.</span></span> <span data-ttu-id="dc7f0-241">Ces méthodes n’ont pas leur impact sur hello bases de données elles-mêmes, uniquement sur les métadonnées dans la carte de partitions hello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-241">These methods do not have any impact on hello databases themselves, only on metadata in hello shard map.</span></span>
* <span data-ttu-id="dc7f0-242">toocreate ou supprimer des points ou des plages qui sont mappés toohello partitions : utilisez  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  de hello [RangeShardMapping classe](https://msdn.microsoft.com/library/azure/dn807318.aspx), et  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  Hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span><span class="sxs-lookup"><span data-stu-id="dc7f0-242">toocreate or remove points or ranges that are mapped toohello shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of hello [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="dc7f0-243">Nombre des différents points ou des plages peuvent être mappé toohello même ID de partition.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-243">Many different points or ranges can be mapped toohello same shard.</span></span> <span data-ttu-id="dc7f0-244">Ces méthodes affectent uniquement les métadonnées. Elles n’affectent pas les données qui peuvent déjà être présentes dans les partitions.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="dc7f0-245">Si les données doivent toobe supprimé de la base de données de hello dans toobe ordre cohérent avec **DeleteMapping** opérations, vous devez tooperform ces opérations séparément mais conjointement à l’aide de ces méthodes.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-245">If data needs toobe removed from hello database in order toobe consistent with **DeleteMapping** operations, you will need tooperform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="dc7f0-246">toosplit des plages existantes en deux ou fusionner les plages adjacentes en une seule : utilisez  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  et  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-246">toosplit existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="dc7f0-247">Notez que fractionne et fusionner les opérations **ne changent pas de clé de toowhich hello partition les valeurs sont mappées**.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-247">Note that split and merge operations **do not change hello shard toowhich key values are mapped**.</span></span> <span data-ttu-id="dc7f0-248">Un fractionnement s’arrête une plage existante en deux parties, mais laisse les deux en tant que toohello mappé même ID de partition.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-248">A split breaks an existing range into two parts, but leaves both as mapped toohello same shard.</span></span> <span data-ttu-id="dc7f0-249">Une fusion fonctionne sur les deux plages adjacentes qui sont déjà mappé toohello même partition, les fusionner dans une même plage.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-249">A merge operates on two adjacent ranges that are already mapped toohello same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="dc7f0-250">déplacement des points ou des plages eux-mêmes entre les partitions Hello doit toobe coordonnée à l’aide de **UpdateMapping** conjointement avec le déplacement des données réelles.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-250">hello movement of points or ranges themselves between shards needs toobe coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="dc7f0-251">Vous pouvez utiliser hello **fractionnement/fusion** les outils de service qui fait partie de la base de données élastique toocoordinate modifications du mappage de partitions avec le déplacement des données, lorsque le déplacement est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-251">You can use hello **Split/Merge** service that is part of elastic database tools toocoordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="dc7f0-252">toore-map (ou déplacement) points ou des plages toodifferent partitions : utilisez  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-252">toore-map (or move) individual points or ranges toodifferent shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="dc7f0-253">Étant donné que les données pouvant nécessiter toobe déplacé de tooanother une partition dans toobe ordre cohérent avec **UpdateMapping** opérations, vous devez tooperform mouvement séparément mais conjointement à l’aide de ces méthodes.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-253">Since data may need toobe moved from one shard tooanother in order toobe consistent with **UpdateMapping** operations, you will need tooperform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="dc7f0-254">mappages tootake en ligne et hors connexion : utilisez  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  et  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol hello état en ligne d’un mappage.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-254">tootake mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** toocontrol hello online state of a mapping.</span></span> 
  
    <span data-ttu-id="dc7f0-255">Certaines opérations des mappages de partitions sont autorisées uniquement lorsque l’état d’un mappage est « hors connexion », notamment **UpdateMapping** et **DeleteMapping**.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="dc7f0-256">Lorsqu'un mappage est hors connexion, une demande dépendant des données basée sur une clé incluse dans ce mappage renvoie une erreur.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="dc7f0-257">En outre, lorsqu’une plage est tout d’abord mises hors connexion, toutes les partitions toohello affectée de connexions sont alors supprimés automatiquement dans l’ordre tooprevent incomplète des résultats incohérents ou pour les requêtes à l’encontre de plages en cours de modification.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-257">In addition, when a range is first taken offline, all connections toohello affected shard are automatically killed in order tooprevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="dc7f0-258">Les mappages sont des objets immuables dans .Net.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="dc7f0-259">Toutes les méthodes de hello ci-dessus qui modifient les mappages d’invalident également tout toothem de références dans votre code.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-259">All of hello methods above that change mappings also invalidate any references toothem in your code.</span></span> <span data-ttu-id="dc7f0-260">toomake informatique des séquences de tooperform plus faciles d’opérations qui modifient l’état d’un mappage, toutes les méthodes hello qui modifient un mappage de retournent un nouveau mappage de référence, afin d’opérations peuvent être chaînées.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-260">toomake it easier tooperform sequences of operations that change a mapping’s state, all of hello methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="dc7f0-261">Par exemple, toodelete un mappage dans sm shardmap qui contient la clé de hello 25 existant, vous pouvez exécuter hello suivant :</span><span class="sxs-lookup"><span data-stu-id="dc7f0-261">For example, toodelete an existing mapping in shardmap sm that contains hello key 25, you can execute hello following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="dc7f0-262">Ajout d'une partition</span><span class="sxs-lookup"><span data-stu-id="dc7f0-262">Adding a shard</span></span>
<span data-ttu-id="dc7f0-263">Applications souvent besoin toosimply ajouter de nouvelles partitions toohandle données qui sont attendues de nouvelles clés ou des plages de clés pour une carte de partitions qui existe déjà.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-263">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="dc7f0-264">Par exemple, une application partitionnée par ID client peut-être tooprovision une nouvelle partition pour un nouveau client, ou mensuelle partitionnée de données peut-être une nouvelle partition configurée avant le début de hello de chaque nouveau mois.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-264">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="dc7f0-265">Si hello nouvelle plage de valeurs de clé n’est pas déjà partie d’un mappage existant et aucun déplacement de données est nécessaire, il est la nouvelle partition de hello tooadd très simple et associer la nouvelle clé de hello ou partition toothat de plage.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-265">If hello new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> <span data-ttu-id="dc7f0-266">Pour plus d’informations sur l’ajout de nouvelles partitions, consultez [Ajout d’une nouvelle partition](sql-database-elastic-scale-add-a-shard.md).</span><span class="sxs-lookup"><span data-stu-id="dc7f0-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="dc7f0-267">Toutefois, pour les scénarios qui requièrent le déplacement des données, outil de fusion et fractionnement hello est tooorchestrate nécessaires hello déplacement des données entre les partitions en association avec les mises à jour de partition nécessaire hello.</span><span class="sxs-lookup"><span data-stu-id="dc7f0-267">For scenarios that require data movement, however, hello split-merge tool is needed tooorchestrate hello data movement between shards in combination with hello necessary shard map updates.</span></span> <span data-ttu-id="dc7f0-268">Pour plus d’informations sur l’utilisation de hello yool de fusion et fractionnement, consultez [vue d’ensemble de la fusion de fractionnement](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="dc7f0-268">For details on using hello split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
