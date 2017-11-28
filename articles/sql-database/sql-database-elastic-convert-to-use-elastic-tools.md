---
title: "aaaMigrate existant de bases de données montée tooscale | Documents Microsoft"
description: "Convertir des outils de bases de données partitionnées toouse élastique de base de données en créant un gestionnaire de carte de partitions"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a><span data-ttu-id="3d491-103">Migrer tooscale-out de bases de données existant</span><span class="sxs-lookup"><span data-stu-id="3d491-103">Migrate existing databases tooscale-out</span></span>
<span data-ttu-id="3d491-104">Gérer facilement à grande échelle partitionnées bases de données existantes à l’aide des outils de base de données de base de données SQL Azure (par exemple hello [bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md)).</span><span class="sxs-lookup"><span data-stu-id="3d491-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as hello [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="3d491-105">Vous devez d’abord convertir un ensemble existant de hello toouse de bases de données [Gestionnaire de carte de partitions](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="3d491-105">You must first convert an existing set of databases toouse hello [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="3d491-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3d491-106">Overview</span></span>
<span data-ttu-id="3d491-107">toomigrate une base de données partitionnée existante :</span><span class="sxs-lookup"><span data-stu-id="3d491-107">toomigrate an existing sharded database:</span></span> 

1. <span data-ttu-id="3d491-108">Préparer hello [base de données de partition carte manager](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="3d491-108">Prepare hello [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="3d491-109">Créer la carte de partitions hello.</span><span class="sxs-lookup"><span data-stu-id="3d491-109">Create hello shard map.</span></span>
3. <span data-ttu-id="3d491-110">Préparez les partitions hello.</span><span class="sxs-lookup"><span data-stu-id="3d491-110">Prepare hello individual shards.</span></span>  
4. <span data-ttu-id="3d491-111">Ajoutez la carte de partitions toohello mappages.</span><span class="sxs-lookup"><span data-stu-id="3d491-111">Add mappings toohello shard map.</span></span>

<span data-ttu-id="3d491-112">Ces techniques peuvent être implémentés en utilisant soit hello [bibliothèque cliente .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), ou des scripts PowerShell hello trouvé à [Azure SQL DB - scripts d’outils de base de données élastique](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="3d491-112">These techniques can be implemented using either hello [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or hello PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="3d491-113">exemples de Hello ici utilisent des scripts PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="3d491-113">hello examples here use hello PowerShell scripts.</span></span>

<span data-ttu-id="3d491-114">Pour plus d’informations sur hello ShardMapManager, consultez [gestion de carte de partitions](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="3d491-114">For more information about hello ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="3d491-115">Pour une vue d’ensemble d’outils de base de données élastique hello, consultez [vue d’ensemble des fonctionnalités de base de données élastique](sql-database-elastic-scale-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3d491-115">For an overview of hello elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-hello-shard-map-manager-database"></a><span data-ttu-id="3d491-116">Préparer hello partition carte manager base de données</span><span class="sxs-lookup"><span data-stu-id="3d491-116">Prepare hello shard map manager database</span></span>
<span data-ttu-id="3d491-117">Gestionnaire de cartes de partitions Hello est une base de données spécial qui contient les bases de données à grande échelle hello données toomanage.</span><span class="sxs-lookup"><span data-stu-id="3d491-117">hello shard map manager is a special database that contains hello data toomanage scaled-out databases.</span></span> <span data-ttu-id="3d491-118">Vous pouvez utiliser une base de données existante ou en créer une.</span><span class="sxs-lookup"><span data-stu-id="3d491-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="3d491-119">Notez qu’une base de données qui agit comme gestionnaire de carte de partitions ne doit pas être hello même base de données comme une partition.</span><span class="sxs-lookup"><span data-stu-id="3d491-119">Note that a database acting as shard map manager should not be hello same database as a shard.</span></span> <span data-ttu-id="3d491-120">Notez également que de script PowerShell hello ne crée pas de base de données hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="3d491-120">Also note that hello PowerShell script does not create hello database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="3d491-121">Étape 1 : créer un gestionnaire de cartes de partitions</span><span class="sxs-lookup"><span data-stu-id="3d491-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a><span data-ttu-id="3d491-122">Gestionnaire de cartes de partitions hello tooretrieve</span><span class="sxs-lookup"><span data-stu-id="3d491-122">tooretrieve hello shard map manager</span></span>
<span data-ttu-id="3d491-123">Après la création, vous pouvez récupérer le Gestionnaire de carte de partitions hello avec cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3d491-123">After creation, you can retrieve hello shard map manager with this cmdlet.</span></span> <span data-ttu-id="3d491-124">Cette étape est nécessaire chaque fois que vous avez besoin toouse hello ShardMapManager objet.</span><span class="sxs-lookup"><span data-stu-id="3d491-124">This step is needed every time you need toouse hello ShardMapManager object.</span></span>

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a><span data-ttu-id="3d491-125">Étape 2 : créer la carte de partitions hello</span><span class="sxs-lookup"><span data-stu-id="3d491-125">Step 2: create hello shard map</span></span>
<span data-ttu-id="3d491-126">Vous devez sélectionner le type hello de toocreate de carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="3d491-126">You must select hello type of shard map toocreate.</span></span> <span data-ttu-id="3d491-127">choix de Hello dépend de l’architecture de base de données hello :</span><span class="sxs-lookup"><span data-stu-id="3d491-127">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="3d491-128">Un seul locataire par base de données (pour les termes du contrat, consultez hello [glossaire](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="3d491-128">Single tenant per database (For terms, see hello [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="3d491-129">Plusieurs clients par base de données (deux types) :</span><span class="sxs-lookup"><span data-stu-id="3d491-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="3d491-130">Mappage de liste</span><span class="sxs-lookup"><span data-stu-id="3d491-130">List mapping</span></span>
   2. <span data-ttu-id="3d491-131">Mappage de plage</span><span class="sxs-lookup"><span data-stu-id="3d491-131">Range mapping</span></span>

<span data-ttu-id="3d491-132">Pour un modèle de client unique, créez une carte de partitions de **mappage de liste** .</span><span class="sxs-lookup"><span data-stu-id="3d491-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="3d491-133">modèle de locataire unique Hello assigne une base de données par client.</span><span class="sxs-lookup"><span data-stu-id="3d491-133">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="3d491-134">Il s’agit d’un modèle efficace pour les développeurs SaaS, car il simplifie la gestion.</span><span class="sxs-lookup"><span data-stu-id="3d491-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Mappage de liste][1]

<span data-ttu-id="3d491-136">modèle d’architecture mutualisée Hello affecte plusieurs clients tooa une seule base de données (et vous pouvez distribuer des groupes de clients sur plusieurs bases de données).</span><span class="sxs-lookup"><span data-stu-id="3d491-136">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="3d491-137">Utilisez ce modèle lorsque vous attendez que chaque données de petite taille toohave client a besoin.</span><span class="sxs-lookup"><span data-stu-id="3d491-137">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="3d491-138">Dans ce modèle, nous affectons une plage d’utilisation de base de données clients tooa **mappage de plage**.</span><span class="sxs-lookup"><span data-stu-id="3d491-138">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Mappage de plage][2]

<span data-ttu-id="3d491-140">Ou vous pouvez implémenter un modèle de base de données à l’aide un *mappage de liste* tooassign plusieurs locataires tooa base de données unique.</span><span class="sxs-lookup"><span data-stu-id="3d491-140">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="3d491-141">Par exemple, DB1 est toostore utilisé plus d’informations sur l’id de client 1 et 5, et DB2 stocke des données pour les locataires 7 et client 10.</span><span class="sxs-lookup"><span data-stu-id="3d491-141">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Plusieurs clients sur une base de données unique][3] 

<span data-ttu-id="3d491-143">**Selon votre choix, procédez de l’une des manières suivantes :**</span><span class="sxs-lookup"><span data-stu-id="3d491-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="3d491-144">Option 1 : Créer une carte de partitions pour un mappage de liste</span><span class="sxs-lookup"><span data-stu-id="3d491-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="3d491-145">Créer une carte de partitions à l’aide hello ShardMapManager objet.</span><span class="sxs-lookup"><span data-stu-id="3d491-145">Create a shard map using hello ShardMapManager object.</span></span> 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="3d491-146">Option 2 : Créer une carte de partitions pour un mappage de plage</span><span class="sxs-lookup"><span data-stu-id="3d491-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="3d491-147">Notez que tooutilize ce modèle de mappage, plages continue de toobe a besoin de valeurs d’id client il est donc écart toohave acceptable dans des plages hello en ignorant simplement des limites de hello lors de la création de bases de données hello.</span><span class="sxs-lookup"><span data-stu-id="3d491-147">Note that tooutilize this mapping pattern, tenant id values needs toobe continuous ranges, and it is acceptable toohave gap in hello ranges by simply skipping hello range when creating hello databases.</span></span>

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="3d491-148">Option 3 : Mappages de liste sur une base de données unique</span><span class="sxs-lookup"><span data-stu-id="3d491-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="3d491-149">La configuration de ce modèle nécessite également la création d’un mappage de liste comme indiqué à l’étape 2, option 1.</span><span class="sxs-lookup"><span data-stu-id="3d491-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="3d491-150">Étape 3 : préparer les partitions individuelles</span><span class="sxs-lookup"><span data-stu-id="3d491-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="3d491-151">Ajoutez chaque gestionnaire de carte de partitions toohello partitions (base de données).</span><span class="sxs-lookup"><span data-stu-id="3d491-151">Add each shard (database) toohello shard map manager.</span></span> <span data-ttu-id="3d491-152">Elle prépare les bases de données individuelles hello pour le stockage des informations de mappage.</span><span class="sxs-lookup"><span data-stu-id="3d491-152">This prepares hello individual databases for storing mapping information.</span></span> <span data-ttu-id="3d491-153">Exécutez cette méthode sur chaque partition.</span><span class="sxs-lookup"><span data-stu-id="3d491-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="3d491-154">Étape 4 : Ajouter des mappages</span><span class="sxs-lookup"><span data-stu-id="3d491-154">Step 4: Add mappings</span></span>
<span data-ttu-id="3d491-155">Ajout de Hello de mappages dépend de type hello de carte de partitions que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="3d491-155">hello addition of mappings depends on hello kind of shard map you created.</span></span> <span data-ttu-id="3d491-156">Si vous avez créé un mappage de liste, vous ajoutez des mappages de liste.</span><span class="sxs-lookup"><span data-stu-id="3d491-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="3d491-157">Si vous avez créé un mappage de plage, vous ajoutez des mappages de plage.</span><span class="sxs-lookup"><span data-stu-id="3d491-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-hello-data-for-a-list-mapping"></a><span data-ttu-id="3d491-158">Option 1 : mapper des données hello pour un mappage de liste</span><span class="sxs-lookup"><span data-stu-id="3d491-158">Option 1: map hello data for a list mapping</span></span>
<span data-ttu-id="3d491-159">Mapper les données de hello en ajoutant un mappage de liste pour chaque client.</span><span class="sxs-lookup"><span data-stu-id="3d491-159">Map hello data by adding a list mapping for each tenant.</span></span>  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a><span data-ttu-id="3d491-160">Option 2 : mapper des données hello pour un mappage de plage</span><span class="sxs-lookup"><span data-stu-id="3d491-160">Option 2: map hello data for a range mapping</span></span>
<span data-ttu-id="3d491-161">Ajouter des mappages de plage hello pour tous les hello client plage d’id - associations de base de données :</span><span class="sxs-lookup"><span data-stu-id="3d491-161">Add hello range mappings for all hello tenant id range - database associations:</span></span>

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="3d491-162">Étape 4 option 3 : mapper des données de hello pour plusieurs clients sur une base de données</span><span class="sxs-lookup"><span data-stu-id="3d491-162">Step 4 option 3: map hello data for multiple tenants on a single database</span></span>
<span data-ttu-id="3d491-163">Pour chaque client, exécutez hello Add-ListMapping (option 1, ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="3d491-163">For each tenant, run hello Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-hello-mappings"></a><span data-ttu-id="3d491-164">Vérification des mappages de hello</span><span class="sxs-lookup"><span data-stu-id="3d491-164">Checking hello mappings</span></span>
<span data-ttu-id="3d491-165">Pour plus d’informations sur les partitions existantes hello et les mappages de hello associées peuvent être interrogés à l’aide de commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="3d491-165">Information about hello existing shards and hello mappings associated with them can be queried using following commands:</span></span>  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="3d491-166">Résumé</span><span class="sxs-lookup"><span data-stu-id="3d491-166">Summary</span></span>
<span data-ttu-id="3d491-167">Une fois que vous avez terminé le programme d’installation hello, vous pouvez commencer la bibliothèque cliente de toouse hello élastique de base de données.</span><span class="sxs-lookup"><span data-stu-id="3d491-167">Once you have completed hello setup, you can begin toouse hello Elastic Database client library.</span></span> <span data-ttu-id="3d491-168">Vous pouvez également utiliser le [routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md) et la [requête sur plusieurs partitions](sql-database-elastic-scale-multishard-querying.md).</span><span class="sxs-lookup"><span data-stu-id="3d491-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d491-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3d491-169">Next steps</span></span>
<span data-ttu-id="3d491-170">Obtenir les scripts PowerShell hello [sripts des outils de base de données élastique de base de données Azure SQL](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="3d491-170">Get hello PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="3d491-171">Hello outils sont également sur GitHub : [Azure/élastique-db-tools](https://github.com/Azure/elastic-db-tools).</span><span class="sxs-lookup"><span data-stu-id="3d491-171">hello tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="3d491-172">Utilisez hello outil de fusion et fractionnement toomove données tooor d’un modèle de client unique tooa modèle mutualisé.</span><span class="sxs-lookup"><span data-stu-id="3d491-172">Use hello split-merge tool toomove data tooor from a multi-tenant model tooa single tenant model.</span></span> <span data-ttu-id="3d491-173">Consultez [Outil de fractionnement et de fusion](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3d491-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d491-174">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3d491-174">Additional resources</span></span>
<span data-ttu-id="3d491-175">Pour plus d’informations sur les modèles d’architecture de données des applications de base de données de logiciels en tant que service (SaaS) mutualisés, consultez [Modèles de conception pour les applications SaaS mutualisées avec Base de données SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="3d491-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="3d491-176">Questions et demandes de fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="3d491-176">Questions and Feature Requests</span></span>
<span data-ttu-id="3d491-177">Pour toute question, veuillez contacter toous sur hello [Forum sur la base de données SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) et pour les demandes de fonctionnalités, ajoutez-les toohello [forum de commentaires de la base de données SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="3d491-177">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

