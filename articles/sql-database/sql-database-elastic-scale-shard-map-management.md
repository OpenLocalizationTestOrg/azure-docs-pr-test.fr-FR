---
title: "Montée en puissance parallèle d’une base de données SQL Azure | Microsoft Docs"
description: "Utilisation de ShardMapManager, la bibliothèque cliente de base de données élastique"
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
ms.openlocfilehash: f626cf417d8b3f1761f3c900d49039b3ff83b093
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-out-databases-with-the-shard-map-manager"></a><span data-ttu-id="180a2-103">Monter en charge les bases de données avec le Gestionnaire de cartes de partitions</span><span class="sxs-lookup"><span data-stu-id="180a2-103">Scale out databases with the shard map manager</span></span>
<span data-ttu-id="180a2-104">Pour monter facilement en charge les bases de données sur SQL Azure, utilisez un Gestionnaire de cartes de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-104">To easily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="180a2-105">Le Gestionnaire de cartes de partitions est une base de données spéciale qui gère les informations de mappage global sur toutes les partitions (bases de données) dans un ensemble de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-105">The shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="180a2-106">Les métadonnées permettent à une application de se connecter à la base de données qui convient en fonction de la valeur de la **clé de partitionnement**.</span><span class="sxs-lookup"><span data-stu-id="180a2-106">The metadata allows an application to connect to the correct database based upon the value of the **sharding key**.</span></span> <span data-ttu-id="180a2-107">En outre, chaque partition de l’ensemble contient les cartes qui suivent les données de partitions locales (appelées **shardlets**).</span><span class="sxs-lookup"><span data-stu-id="180a2-107">In addition, every shard in the set contains maps that track the local shard data (known as **shardlets**).</span></span> 

![Gestion des cartes de partitions](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="180a2-109">Il est essentiel de comprendre comment ces mappages sont construits pour la gestion du mappage de partition.</span><span class="sxs-lookup"><span data-stu-id="180a2-109">Understanding how these maps are constructed is essential to shard map management.</span></span> <span data-ttu-id="180a2-110">Utilisez pour cela la [classe ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) située dans la [bibliothèque cliente de bases de données élastiques](sql-database-elastic-database-client-library.md) pour gérer les cartes de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-110">This is done using the [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in the [Elastic Database client library](sql-database-elastic-database-client-library.md) to manage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="180a2-111">Cartes de partitions et mappages de partitions</span><span class="sxs-lookup"><span data-stu-id="180a2-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="180a2-112">Pour chaque partition, vous devez sélectionner le type de carte de partitions à créer.</span><span class="sxs-lookup"><span data-stu-id="180a2-112">For each shard, you must select the type of shard map to create.</span></span> <span data-ttu-id="180a2-113">Votre choix dépend de l’architecture de la base de données :</span><span class="sxs-lookup"><span data-stu-id="180a2-113">The choice depends on the database architecture:</span></span> 

1. <span data-ttu-id="180a2-114">Client unique par base de données</span><span class="sxs-lookup"><span data-stu-id="180a2-114">Single tenant per database</span></span>  
2. <span data-ttu-id="180a2-115">Plusieurs clients par base de données (deux types) :</span><span class="sxs-lookup"><span data-stu-id="180a2-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="180a2-116">Mappage de liste</span><span class="sxs-lookup"><span data-stu-id="180a2-116">List mapping</span></span>
   2. <span data-ttu-id="180a2-117">Mappage de plage</span><span class="sxs-lookup"><span data-stu-id="180a2-117">Range mapping</span></span>

<span data-ttu-id="180a2-118">Pour un modèle de client unique, créez une carte de partitions de **mappage de liste** .</span><span class="sxs-lookup"><span data-stu-id="180a2-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="180a2-119">Le modèle à un seul client attribue une base de données par client.</span><span class="sxs-lookup"><span data-stu-id="180a2-119">The single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="180a2-120">Il s’agit d’un modèle efficace pour les développeurs SaaS, car il simplifie la gestion.</span><span class="sxs-lookup"><span data-stu-id="180a2-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Mappage de liste][1]

<span data-ttu-id="180a2-122">Le modèle mutualisé affecte plusieurs clients à une seule base de données (et vous pouvez distribuer des groupes de clients sur plusieurs bases de données).</span><span class="sxs-lookup"><span data-stu-id="180a2-122">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="180a2-123">Utilisez ce modèle lorsque vous pensez que chaque client va avoir de faibles besoins en termes de données.</span><span class="sxs-lookup"><span data-stu-id="180a2-123">Use this model when you expect each tenant to have small data needs.</span></span> <span data-ttu-id="180a2-124">Dans ce modèle, nous attribuons une plage de clients à une base de données à l’aide du **mappage de plage**.</span><span class="sxs-lookup"><span data-stu-id="180a2-124">In this model, we assign a range of tenants to a database using **range mapping**.</span></span> 

![Mappage de plage][2]

<span data-ttu-id="180a2-126">Vous pouvez également implémenter un modèle de base de données mutualisée à l’aide d’un *mappage de liste* pour affecter plusieurs clients à une base de données unique.</span><span class="sxs-lookup"><span data-stu-id="180a2-126">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span></span> <span data-ttu-id="180a2-127">Par exemple, DB1 est utilisée pour stocker les informations d’id client 1 et 5 et DB2 stocke les données pour les clients 7 et 10.</span><span class="sxs-lookup"><span data-stu-id="180a2-127">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Plusieurs clients sur une base de données unique][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="180a2-129">Types .Net pris en charge pour les clés de partitionnement</span><span class="sxs-lookup"><span data-stu-id="180a2-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="180a2-130">L'infrastructure élastique prend en charge les types .Net Framework suivants en tant que clés de partitionnement :</span><span class="sxs-lookup"><span data-stu-id="180a2-130">Elastic Scale support the following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="180a2-131">integer</span><span class="sxs-lookup"><span data-stu-id="180a2-131">integer</span></span>
* <span data-ttu-id="180a2-132">long</span><span class="sxs-lookup"><span data-stu-id="180a2-132">long</span></span>
* <span data-ttu-id="180a2-133">guid</span><span class="sxs-lookup"><span data-stu-id="180a2-133">guid</span></span>
* <span data-ttu-id="180a2-134">byte[]</span><span class="sxs-lookup"><span data-stu-id="180a2-134">byte[]</span></span>  
* <span data-ttu-id="180a2-135">datetime</span><span class="sxs-lookup"><span data-stu-id="180a2-135">datetime</span></span>
* <span data-ttu-id="180a2-136">timespan</span><span class="sxs-lookup"><span data-stu-id="180a2-136">timespan</span></span>
* <span data-ttu-id="180a2-137">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="180a2-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="180a2-138">Liste et cartes de partitions de plage</span><span class="sxs-lookup"><span data-stu-id="180a2-138">List and range shard maps</span></span>
<span data-ttu-id="180a2-139">Vous pouvez construire des cartes de partition en utilisant des **listes de valeurs de clés de partitionnement individuelles** ou des **plages de valeurs de clés de partitionnement**.</span><span class="sxs-lookup"><span data-stu-id="180a2-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="180a2-140">Cartes de partition de liste</span><span class="sxs-lookup"><span data-stu-id="180a2-140">List shard maps</span></span>
<span data-ttu-id="180a2-141">Les **partitions** contiennent des **shardlets** (micro-partitions) et le mappage de ces shardlets en partitions est tenu à jour par une carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-141">**Shards** contain **shardlets** and the mapping of shardlets to shards is maintained by a shard map.</span></span> <span data-ttu-id="180a2-142">Une **carte de partitions de liste** est une association entre les valeurs de clés individuelles identifiant les shardlets et les bases de données qui servent de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-142">A **list shard map** is an association between the individual key values that identify the shardlets and the databases that serve as shards.</span></span>  <span data-ttu-id="180a2-143">**mappages de liste** sont explicites et plusieurs valeurs de clés peuvent être mappées à la même base de données.</span><span class="sxs-lookup"><span data-stu-id="180a2-143">**List mappings** are explicit and different key values can be mapped to the same database.</span></span> <span data-ttu-id="180a2-144">Par exemple, la clé 1 est mappée à la base de données A et les valeurs de clés 3 et 6 font toutes deux référence à la base de données B.</span><span class="sxs-lookup"><span data-stu-id="180a2-144">For example, key 1 maps to Database A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="180a2-145">Clé</span><span class="sxs-lookup"><span data-stu-id="180a2-145">Key</span></span> | <span data-ttu-id="180a2-146">Emplacement de partition</span><span class="sxs-lookup"><span data-stu-id="180a2-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="180a2-147">1</span><span class="sxs-lookup"><span data-stu-id="180a2-147">1</span></span> |<span data-ttu-id="180a2-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="180a2-148">Database_A</span></span> |
| <span data-ttu-id="180a2-149">3</span><span class="sxs-lookup"><span data-stu-id="180a2-149">3</span></span> |<span data-ttu-id="180a2-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="180a2-150">Database_B</span></span> |
| <span data-ttu-id="180a2-151">4</span><span class="sxs-lookup"><span data-stu-id="180a2-151">4</span></span> |<span data-ttu-id="180a2-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="180a2-152">Database_C</span></span> |
| <span data-ttu-id="180a2-153">6</span><span class="sxs-lookup"><span data-stu-id="180a2-153">6</span></span> |<span data-ttu-id="180a2-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="180a2-154">Database_B</span></span> |
| <span data-ttu-id="180a2-155">...</span><span class="sxs-lookup"><span data-stu-id="180a2-155">...</span></span> |<span data-ttu-id="180a2-156">...</span><span class="sxs-lookup"><span data-stu-id="180a2-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="180a2-157">Cartes de partitions de plage</span><span class="sxs-lookup"><span data-stu-id="180a2-157">Range shard maps</span></span>
<span data-ttu-id="180a2-158">Dans une **carte de partitions de plage**, la plage de clé est décrite par une paire **[valeur inférieure, valeur supérieure)**, où la *valeur inférieure* correspond à la clé minimale de la plage, tandis que la *valeur supérieure* correspond à la première valeur supérieure à la plage.</span><span class="sxs-lookup"><span data-stu-id="180a2-158">In a **range shard map**, the key range is described by a pair **[Low Value, High Value)** where the *Low Value* is the minimum key in the range, and the *High Value* is the first value higher than the range.</span></span> 

<span data-ttu-id="180a2-159">Par exemple, **[0, 100)** inclut tous les entiers égaux ou supérieurs à 0 et inférieurs à 100.</span><span class="sxs-lookup"><span data-stu-id="180a2-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="180a2-160">Notez que plusieurs plages peuvent pointer vers la même base de données et que les plages disjointes sont prises en charge (par exemple, [100,200) et [400,600) pointent vers la base de données C dans l’exemple ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="180a2-160">Note that multiple ranges can point to the same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point to Database C in the example below.)</span></span>

| <span data-ttu-id="180a2-161">Clé</span><span class="sxs-lookup"><span data-stu-id="180a2-161">Key</span></span> | <span data-ttu-id="180a2-162">Emplacement de partition</span><span class="sxs-lookup"><span data-stu-id="180a2-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="180a2-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="180a2-163">[1,50)</span></span> |<span data-ttu-id="180a2-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="180a2-164">Database_A</span></span> |
| <span data-ttu-id="180a2-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="180a2-165">[50,100)</span></span> |<span data-ttu-id="180a2-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="180a2-166">Database_B</span></span> |
| <span data-ttu-id="180a2-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="180a2-167">[100,200)</span></span> |<span data-ttu-id="180a2-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="180a2-168">Database_C</span></span> |
| <span data-ttu-id="180a2-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="180a2-169">[400,600)</span></span> |<span data-ttu-id="180a2-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="180a2-170">Database_C</span></span> |
| <span data-ttu-id="180a2-171">...</span><span class="sxs-lookup"><span data-stu-id="180a2-171">...</span></span> |<span data-ttu-id="180a2-172">...</span><span class="sxs-lookup"><span data-stu-id="180a2-172">...</span></span> |

<span data-ttu-id="180a2-173">Chacune des tables présentées ci-dessus correspond à un exemple conceptuel d'un objet **ShardMap** .</span><span class="sxs-lookup"><span data-stu-id="180a2-173">Each of the tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="180a2-174">Chaque ligne correspond à un exemple simplifié d’un objet **PointMapping** (pour la carte de partitions de liste) ou **RangeMapping** (pour la carte de partitions de plage).</span><span class="sxs-lookup"><span data-stu-id="180a2-174">Each row is a simplified example of an individual **PointMapping** (for the list shard map) or **RangeMapping** (for the range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="180a2-175">Gestionnaire des cartes de partitions</span><span class="sxs-lookup"><span data-stu-id="180a2-175">Shard map manager</span></span>
<span data-ttu-id="180a2-176">Dans la bibliothèque cliente, le gestionnaire des cartes de partitions correspond à une collection de cartes de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-176">In the client library, the shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="180a2-177">Les données gérées par une instance **ShardMapManager** sont conservées à trois emplacements :</span><span class="sxs-lookup"><span data-stu-id="180a2-177">The data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="180a2-178">**Carte de partitions globale (GSM)**: vous spécifiez une base de données en tant que référentiel pour l’ensemble de ses cartes et mappages de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-178">**Global Shard Map (GSM)**: You specify a database to serve as the repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="180a2-179">Les tables spéciales et les procédures stockées sont automatiquement créées pour gérer les informations.</span><span class="sxs-lookup"><span data-stu-id="180a2-179">Special tables and stored procedures are automatically created to manage the information.</span></span> <span data-ttu-id="180a2-180">Il s'agit généralement d'une petite base de données à laquelle vous pouvez accéder rapidement, et elle ne doit pas être utilisée pour d'autres besoins de l'application.</span><span class="sxs-lookup"><span data-stu-id="180a2-180">This is typically a small database and lightly accessed, and it should not be used for other needs of the application.</span></span> <span data-ttu-id="180a2-181">Les tables sont stockées dans un schéma spécifique nommé **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="180a2-181">The tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="180a2-182">**Carte de partitions locale (LSM)** : chaque base de données que vous définissez en tant que partition est modifiée pour contenir des petites tables et des procédures stockées spécifiques qui renferment et gèrent les informations de carte de partitions propres à cette partition.</span><span class="sxs-lookup"><span data-stu-id="180a2-182">**Local Shard Map (LSM)**: Every database that you specify to be a shard is modified to contain several small tables and special stored procedures that contain and manage shard map information specific to that shard.</span></span> <span data-ttu-id="180a2-183">Ces informations sont redondantes avec les informations contenues dans la GSM et elles permettent aux applications de valider les informations de carte de partitions mises en cache sans placer aucune charge sur la GSM. L'application utilise la LSM pour déterminer la validité d'un mappage mis en cache.</span><span class="sxs-lookup"><span data-stu-id="180a2-183">This information is redundant with the information in the GSM, and it allows the application to validate cached shard map information without placing any load on the GSM; the application uses the LSM to determine if a cached mapping is still valid.</span></span> <span data-ttu-id="180a2-184">Les tables correspondant à la LSM de chaque partition sont également stockées dans le schéma **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="180a2-184">The tables corresponding to the LSM on each shard are also in the schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="180a2-185">**Cache d’application** : chaque instance d’application accédant à un objet **ShardMapManager** conserve un cache local en mémoire de ses mappages.</span><span class="sxs-lookup"><span data-stu-id="180a2-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="180a2-186">Elle stocke les informations de routage récupérées récemment.</span><span class="sxs-lookup"><span data-stu-id="180a2-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="180a2-187">Construction d'un objet ShardMapManager</span><span class="sxs-lookup"><span data-stu-id="180a2-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="180a2-188">Un objet **ShardMapManager** est construit à l’aide d’un modèle [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) .</span><span class="sxs-lookup"><span data-stu-id="180a2-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="180a2-189">La méthode **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** récupère des informations d’identification (incluant le nom du serveur et le nom de base de données contenant la GSM) sous la forme d’un objet **ConnectionString** et renvoie l’instance d’un objet **ShardMapManager**.</span><span class="sxs-lookup"><span data-stu-id="180a2-189">The **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including the server name and database name holding the GSM) in the form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="180a2-190">**Remarque** : l’objet **ShardMapManager** doit être instancié une seule fois par domaine d’application, dans le code d’initialisation d’une application.</span><span class="sxs-lookup"><span data-stu-id="180a2-190">**Please Note:** The **ShardMapManager** should be instantiated only once per app domain, within the initialization code for an application.</span></span> <span data-ttu-id="180a2-191">La création d’instances supplémentaires de ShardMapManager dans le même appdomain entraîne l’augmentation de l’utilisation de la mémoire et du processeur de l’application.</span><span class="sxs-lookup"><span data-stu-id="180a2-191">Creation of additional instances of ShardMapManager in the same appdomain, will result in increased memory and CPU utilization of the application.</span></span> <span data-ttu-id="180a2-192">Un **ShardMapManager** peut contenir n’importe quel nombre de cartes de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="180a2-193">Si une carte de partitions peut suffire à de nombreuses applications, il arrive que différents ensembles de bases de données soient utilisés pour différents schémas ou pour des objectifs uniques. Lorsque cela se produit, il est préférable d'employer plusieurs cartes de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="180a2-194">Dans ce code, une application tente d’ouvrir un objet **ShardMapManager** existant avec la [méthode TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="180a2-194">In this code, an application tries to open an existing **ShardMapManager** with the [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="180a2-195">Si des objets représentant un objet **ShardMapManager** global (GSM) n’existent pas encore dans la base de données, ils y sont créés par la bibliothèque cliente à l’aide de la [méthode CreateSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="180a2-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside the database, the client library creates them there using the [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try to get a reference to the Shard Map Manager 
     // via the Shard Map Manager database.  
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
        // Create the Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // The connectionString contains server name, database name, and admin credentials 
        // for privileges on both the GSM and the shards themselves.
    } 

<span data-ttu-id="180a2-196">Comme alternative, vous pouvez utiliser PowerShell pour créer un gestionnaire de cartes de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-196">As an alternative, you can use Powershell to create a new Shard Map Manager.</span></span> <span data-ttu-id="180a2-197">Un exemple est disponible [ici](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="180a2-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="180a2-198">Obtenir un objet RangeShardMap ou ListShardMap</span><span class="sxs-lookup"><span data-stu-id="180a2-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="180a2-199">Après avoir créé un Gestionnaire de cartes de partition, vous pouvez obtenir l’objet [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) ou [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) à l’aide de la méthode [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx) ou [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="180a2-199">After creating a shard map manager, you can get the [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using the [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), the [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or the [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with the specified name, or gets the Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try to get a reference to the Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // The Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="180a2-200">Informations d'identification de l'administration de carte de partitions</span><span class="sxs-lookup"><span data-stu-id="180a2-200">Shard map administration credentials</span></span>
<span data-ttu-id="180a2-201">Les applications d'administration et de manipulation de cartes de partitions diffèrent des applications acheminant des connexions grâce aux cartes de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-201">Applications that administer and manipulate shard maps are different from those that use the shard maps to route connections.</span></span> 

<span data-ttu-id="180a2-202">Pour administrer des cartes de partitions (ajouter ou modifier des partitions, cartes de partitions, mappages de partitions, etc.), vous devez instancier l’objet **ShardMapManager** en utilisant des **informations d’identification dotées de privilèges de lecture/écriture sur la base de données GSM et sur chaque base de données servant de partition**.</span><span class="sxs-lookup"><span data-stu-id="180a2-202">To administer shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate the **ShardMapManager** using **credentials that have read/write privileges on both the GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="180a2-203">Les informations d'identification doivent autoriser l'écriture sur les tables dans la CPG et la CPL à chaque saisie ou modification des informations de carte de partitions, ainsi qu'à chaque création d'une table CPL sur une nouvelle partition.</span><span class="sxs-lookup"><span data-stu-id="180a2-203">The credentials must allow for writes against the tables in both the GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="180a2-204">Consultez [Informations d’identification utilisées pour accéder à la bibliothèque cliente de la base de données élastique](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="180a2-204">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="180a2-205">Seules les métadonnées sont affectées</span><span class="sxs-lookup"><span data-stu-id="180a2-205">Only metadata affected</span></span>
<span data-ttu-id="180a2-206">Les méthodes utilisées pour remplir ou modifier les données d'un objet **ShardMapManager** n'affectent pas les données utilisateur stockées dans les partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-206">Methods used for populating or changing the **ShardMapManager** data do not alter the user data stored in the shards themselves.</span></span> <span data-ttu-id="180a2-207">Par exemple, des méthodes telles que **CreateShard**, **DeleteShard** ou **UpdateMapping** affectent uniquement les métadonnées de carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect the shard map metadata only.</span></span> <span data-ttu-id="180a2-208">affectent uniquement les métadonnées de carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-208">They do not remove, add, or alter user data contained in the shards.</span></span> <span data-ttu-id="180a2-209">Elles ne suppriment pas, n’ajoutent pas ou ni ne modifient les données utilisateur contenues dans les partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-209">Instead, these methods are designed to be used in conjunction with separate operations you perform to create or remove actual databases, or that move rows from one shard to another to rebalance a sharded environment.</span></span>  <span data-ttu-id="180a2-210">(L’outil de **fractionnement/fusion** inclus avec les outils de base de données élastique utilise ces applications avec l’orchestration des mouvements de données réels entre les partitions.) Consultez [Mise à l’échelle utilisant l’outil de fractionnement et de fusion de bases de données élastiques](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="180a2-210">(The **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using the Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="180a2-211">Exemple de remplissage d'une carte de partitions</span><span class="sxs-lookup"><span data-stu-id="180a2-211">Populating a shard map example</span></span>
<span data-ttu-id="180a2-212">Vous trouverez ci-dessous un exemple de séquence d'opérations pour remplir une carte de partitions spécifique.</span><span class="sxs-lookup"><span data-stu-id="180a2-212">An example sequence of operations to populate a specific shard map is shown below.</span></span> <span data-ttu-id="180a2-213">Le code suit cette procédure :</span><span class="sxs-lookup"><span data-stu-id="180a2-213">The code performs these steps:</span></span> 

1. <span data-ttu-id="180a2-214">Une carte de partitions est créée dans un gestionnaire des cartes de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="180a2-215">Les métadonnées de deux partitions différentes sont ajoutées à la carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-215">The metadata for two different shards is added to the shard map.</span></span> 
3. <span data-ttu-id="180a2-216">Différents mappages de plages de clés sont ajoutés et le contenu global de la carte de partitions s’affiche.</span><span class="sxs-lookup"><span data-stu-id="180a2-216">A variety of key range mappings are added, and the overall contents of the shard map are displayed.</span></span> 

<span data-ttu-id="180a2-217">Le code est écrit de sorte que la méthode peut être réexécutée si une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="180a2-217">The code is written so that the method can be rerun if an error occurs.</span></span> <span data-ttu-id="180a2-218">Chaque requête vérifie si une partition ou un mappage existe déjà, avant d'essayer de le créer.</span><span class="sxs-lookup"><span data-stu-id="180a2-218">Each request tests whether a shard or mapping already exists, before attempting to create it.</span></span> <span data-ttu-id="180a2-219">Le code part du principe que les bases de données nommées **sample_shard_0**, **sample_shard_1** et **sample_shard_2** ont déjà été créées dans le serveur référencé par la chaîne **shardServer**.</span><span class="sxs-lookup"><span data-stu-id="180a2-219">The code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in the server referenced by string **shardServer**.</span></span> 

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

            // List the shards and mappings 
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

<span data-ttu-id="180a2-220">En guise d'alternative, vous pouvez utiliser des scripts PowerShell pour obtenir le même résultat.</span><span class="sxs-lookup"><span data-stu-id="180a2-220">As an alternative you can use PowerShell scripts to achieve the same result.</span></span> <span data-ttu-id="180a2-221">Certains exemples d’extraits de codes PowerShell sont disponibles [ici](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="180a2-221">Some of the sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="180a2-222">Une fois les cartes de partitions remplies, vous pouvez créer ou adapter des applications pour accéder aux données, afin d'utiliser les cartes.</span><span class="sxs-lookup"><span data-stu-id="180a2-222">Once shard maps have been populated, data access applications can be created or adapted to work with the maps.</span></span> <span data-ttu-id="180a2-223">Le remplissage ou la manipulation des cartes ne doit pas survenir tant que la **disposition de la carte** n'a pas été modifiée.</span><span class="sxs-lookup"><span data-stu-id="180a2-223">Populating or manipulating the maps need not occur again until **map layout** needs to change.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="180a2-224">Routage dépendant des données</span><span class="sxs-lookup"><span data-stu-id="180a2-224">Data dependent routing</span></span>
<span data-ttu-id="180a2-225">Le gestionnaire des cartes de partitions est principalement utilisé par des applications devant se connecter à une base de données pour exploiter leurs données.</span><span class="sxs-lookup"><span data-stu-id="180a2-225">The shard map manager will be most used in applications that require database connections to perform the app-specific data operations.</span></span> <span data-ttu-id="180a2-226">Ces connexions doivent être associées à la base de données correcte.</span><span class="sxs-lookup"><span data-stu-id="180a2-226">Those connections must be associated with the correct database.</span></span> <span data-ttu-id="180a2-227">Cette opération est nommée **Routage dépendant des données**.</span><span class="sxs-lookup"><span data-stu-id="180a2-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="180a2-228">Pour ces applications, instanciez un objet Gestionnaire des cartes de partitions à partir de la fabrique à l'aide des informations d'identification ayant un accès en lecture seule sur la base de données CPG.</span><span class="sxs-lookup"><span data-stu-id="180a2-228">For these applications, instantiate a shard map manager object from the factory using credentials that have read-only access on the GSM database.</span></span> <span data-ttu-id="180a2-229">Les requêtes de connexion individuelles ultérieures fournissent les informations d'identification requises pour la connexion à la base de données de partitions adéquate.</span><span class="sxs-lookup"><span data-stu-id="180a2-229">Individual requests for later connections supply credentials necessary for connecting to the appropriate shard database.</span></span>

<span data-ttu-id="180a2-230">Ces applications (utilisant **ShardMapManager** ouvert avec des informations d’identification en lecture seule) ne peuvent pas modifier les cartes ni les mappages.</span><span class="sxs-lookup"><span data-stu-id="180a2-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes to the maps or mappings.</span></span> <span data-ttu-id="180a2-231">Pour cela, vous devez créer des applications d'administration ou des scripts PowerShell qui fourniront des informations d'identification dotées de privilèges élevés comme indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="180a2-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="180a2-232">Consultez [Informations d’identification utilisées pour accéder à la bibliothèque cliente de la base de données élastique](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="180a2-232">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="180a2-233">Pour plus d'informations, consultez [Routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="180a2-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="180a2-234">Modification d'une carte de partitions</span><span class="sxs-lookup"><span data-stu-id="180a2-234">Modifying a shard map</span></span>
<span data-ttu-id="180a2-235">Vous disposez de plusieurs méthodes pour modifier une carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="180a2-236">Toutes les méthodes suivantes modifient les métadonnées décrivant les partitions et leurs mappages, mais elles ne modifient pas physiquement les données dans les partitions et ne créent ni ne suppriment les bases de données réelles.</span><span class="sxs-lookup"><span data-stu-id="180a2-236">All of the following methods modify the metadata describing the shards and their mappings, but they do not physically modify data within the shards, nor do they create or delete the actual databases.</span></span>  <span data-ttu-id="180a2-237">Il est possible que certaines opérations de carte de partitions décrites ci-dessous requièrent une coordination à l’aide d’actions d’administration qui déplacent physiquement les données ou qui ajoutent et suppriment des bases de données servant de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-237">Some of the operations on the shard map described below may need to be coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="180a2-238">Ces méthodes fonctionnent ensemble en tant que blocs de construction disponibles pour la modification de la distribution globale des données dans votre environnement de base de données partitionnée.</span><span class="sxs-lookup"><span data-stu-id="180a2-238">These methods work together as the building blocks available for modifying the overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="180a2-239">Pour ajouter ou supprimer des partitions : utilisez **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** et **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** de la [classe Shardmap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="180a2-239">To add or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of the [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="180a2-240">Le serveur et la base de données représentant la partition cible doivent déjà exister pour pouvoir exécuter ces opérations.</span><span class="sxs-lookup"><span data-stu-id="180a2-240">The server and database representing the target shard must already exist for these operations to execute.</span></span> <span data-ttu-id="180a2-241">Ces méthodes n’ont pas d’incidence sur les bases de données elles-mêmes. Elles affectent uniquement les métadonnées de la carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-241">These methods do not have any impact on the databases themselves, only on metadata in the shard map.</span></span>
* <span data-ttu-id="180a2-242">Pour créer ou supprimer des points ou des plages mappés sur les partitions : utilisez **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** de la [classe RangeShardMapping](https://msdn.microsoft.com/library/azure/dn807318.aspx), et **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** de [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span><span class="sxs-lookup"><span data-stu-id="180a2-242">To create or remove points or ranges that are mapped to the shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of the [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of the [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="180a2-243">Vous pouvez mapper différents points ou plages vers la même partition.</span><span class="sxs-lookup"><span data-stu-id="180a2-243">Many different points or ranges can be mapped to the same shard.</span></span> <span data-ttu-id="180a2-244">Ces méthodes affectent uniquement les métadonnées. Elles n’affectent pas les données qui peuvent déjà être présentes dans les partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="180a2-245">Si vous devez supprimer des données de la base de données par souci de cohérence avec les opérations **DeleteMapping**, vous devez effectuer ces opérations séparément, mais en utilisant ces méthodes.</span><span class="sxs-lookup"><span data-stu-id="180a2-245">If data needs to be removed from the database in order to be consistent with **DeleteMapping** operations, you will need to perform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="180a2-246">Pour diviser des plages existantes en deux ou pour fusionner des plages adjacentes en une seule : utilisez **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** et **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="180a2-246">To split existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="180a2-247">Notez que les opérations de fractionnement/fusion **ne changent pas la partition sur laquelle les valeurs de clé sont mappées**.</span><span class="sxs-lookup"><span data-stu-id="180a2-247">Note that split and merge operations **do not change the shard to which key values are mapped**.</span></span> <span data-ttu-id="180a2-248">Un fractionnement divise une plage existante en deux parties, qui sont chacune mappées vers la même partition.</span><span class="sxs-lookup"><span data-stu-id="180a2-248">A split breaks an existing range into two parts, but leaves both as mapped to the same shard.</span></span> <span data-ttu-id="180a2-249">Une fusion s'applique sur deux plages adjacentes qui sont déjà mappées vers la même partition, afin d'en faire une plage unique.</span><span class="sxs-lookup"><span data-stu-id="180a2-249">A merge operates on two adjacent ranges that are already mapped to the same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="180a2-250">Le déplacement des points ou des plages entre des partitions doit être coordonné à l’aide de l’objet **UpdateMapping** , conjointement au déplacement des données réelles.</span><span class="sxs-lookup"><span data-stu-id="180a2-250">The movement of points or ranges themselves between shards needs to be coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="180a2-251">Vous pouvez utiliser le service de **fractionnement/fusion** , compris dans les outils de base de données élastique, pour coordonner les modifications de la carte de partitions avec le mouvement des données, lorsque celui-ci est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="180a2-251">You can use the **Split/Merge** service that is part of elastic database tools to coordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="180a2-252">Pour remapper (ou déplacer) des points ou des plages vers différentes partitions : utilisez **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="180a2-252">To re-map (or move) individual points or ranges to different shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="180a2-253">Comme il est possible que les données soient déplacées d'une partition à l'autre afin d'être cohérentes avec les opérations **UpdateMapping** , vous devez effectuer ces déplacements séparément tout en utilisant ces méthodes.</span><span class="sxs-lookup"><span data-stu-id="180a2-253">Since data may need to be moved from one shard to another in order to be consistent with **UpdateMapping** operations, you will need to perform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="180a2-254">Pour effectuer des mappages en ligne et hors connexion : utilisez **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** et **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** pour contrôler l’état en ligne d’un mappage.</span><span class="sxs-lookup"><span data-stu-id="180a2-254">To take mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** to control the online state of a mapping.</span></span> 
  
    <span data-ttu-id="180a2-255">Certaines opérations des mappages de partitions sont autorisées uniquement lorsque l’état d’un mappage est « hors connexion », notamment **UpdateMapping** et **DeleteMapping**.</span><span class="sxs-lookup"><span data-stu-id="180a2-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="180a2-256">Lorsqu'un mappage est hors connexion, une demande dépendant des données basée sur une clé incluse dans ce mappage renvoie une erreur.</span><span class="sxs-lookup"><span data-stu-id="180a2-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="180a2-257">En outre, lorsqu'une plage est d'abord mise hors connexion, toutes les connexions vers la partition concernée sont supprimées automatiquement afin d'éviter des résultats incohérents ou incomplets pour les requêtes émises vers les plages en cours de modification.</span><span class="sxs-lookup"><span data-stu-id="180a2-257">In addition, when a range is first taken offline, all connections to the affected shard are automatically killed in order to prevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="180a2-258">Les mappages sont des objets immuables dans .Net.</span><span class="sxs-lookup"><span data-stu-id="180a2-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="180a2-259">Toutes les méthodes ci-dessus qui modifient les mappages invalident également les références à ceux-ci dans votre code.</span><span class="sxs-lookup"><span data-stu-id="180a2-259">All of the methods above that change mappings also invalidate any references to them in your code.</span></span> <span data-ttu-id="180a2-260">Pour faciliter l’exécution des séquences d'opérations qui modifient l'état d'un mappage, toutes les méthodes qui modifient un mappage renvoient une nouvelle référence de mappage, permettant aux opérations d’être chaînées.</span><span class="sxs-lookup"><span data-stu-id="180a2-260">To make it easier to perform sequences of operations that change a mapping’s state, all of the methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="180a2-261">Par exemple, pour supprimer un mappage existant dans shardmap sm qui contient la clé 25, vous pouvez exécuter les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="180a2-261">For example, to delete an existing mapping in shardmap sm that contains the key 25, you can execute the following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="180a2-262">Ajout d'une partition</span><span class="sxs-lookup"><span data-stu-id="180a2-262">Adding a shard</span></span>
<span data-ttu-id="180a2-263">Souvent, les applications n'ont qu'à ajouter de nouvelles partitions pour gérer des données prévues à partir de nouvelles clés ou plages de clés, pour une carte de partitions qui existe déjà.</span><span class="sxs-lookup"><span data-stu-id="180a2-263">Applications often need to simply add new shards to handle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="180a2-264">Par exemple, une application partitionnée par un ID de client peut requérir l'approvisionnement d'une nouvelle partition pour un nouveau client, ou des données partitionnées mensuellement peuvent requérir l'approvisionnement d'une nouvelle partition avant le début de chaque mois.</span><span class="sxs-lookup"><span data-stu-id="180a2-264">For example, an application sharded by Tenant ID may need to provision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before the start of each new month.</span></span> 

<span data-ttu-id="180a2-265">Si la nouvelle plage de valeurs de clé n'appartient pas déjà à un mappage existant et qu'aucun déplacement de données n'est nécessaire, il est très simple d'ajouter la nouvelle partition et d'associer la nouvelle clé ou la plage à cette partition.</span><span class="sxs-lookup"><span data-stu-id="180a2-265">If the new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple to add the new shard and associate the new key or range to that shard.</span></span> <span data-ttu-id="180a2-266">Pour plus d’informations sur l’ajout de nouvelles partitions, consultez [Ajout d’une nouvelle partition](sql-database-elastic-scale-add-a-shard.md).</span><span class="sxs-lookup"><span data-stu-id="180a2-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="180a2-267">Cependant, pour les scénarios requérant le déplacement de données, l’outil de fusion/fractionnement est requis pour orchestrer le déplacement des données entre les partitions conjointement aux mises à jour nécessaires de la carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="180a2-267">For scenarios that require data movement, however, the split-merge tool is needed to orchestrate the data movement between shards in combination with the necessary shard map updates.</span></span> <span data-ttu-id="180a2-268">Pour plus d'informations sur l'utilisation de l'outil de fractionnement/fusion, consultez [Présentation du service de fractionnement/fusion](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="180a2-268">For details on using the split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
