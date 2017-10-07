---
title: "technologies de base de données SQL en mémoire aaaAzure | Documents Microsoft"
description: "Les technologies de base de données SQL en mémoire Azure améliorer sensiblement les performances hello de transactionnelle et les charges de travail analytique. Découvrez comment parti tootake de ces technologies."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="e658b-104">Optimisation des performances à l’aide des technologies en mémoire dans SQL Database</span><span class="sxs-lookup"><span data-stu-id="e658b-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="e658b-105">À l’aide des technologies en mémoire dans Azure SQL Database, vous pouvez obtenir des améliorations des performances pour différentes charges de travail : transactionnelles (traitement transactionnel en ligne (OLTP)), analytiques (traitement analytique en ligne (OLAP)) et mixtes (traitement transactionnel/analytique hybride (HTAP)).</span><span class="sxs-lookup"><span data-stu-id="e658b-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="e658b-106">Raison de hello plus efficace des requêtes et traitement des transactions, de technologies en mémoire vous aident également tooreduce coût.</span><span class="sxs-lookup"><span data-stu-id="e658b-106">Because of hello more efficient query and transaction processing, In-Memory technologies also help you tooreduce cost.</span></span> <span data-ttu-id="e658b-107">Vous n’avez généralement pas besoin hello tooupgrade tarification hello de base de données tooachieve des gains de performances.</span><span class="sxs-lookup"><span data-stu-id="e658b-107">You typically don't need tooupgrade hello pricing tier of hello database tooachieve performance gains.</span></span> <span data-ttu-id="e658b-108">Dans certains cas, vous pouvez même peut-être réduire hello tarification et toujours voir les améliorations des performances avec les technologies en mémoire.</span><span class="sxs-lookup"><span data-stu-id="e658b-108">In some cases, you might even be able reduce hello pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="e658b-109">Voici deux exemples illustrant comment l’OLTP en mémoire ont aidé à toosignificantly améliorer les performances :</span><span class="sxs-lookup"><span data-stu-id="e658b-109">Here are two examples of how In-Memory OLTP helped toosignificantly improve performance:</span></span>

- <span data-ttu-id="e658b-110">À l’aide de l’OLTP en mémoire, [Solutions d’entreprise de Quorum a été toodouble en mesure de leur charge de travail tout en améliorant la dtu de 70 %](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="e658b-110">By using In-Memory OLTP, [Quorum Business Solutions was able toodouble their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="e658b-111">DTU signifie *unité de débit de base de données* et inclut une mesure de la consommation des ressources.</span><span class="sxs-lookup"><span data-stu-id="e658b-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="e658b-112">Hello vidéo suivante montre une amélioration significative de la consommation des ressources avec une charge de travail d’exemple : [OLTP en mémoire dans la base de données de SQL Azure vidéo](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span><span class="sxs-lookup"><span data-stu-id="e658b-112">hello following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="e658b-113">Pour plus d’informations, voir blog de hello : [OLTP en mémoire dans le billet de Blog de base de données SQL Azure](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="e658b-113">For more details, see hello blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="e658b-114">Technologies en mémoire sont disponibles dans toutes les bases de données de niveau Premium de hello, y compris les bases de données dans les pools élastiques Premium.</span><span class="sxs-lookup"><span data-stu-id="e658b-114">In-Memory technologies are available in all databases in hello Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="e658b-115">Hello vidéo suivante explique les gains de performances potentiels avec les technologies en mémoire dans la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e658b-115">hello following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="e658b-116">N’oubliez pas que les gains de performance hello que vous voyez toujours dépendent de nombreux facteurs, notamment la nature hello de charge de travail hello et des données, le modèle d’accès de base de données hello et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="e658b-116">Remember that hello performance gain that you see always depends on many factors, including hello nature of hello workload and data, access pattern of hello database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="e658b-117">Base de données SQL Azure a hello suivant des technologies en mémoire :</span><span class="sxs-lookup"><span data-stu-id="e658b-117">Azure SQL Database has hello following In-Memory technologies:</span></span>

- <span data-ttu-id="e658b-118">*L’OLTP en mémoire* augmente le débit et réduit la latence de traitement des transactions.</span><span class="sxs-lookup"><span data-stu-id="e658b-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="e658b-119">Les scénarios qui bénéficient de l’OLTP en mémoire sont : le traitement de transactions haut débit, notamment les données commerciales et de jeux, l’ingestion de données d’événements ou d’appareils IoT, la mise en cache, le chargement de données, les tables temporaires et les scénarios de variables de table.</span><span class="sxs-lookup"><span data-stu-id="e658b-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="e658b-120">*Index cluster columnstore* réduit l’encombrement de votre stockage (haut too10 fois) et d’améliorer les performances des requêtes de création de rapports et analytique.</span><span class="sxs-lookup"><span data-stu-id="e658b-120">*Clustered columnstore indexes* reduce your storage footprint (up too10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="e658b-121">Vous pouvez l’utiliser avec les tables de faits dans votre toofit de mini-Data Warehouses données davantage de données dans votre base de données et améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="e658b-121">You can use it with fact tables in your data marts toofit more data in your database and improve performance.</span></span> <span data-ttu-id="e658b-122">En outre, vous pouvez utiliser avec les données d’historique dans tooarchive de votre base de données opérationnelle et être en mesure de tooquery des heures de too10 davantage de données.</span><span class="sxs-lookup"><span data-stu-id="e658b-122">Also, you can use it with historical data in your operational database tooarchive and be able tooquery up too10 times more data.</span></span>
- <span data-ttu-id="e658b-123">*Les index non cluster columnstore* pour HTAP aide vous toogain des informations en temps réel dans votre entreprise grâce à l’interrogation hello opérationnelle de base de données directement, sans hello besoin toorun une extraction coûteuse, la transformation et le processus de chargement (ETL) et attendre pour hello toobe de l’entrepôt de données remplie.</span><span class="sxs-lookup"><span data-stu-id="e658b-123">*Nonclustered columnstore indexes* for HTAP help you toogain real-time insights into your business through querying hello operational database directly, without hello need toorun an expensive extract, transform, and load (ETL) process and wait for hello data warehouse toobe populated.</span></span> <span data-ttu-id="e658b-124">Les index non cluster columnstore exécution est très rapide des requêtes de l’analytique sur la base de données OLTP hello, tout en réduisant l’impact de hello sur la charge de travail opérationnelle hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on hello OLTP database, while reducing hello impact on hello operational workload.</span></span>
- <span data-ttu-id="e658b-125">Vous pouvez également avoir combinaison hello d’une table mémoire optimisée avec un index columnstore.</span><span class="sxs-lookup"><span data-stu-id="e658b-125">You can also have hello combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="e658b-126">Cette combinaison vous permet de tooperform très rapide traitement des transactions et trop*simultanément* analytique d’exécution des requêtes très rapidement sur hello même données.</span><span class="sxs-lookup"><span data-stu-id="e658b-126">This combination enables you tooperform very fast transaction processing, and too*concurrently* run analytics queries very quickly on hello same data.</span></span>

<span data-ttu-id="e658b-127">Les index columnstore et OLTP en mémoire ont fait partie du produit de SQL Server hello depuis 2012 et 2014, respectivement.</span><span class="sxs-lookup"><span data-stu-id="e658b-127">Both columnstore indexes and In-Memory OLTP have been part of hello SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="e658b-128">Base de données SQL Azure et de SQL Server partagent hello même implémentation des technologies en mémoire.</span><span class="sxs-lookup"><span data-stu-id="e658b-128">Azure SQL Database and SQL Server share hello same implementation of In-Memory technologies.</span></span> <span data-ttu-id="e658b-129">À l’avenir, les nouvelles fonctionnalités pour ces technologies seront publiées dans Azure SQL Database avant d’être publiées dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e658b-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="e658b-130">Cette rubrique décrit les aspects de l’OLTP et columnstore index tooAzure spécifique de la base de données SQL et comprend également des exemples :</span><span class="sxs-lookup"><span data-stu-id="e658b-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific tooAzure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="e658b-131">Vous verrez impact hello de ces technologies sur des limites de taille de stockage et des données.</span><span class="sxs-lookup"><span data-stu-id="e658b-131">You'll see hello impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="e658b-132">Vous verrez comment toomanage hello déplacement de bases de données qui utilisent ces technologies entre hello différent niveaux tarifaires.</span><span class="sxs-lookup"><span data-stu-id="e658b-132">You'll see how toomanage hello movement of databases that use these technologies between hello different pricing tiers.</span></span>
- <span data-ttu-id="e658b-133">Vous verrez deux exemples qui illustrent l’utilisation de hello d’OLTP en mémoire, ainsi que les index columnstore dans la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e658b-133">You'll see two samples that illustrate hello use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="e658b-134">Hello suivant des ressources pour plus d’informations, consultez.</span><span class="sxs-lookup"><span data-stu-id="e658b-134">See hello following resources for more information.</span></span>

<span data-ttu-id="e658b-135">Obtenir des informations détaillées sur les technologies hello :</span><span class="sxs-lookup"><span data-stu-id="e658b-135">In-depth information about hello technologies:</span></span>

- <span data-ttu-id="e658b-136">[Vue d’ensemble de l’OLTP en mémoire et les scénarios d’utilisation](https://msdn.microsoft.com/library/mt774593.aspx) (inclut des études de cas de références toocustomer et tooget informations démarré)</span><span class="sxs-lookup"><span data-stu-id="e658b-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references toocustomer case studies and information tooget started)</span></span>
- [<span data-ttu-id="e658b-137">Documentation pour l’OLTP In-Memory</span><span class="sxs-lookup"><span data-stu-id="e658b-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="e658b-138">Description des index columnstore</span><span class="sxs-lookup"><span data-stu-id="e658b-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="e658b-139">Traitement hybride transactionnel et analytique (HTAP), également appelé [analytique opérationnelle en temps réel](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="e658b-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="e658b-140">Une introduction rapide sur OLTP en mémoire : [démarrage rapide 1 : Technologies d’OLTP en mémoire plus rapidement les performances de T-SQL](http://msdn.microsoft.com/library/mt694156.aspx) (un autre article toohelp mise en route)</span><span class="sxs-lookup"><span data-stu-id="e658b-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article toohelp you get started)</span></span>

<span data-ttu-id="e658b-141">Vidéos détaillées sur les technologies de hello :</span><span class="sxs-lookup"><span data-stu-id="e658b-141">In-depth videos about hello technologies:</span></span>

- <span data-ttu-id="e658b-142">[OLTP en mémoire dans la base de données SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (qui contient une démonstration de performances avantages et les étapes tooreproduce ces résultats vous-même)</span><span class="sxs-lookup"><span data-stu-id="e658b-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps tooreproduce these results yourself)</span></span>
- [<span data-ttu-id="e658b-143">Vidéos d’OLTP en mémoire : Ce qu’il est/comment et quand toouse il</span><span class="sxs-lookup"><span data-stu-id="e658b-143">In-Memory OLTP Videos: What it is and When/How toouse it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="e658b-144">Index Columnstore : vidéos d’analyse en mémoire d’Ignite 2016</span><span class="sxs-lookup"><span data-stu-id="e658b-144">Columnstore Index: In-Memory Analytics Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="e658b-145">Taille des données et du stockage</span><span class="sxs-lookup"><span data-stu-id="e658b-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="e658b-146">Seuil de la taille des données et du stockage pour l’OLTP en mémoire</span><span class="sxs-lookup"><span data-stu-id="e658b-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="e658b-147">l’OLTP en mémoire inclut des tables optimisées en mémoire, qui sont utilisées pour stocker des données de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e658b-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="e658b-148">Ces tables sont toofit requis dans la mémoire.</span><span class="sxs-lookup"><span data-stu-id="e658b-148">These tables are required toofit in memory.</span></span> <span data-ttu-id="e658b-149">Étant donné que vous gérez mémoire directement dans hello service de base de données SQL, nous avons concept hello d’un quota pour les données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e658b-149">Because you manage memory directly in hello SQL Database service, we have hello  concept of a quota for user data.</span></span> <span data-ttu-id="e658b-150">Cette idée est référencé tooas *stockage de l’OLTP en mémoire*.</span><span class="sxs-lookup"><span data-stu-id="e658b-150">This idea is referred tooas *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="e658b-151">Chaque niveau tarifaire de base de données autonome pris en charge et chaque niveau tarifaire de pool élastique inclut une certaine quantité de stockage OLTP en mémoire.</span><span class="sxs-lookup"><span data-stu-id="e658b-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="e658b-152">Au moment de hello de l’écriture, vous obtenez un gigaoctet de stockage pour chaque 125 unités de transaction de base de données (Udbd) ou d’une base de données élastique unités de transaction (Edtu).</span><span class="sxs-lookup"><span data-stu-id="e658b-152">At hello time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="e658b-153">Hello [les niveaux de service de base de données SQL](sql-database-service-tiers.md) article a liste officielle de hello de stockage hello OLTP en mémoire est disponible pour chaque base de données autonome et pool élastique tarification pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e658b-153">hello [SQL Database service tiers](sql-database-service-tiers.md) article has hello official list of hello In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="e658b-154">Hello suivant le nombre d’éléments vers votre plafond de stockage OLTP en mémoire :</span><span class="sxs-lookup"><span data-stu-id="e658b-154">hello following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="e658b-155">Lignes de données utilisateur actives dans des tables optimisées en mémoire et variables de table.</span><span class="sxs-lookup"><span data-stu-id="e658b-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="e658b-156">Notez que les anciennes versions de ligne ne comptent pas vers l’extrémité de fin hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-156">Note that old row versions don't count toward hello cap.</span></span>
- <span data-ttu-id="e658b-157">Index de tables optimisées en mémoire.</span><span class="sxs-lookup"><span data-stu-id="e658b-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="e658b-158">Coûts de fonctionnement des opérations ALTER TABLE.</span><span class="sxs-lookup"><span data-stu-id="e658b-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="e658b-159">Si vous avez atteint le plafond de hello, vous recevez une erreur de quota de sortie, et vous n’êtes plus en mesure de données de tooinsert ou de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="e658b-159">If you hit hello cap, you receive an out-of-quota error, and you are no longer able tooinsert or update data.</span></span> <span data-ttu-id="e658b-160">toomitigate cette erreur, supprimer des données ou augmenter hello tarification de base de données hello ou un pool.</span><span class="sxs-lookup"><span data-stu-id="e658b-160">toomitigate this error, delete data or increase hello pricing tier of hello database or pool.</span></span>

<span data-ttu-id="e658b-161">Pour plus d’informations sur l’analyse de l’utilisation du stockage de l’OLTP en mémoire et de configuration des alertes quand vous atteignez presque cap de hello, consultez [stockage analyse en mémoire](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="e658b-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit hello cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="e658b-162">À propos des pools élastiques</span><span class="sxs-lookup"><span data-stu-id="e658b-162">About elastic pools</span></span>

<span data-ttu-id="e658b-163">Avec les pools élastiques, hello stockage de l’OLTP en mémoire est partagé entre toutes les bases de données dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-163">With elastic pools, hello In-Memory OLTP storage is shared across all databases in hello pool.</span></span> <span data-ttu-id="e658b-164">Par conséquent, l’utilisation de hello dans une base de données peut éventuellement affecter les autres bases de données.</span><span class="sxs-lookup"><span data-stu-id="e658b-164">Therefore, hello usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="e658b-165">Voici deux solutions :</span><span class="sxs-lookup"><span data-stu-id="e658b-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="e658b-166">Configurez un Max-eDTU pour les bases de données qui est inférieur au nombre d’eDTU hello pour le pool hello dans sa globalité.</span><span class="sxs-lookup"><span data-stu-id="e658b-166">Configure a Max-eDTU for databases that is lower than hello eDTU count for hello pool as a whole.</span></span> <span data-ttu-id="e658b-167">Cette valeur maximale limite hello OLTP en mémoire l’utilisation du stockage, des bases de données dans le pool de hello, toohello taille qui correspond le nombre d’eDTU toohello.</span><span class="sxs-lookup"><span data-stu-id="e658b-167">This maximum caps hello In-Memory OLTP storage utilization, in any database in hello pool, toohello size that corresponds toohello eDTU count.</span></span>
- <span data-ttu-id="e658b-168">Configurez un nombre d’eDTU minimal supérieur à 0.</span><span class="sxs-lookup"><span data-stu-id="e658b-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="e658b-169">Cette garantie minimale que chaque base de données dans le pool de hello a quantité hello du stockage OLTP en mémoire disponible qui correspond toohello configuré Min-eDTU.</span><span class="sxs-lookup"><span data-stu-id="e658b-169">This minimum guarantees that each database in hello pool has hello amount of available In-Memory OLTP storage that corresponds toohello configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="e658b-170">Taille des données et stockage pour les index columnstore</span><span class="sxs-lookup"><span data-stu-id="e658b-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="e658b-171">Index ColumnStore ne sont pas requis toofit en mémoire.</span><span class="sxs-lookup"><span data-stu-id="e658b-171">Columnstore indexes aren't required toofit in memory.</span></span> <span data-ttu-id="e658b-172">Par conséquent, hello limite sur la taille de hello des index de hello a la taille globale maximale de la base de données de hello, qui est décrit dans hello [les niveaux de service de base de données SQL](sql-database-service-tiers.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="e658b-172">Therefore, hello only cap on hello size of hello indexes is hello maximum overall database size, which is documented in hello [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="e658b-173">Lorsque vous utilisez des index columnstore en cluster, la compression en colonnes est utilisée pour le stockage de table de base hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-173">When you use clustered columnstore indexes, columnar compression is used for hello base table storage.</span></span> <span data-ttu-id="e658b-174">Cette compression peut réduire considérablement l’encombrement du stockage des données utilisateur, ce qui signifie que vous pouvez entrer davantage de données dans la base de données hello hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-174">This compression can significantly reduce hello storage footprint of your user data, which means that you can fit more data in hello database.</span></span> <span data-ttu-id="e658b-175">Et la compression de hello peut être accrue encore plue avec [la compression d’archivage en colonnes](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span><span class="sxs-lookup"><span data-stu-id="e658b-175">And hello compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="e658b-176">quantité de Hello de compression qui vous pouvez d’obtenir dépend de la nature hello de données de hello, mais la compression de 10 fois hello n’est pas rare.</span><span class="sxs-lookup"><span data-stu-id="e658b-176">hello amount of compression that you can achieve depends on hello nature of hello data, but 10 times hello compression is not uncommon.</span></span>

<span data-ttu-id="e658b-177">Par exemple, si vous disposez d’une base de données avec une taille maximale de 1 téraoctet (To) et obtenir de compression de hello 10 fois à l’aide des index columnstore, vous pouvez inclure un total de 10 To de données utilisateur dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times hello compression by using columnstore indexes, you can fit a total of 10 TB of user data in hello database.</span></span>

<span data-ttu-id="e658b-178">Lorsque vous utilisez des index columnstore non cluster, table de base hello est toujours stockée au format rowstore traditionnelle de hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-178">When you use nonclustered columnstore indexes, hello base table is still stored in hello traditional rowstore format.</span></span> <span data-ttu-id="e658b-179">Par conséquent, les économies de stockage hello ne sont pas important qu’avec des index columnstore en cluster.</span><span class="sxs-lookup"><span data-stu-id="e658b-179">Therefore, hello storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="e658b-180">Toutefois, si vous remplacez un nombre d’index non cluster traditionnels avec un index columnstore unique, vous pouvez toujours voir un économies globales dans un encombrement de stockage hello pour la table de hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in hello storage footprint for hello table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="e658b-181">Déplacement de bases de données utilisant des technologies en mémoire entre différents niveaux tarifaires</span><span class="sxs-lookup"><span data-stu-id="e658b-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="e658b-182">Il ne sont jamais les incompatibilités ou autres problèmes lorsque vous mettez à niveau tooa supérieur tarification, telles que de tooPremium Standard.</span><span class="sxs-lookup"><span data-stu-id="e658b-182">There are never any incompatibilities or other problems when you upgrade tooa higher pricing tier, such as from Standard tooPremium.</span></span> <span data-ttu-id="e658b-183">ressources et les fonctionnalités disponibles hello uniquement augmentent.</span><span class="sxs-lookup"><span data-stu-id="e658b-183">hello available functionality and resources only increase.</span></span>

<span data-ttu-id="e658b-184">Mais hello déclassement tarification peut nuire à votre base de données.</span><span class="sxs-lookup"><span data-stu-id="e658b-184">But downgrading hello pricing tier can negatively impact your database.</span></span> <span data-ttu-id="e658b-185">impact de Hello est particulièrement évident lorsque vous rétrogradez à partir de Premium tooStandard ou de base lorsque votre base de données contient des objets de l’OLTP en mémoire.</span><span class="sxs-lookup"><span data-stu-id="e658b-185">hello impact is especially apparent when you downgrade from Premium tooStandard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="e658b-186">Tables optimisées en mémoire et des index columnstore, ne sont pas disponibles après la rétrogradation de hello (même si elles restent visibles).</span><span class="sxs-lookup"><span data-stu-id="e658b-186">Memory-optimized tables, and columnstore indexes, are unavailable after hello downgrade (even if they remain visible).</span></span> <span data-ttu-id="e658b-187">Bonjour les mêmes considérations s’appliquent lorsque vous êtes réduisant hello tarification d’un pool élastique ou déplacement d’une base de données avec des technologies en mémoire, dans une norme ou base pool élastique.</span><span class="sxs-lookup"><span data-stu-id="e658b-187">hello same considerations apply when you're lowering hello pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="e658b-188">OLTP In-Memory.</span><span class="sxs-lookup"><span data-stu-id="e658b-188">In-Memory OLTP</span></span>

<span data-ttu-id="e658b-189">*Rétrogradation tooBasic et Standard*: OLTP en mémoire n’est pas pris en charge dans les bases de données de niveau Standard ou Basic de hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-189">*Downgrading tooBasic/Standard*: In-Memory OLTP isn't supported in databases in hello Standard or Basic tier.</span></span> <span data-ttu-id="e658b-190">En outre, il n’est pas possible de toomove une base de données qui a des toohello d’objets OLTP en mémoire niveau Standard ou Basic.</span><span class="sxs-lookup"><span data-stu-id="e658b-190">In addition, it isn't possible toomove a database that has any In-Memory OLTP objects toohello Standard or Basic tier.</span></span>

<span data-ttu-id="e658b-191">Avant de la rétrogradation de base/tooStandard hello de base de données, supprimez toutes les tables optimisées en mémoire et les types de tables, ainsi que tous les modules T-SQL compilés en mode natif.</span><span class="sxs-lookup"><span data-stu-id="e658b-191">Before you downgrade hello database tooStandard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="e658b-192">Il existe un toounderstand moyen par programmation si une base de données prend en charge OLTP en mémoire.</span><span class="sxs-lookup"><span data-stu-id="e658b-192">There is a programmatic way toounderstand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="e658b-193">Vous pouvez exécuter hello suivant la requête Transact-SQL :</span><span class="sxs-lookup"><span data-stu-id="e658b-193">You can execute hello following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="e658b-194">Si la requête de hello retourne **1**, OLTP en mémoire est prise en charge dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="e658b-194">If hello query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="e658b-195">*Rétrogradation de niveau Premium inférieur de tooa*: les données dans des tables optimisées en mémoire doivent tenir au sein du stockage hello OLTP en mémoire est associée à hello tarification de base de données hello ou qui est disponible dans le pool élastique de hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-195">*Downgrading tooa lower Premium tier*: Data in memory-optimized tables must fit within hello In-Memory OLTP storage that is associated with hello pricing tier of hello database or is available in hello elastic pool.</span></span> <span data-ttu-id="e658b-196">Si vous essayez de hello toolower niveau tarifaire ou déplacez la base de données hello dans un pool qui n’a pas suffisamment stockage OLTP en mémoire disponible, hello échoue.</span><span class="sxs-lookup"><span data-stu-id="e658b-196">If you try toolower hello pricing tier or move hello database into a pool that doesn't have enough available In-Memory OLTP storage, hello operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="e658b-197">Index Columnstore</span><span class="sxs-lookup"><span data-stu-id="e658b-197">Columnstore indexes</span></span>

<span data-ttu-id="e658b-198">*Rétrogradation tooBasic ou Standard*: Columnstore index sont pris en charge uniquement sur le niveau de tarification hello Premium et non sous hello niveaux Standard ou Basic.</span><span class="sxs-lookup"><span data-stu-id="e658b-198">*Downgrading tooBasic or Standard*: Columnstore indexes are supported only on hello Premium pricing tier, and not on hello Standard or Basic tiers.</span></span> <span data-ttu-id="e658b-199">Lors de la rétrogradation de votre base de données tooStandard ou le Basic, l’index columnstore est plus disponible.</span><span class="sxs-lookup"><span data-stu-id="e658b-199">When you downgrade your database tooStandard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="e658b-200">système de Hello tient à jour l’index columnstore, mais il ne s’appuie sur les index hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-200">hello system maintains your columnstore index, but it never leverages hello index.</span></span> <span data-ttu-id="e658b-201">Si vous passez ensuite tooPremium précédent, l’index columnstore est immédiatement prêt toobe exploitée à nouveau.</span><span class="sxs-lookup"><span data-stu-id="e658b-201">If you later upgrade back tooPremium, your columnstore index is immediately ready toobe leveraged again.</span></span>

<span data-ttu-id="e658b-202">Si vous avez un **cluster** index columnstore, ensemble de la table hello devient indisponible après la rétrogradation de la couche.</span><span class="sxs-lookup"><span data-stu-id="e658b-202">If you have a **clustered** columnstore index, hello whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="e658b-203">Par conséquent, nous vous recommandons de supprimer l’ensemble *cluster* d’index columnstore avant de passer de votre base de données sous le niveau Premium de hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below hello Premium tier.</span></span>

<span data-ttu-id="e658b-204">*Rétrogradation de niveau Premium inférieur de tooa*: cette rétrogradation réussit si la base de données entière hello s’intègre au sein de la taille maximale de la base de données de hello pour cible hello niveau tarifaire ou au sein du stockage disponible dans le pool élastique de hello hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-204">*Downgrading tooa lower Premium tier*: This downgrade succeeds if hello whole database fits within hello maximum database size for hello target pricing tier, or within hello available storage in hello elastic pool.</span></span> <span data-ttu-id="e658b-205">Aucun impact n’est spécifique à partir de l’index columnstore de hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-205">There is no specific impact from hello columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a><span data-ttu-id="e658b-206">1. Installer l’exemple d’OLTP en mémoire hello</span><span class="sxs-lookup"><span data-stu-id="e658b-206">1. Install hello In-Memory OLTP sample</span></span>

<span data-ttu-id="e658b-207">Vous pouvez créer la base de données AdventureWorksLT hello en quelques clics dans hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e658b-207">You can create hello AdventureWorksLT sample database with a few clicks in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="e658b-208">Ensuite, hello étapes de cette section expliquent comment vous pouvez enrichir votre base de données AdventureWorksLT avec des objets OLTP en mémoire et illustre les performances.</span><span class="sxs-lookup"><span data-stu-id="e658b-208">Then, hello steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="e658b-209">Pour une démonstration plus simple mais intéressante des performances de l’OLTP en mémoire, consultez :</span><span class="sxs-lookup"><span data-stu-id="e658b-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="e658b-210">Version : [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="e658b-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="e658b-211">Code source : [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="e658b-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="e658b-212">Procédure d’installation :</span><span class="sxs-lookup"><span data-stu-id="e658b-212">Installation steps</span></span>

1. <span data-ttu-id="e658b-213">Bonjour [portail Azure](https://portal.azure.com/), créez une base de données Premium sur un serveur.</span><span class="sxs-lookup"><span data-stu-id="e658b-213">In hello [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="e658b-214">Ensemble hello **Source** base de données AdventureWorksLT toohello.</span><span class="sxs-lookup"><span data-stu-id="e658b-214">Set hello **Source** toohello AdventureWorksLT sample database.</span></span> <span data-ttu-id="e658b-215">Pour obtenir des instructions détaillées, consultez [Créer votre première base de données SQL Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e658b-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="e658b-216">Se connecter toohello de base de données avec SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="e658b-216">Connect toohello database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="e658b-217">Hello de copie [script Transact-SQL de l’OLTP en mémoire](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="e658b-217">Copy hello [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour clipboard.</span></span> <span data-ttu-id="e658b-218">Hello script T-SQL crée des objets en mémoire nécessaire hello hello AdventureWorksLT base de données exemple que vous avez créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="e658b-218">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="e658b-219">Collez le script T-SQL de hello dans SSMS, puis exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-219">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="e658b-220">Hello `MEMORY_OPTIMIZED = ON` les instructions CREATE TABLE clause sont cruciales.</span><span class="sxs-lookup"><span data-stu-id="e658b-220">hello `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="e658b-221">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e658b-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="e658b-222">Erreur 40536</span><span class="sxs-lookup"><span data-stu-id="e658b-222">Error 40536</span></span>


<span data-ttu-id="e658b-223">Si vous obtenez une erreur 40536 lorsque vous exécutez le script de hello T-SQL, exécutez hello suivant tooverify de script T-SQL si la base de données hello prend en charge en mémoire :</span><span class="sxs-lookup"><span data-stu-id="e658b-223">If you get error 40536 when you run hello T-SQL script, run hello following T-SQL script tooverify whether hello database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="e658b-224">Un résultat de **0** signifie que la technologie en mémoire n’est pas prise en charge, et un résultat de **1** signifie qu’elle l’est.</span><span class="sxs-lookup"><span data-stu-id="e658b-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="e658b-225">problème de hello toodiagnose, assurez-vous que cette base de données hello est au niveau de service Premium hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-225">toodiagnose hello problem, ensure that hello database is at hello Premium service tier.</span></span>


#### <a name="about-hello-created-memory-optimized-items"></a><span data-ttu-id="e658b-226">À propos de hello créé des éléments de la mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="e658b-226">About hello created memory-optimized items</span></span>

<span data-ttu-id="e658b-227">**Tables**: exemple hello contient hello optimisées en mémoire des tables suivantes :</span><span class="sxs-lookup"><span data-stu-id="e658b-227">**Tables**: hello sample contains hello following memory-optimized tables:</span></span>

- <span data-ttu-id="e658b-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="e658b-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="e658b-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="e658b-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="e658b-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="e658b-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="e658b-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="e658b-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="e658b-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="e658b-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="e658b-233">Vous pouvez inspecter les tables optimisées en mémoire via hello **l’Explorateur d’objets** dans SSMS.</span><span class="sxs-lookup"><span data-stu-id="e658b-233">You can inspect memory-optimized tables through hello **Object Explorer** in SSMS.</span></span> <span data-ttu-id="e658b-234">Cliquez avec le bouton droit sur **Tables** > **Filtre** > **Paramètres de filtre** > **Est à mémoire optimisée**.</span><span class="sxs-lookup"><span data-stu-id="e658b-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="e658b-235">valeur de Hello est égal à 1.</span><span class="sxs-lookup"><span data-stu-id="e658b-235">hello value equals 1.</span></span>


<span data-ttu-id="e658b-236">Ou bien, vous pouvez interroger les vues de catalogue hello, telles que :</span><span class="sxs-lookup"><span data-stu-id="e658b-236">Or you can query hello catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="e658b-237">**Procédure stockée compilée en mode natif** : vous pouvez inspecter SalesLT.usp_InsertSalesOrder_inmem via une requête de vue de catalogue :</span><span class="sxs-lookup"><span data-stu-id="e658b-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a><span data-ttu-id="e658b-238">Exécuter la charge de travail OLTP hello exemple</span><span class="sxs-lookup"><span data-stu-id="e658b-238">Run hello sample OLTP workload</span></span>

<span data-ttu-id="e658b-239">Hello la seule différence entre hello suivant deux *des procédures stockées* est que la première procédure de hello utilise les versions mémoire optimisées des tables de hello, hello lors de la deuxième procédure utilise les tables sur disque standard hello :</span><span class="sxs-lookup"><span data-stu-id="e658b-239">hello only difference between hello following two *stored procedures* is that hello first procedure uses memory-optimized versions of hello tables, while hello second procedure uses hello regular on-disk tables:</span></span>

- <span data-ttu-id="e658b-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="e658b-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="e658b-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="e658b-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="e658b-242">Dans cette section, vous voyez comment toouse hello pratique **ostress.exe** utilitaire tooexecute hello deux procédures stockées à des niveaux stressants.</span><span class="sxs-lookup"><span data-stu-id="e658b-242">In this section, you see how toouse hello handy **ostress.exe** utility tooexecute hello two stored procedures at stressful levels.</span></span> <span data-ttu-id="e658b-243">Vous pouvez comparer la durée pour hello deux contraintes s’exécute toofinish.</span><span class="sxs-lookup"><span data-stu-id="e658b-243">You can compare how long it takes for hello two stress runs toofinish.</span></span>


<span data-ttu-id="e658b-244">Lorsque vous exécutez ostress.exe, nous recommandons que vous passez des valeurs de paramètre conçus pour les deux éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="e658b-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of hello following:</span></span>

- <span data-ttu-id="e658b-245">Exécuter un grand nombre de connexions simultanées, en utilisant -n100.</span><span class="sxs-lookup"><span data-stu-id="e658b-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="e658b-246">Répéter chaque boucle de connexion une centaine de fois, en utilisant -r500.</span><span class="sxs-lookup"><span data-stu-id="e658b-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="e658b-247">Toutefois, vous pourriez toostart avec beaucoup plus petites valeurs telle que - tooensure n10 et - r 50 que tout fonctionne.</span><span class="sxs-lookup"><span data-stu-id="e658b-247">However, you might want toostart with much smaller values like -n10 and -r50 tooensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="e658b-248">Script pour ostress.exe</span><span class="sxs-lookup"><span data-stu-id="e658b-248">Script for ostress.exe</span></span>


<span data-ttu-id="e658b-249">Cette section affiche le script T-SQL hello qui est incorporé dans notre ligne de commande ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="e658b-249">This section displays hello T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="e658b-250">script de Hello utilise des éléments qui ont été créés par hello script T-SQL que vous avez installé précédemment.</span><span class="sxs-lookup"><span data-stu-id="e658b-250">hello script uses items that were created by hello T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="e658b-251">Hello script suivant insère un exemple de commande client avec cinq éléments de la ligne suivante hello optimisées en mémoire *tables*:</span><span class="sxs-lookup"><span data-stu-id="e658b-251">hello following script inserts a sample sales order with five line items into hello following memory-optimized *tables*:</span></span>

- <span data-ttu-id="e658b-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="e658b-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="e658b-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="e658b-253">SalesLT.SalesOrderDetail_inmem</span></span>


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


<span data-ttu-id="e658b-254">toomake hello *_ondisk* version de hello précédent script T-SQL pour ostress.exe, vous devez remplacer les deux occurrences de hello *_inmem* substring avec *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="e658b-254">toomake hello *_ondisk* version of hello preceding T-SQL script for ostress.exe, you would replace both occurrences of hello *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="e658b-255">Ces remplacements affectent les noms de tables et procédures stockées hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-255">These replacements affect hello names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="e658b-256">Installer les utilitaires RML et ostress</span><span class="sxs-lookup"><span data-stu-id="e658b-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="e658b-257">Dans l’idéal, vous devez prévoir toorun ostress.exe sur une machine virtuelle Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="e658b-257">Ideally, you would plan toorun ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="e658b-258">Vous devez créer un [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) Bonjour même région géographique Azure où se trouve votre base de données AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="e658b-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in hello same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="e658b-259">Vous pouvez aussi exécuter ostress.exe sur votre ordinateur portable.</span><span class="sxs-lookup"><span data-stu-id="e658b-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="e658b-260">Hello machine virtuelle, ou sur tout ce qui hébergent vous choisissez, installez les utilitaires de langage de balisage de relecture (RML) hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-260">On hello VM, or on whatever host you choose, install hello Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="e658b-261">utilitaires de Hello incluent ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="e658b-261">hello utilities include ostress.exe.</span></span>

<span data-ttu-id="e658b-262">Pour plus d'informations, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="e658b-262">For more information, see:</span></span>
- <span data-ttu-id="e658b-263">Hello discussion ostress.exe dans [exemple de base de données pour OLTP en mémoire](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="e658b-263">hello ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="e658b-264">[Exemple de base de données pour OLTP en mémoire](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="e658b-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="e658b-265">Hello [blog pour l’installation de ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="e658b-265">hello [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a><span data-ttu-id="e658b-266">Exécutez hello *_inmem* tout d’abord une contrainte la charge de travail</span><span class="sxs-lookup"><span data-stu-id="e658b-266">Run hello *_inmem* stress workload first</span></span>


<span data-ttu-id="e658b-267">Vous pouvez utiliser un *invite de commandes RML* fenêtre toorun notre ligne de commande ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="e658b-267">You can use an *RML Cmd Prompt* window toorun our ostress.exe command line.</span></span> <span data-ttu-id="e658b-268">paramètres de ligne de commande Hello directe ostress à :</span><span class="sxs-lookup"><span data-stu-id="e658b-268">hello command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="e658b-269">Exécuter 100 connexions simultanément (-n100).</span><span class="sxs-lookup"><span data-stu-id="e658b-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="e658b-270">Chaque connexion exécuter les script T-SQL de hello 50 fois (-r 50).</span><span class="sxs-lookup"><span data-stu-id="e658b-270">Have each connection run hello T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="e658b-271">hello toorun précédant la ligne de commande ostress.exe :</span><span class="sxs-lookup"><span data-stu-id="e658b-271">toorun hello preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="e658b-272">Réinitialiser le contenu des données de base de données hello en exécutant hello suivant de commande dans SSMS, toodelete toutes les données hello qui ont été insérées par les exécutions précédentes :</span><span class="sxs-lookup"><span data-stu-id="e658b-272">Reset hello database data content by running hello following command in SSMS, toodelete all hello data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="e658b-273">Copier le texte hello Hello précédant tooyour du Presse-papiers de la ligne de commande ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="e658b-273">Copy hello text of hello preceding ostress.exe command line tooyour clipboard.</span></span>

3. <span data-ttu-id="e658b-274">Remplacez hello `<placeholders>` pour hello paramètres -S - U -P -d par hello corriger des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="e658b-274">Replace hello `<placeholders>` for hello parameters -S -U -P -d with hello correct real values.</span></span>

4. <span data-ttu-id="e658b-275">Exécutez la ligne de commande que vous avez modifiée dans la fenêtre de commande RML.</span><span class="sxs-lookup"><span data-stu-id="e658b-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="e658b-276">Il en résulte une durée</span><span class="sxs-lookup"><span data-stu-id="e658b-276">Result is a duration</span></span>


<span data-ttu-id="e658b-277">Une fois ostress.exe, il écrit hello durée d’exécution en tant que sa dernière ligne de sortie dans la fenêtre de RML Cmd hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-277">When ostress.exe finishes, it writes hello run duration as its final line of output in hello RML Cmd window.</span></span> <span data-ttu-id="e658b-278">Par exemple, une série de tests plus courte a duré environ 1,5 minute :</span><span class="sxs-lookup"><span data-stu-id="e658b-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="e658b-279">Réinitialisez, paramétrez *_ondisk*, puis procédez à une nouvelle exécution.</span><span class="sxs-lookup"><span data-stu-id="e658b-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="e658b-280">Après avoir résultant de hello hello *_inmem* exécuter, effectuer hello comme suit pour hello *_ondisk* exécuter :</span><span class="sxs-lookup"><span data-stu-id="e658b-280">After you have hello result from hello *_inmem* run, perform hello following steps for hello *_ondisk* run:</span></span>


1. <span data-ttu-id="e658b-281">Réinitialisation de la base de données hello en exécutant hello suivant de commande dans SSMS toodelete toutes les données hello ayant été insérées par hello précédente exécution :</span><span class="sxs-lookup"><span data-stu-id="e658b-281">Reset hello database by running hello following command in SSMS toodelete all hello data that was inserted by hello previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="e658b-282">Modifier tooreplace de ligne de commande hello ostress.exe tous les *_inmem* avec *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="e658b-282">Edit hello ostress.exe command line tooreplace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="e658b-283">Réexécutez ostress.exe pour hello deuxième fois et capturer les résultats de durée hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-283">Rerun ostress.exe for hello second time, and capture hello duration result.</span></span>

4. <span data-ttu-id="e658b-284">Là encore, réinitialisation hello base de données (pour la suppression de façon responsable qui peut être une grande quantité de données de test).</span><span class="sxs-lookup"><span data-stu-id="e658b-284">Again, reset hello database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="e658b-285">Résultats de la comparaison attendus</span><span class="sxs-lookup"><span data-stu-id="e658b-285">Expected comparison results</span></span>

<span data-ttu-id="e658b-286">Nos tests en mémoire ont montré que les performances améliorées par **neuf fois** pour cette charge de travail très simplifiée avec ostress s’exécutant sur une machine virtuelle de Azure dans hello même région Azure en tant que base de données hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in hello same Azure region as hello database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a><span data-ttu-id="e658b-287">2. Installer hello en mémoire Analytique</span><span class="sxs-lookup"><span data-stu-id="e658b-287">2. Install hello In-Memory Analytics sample</span></span>


<span data-ttu-id="e658b-288">Dans cette section, vous comparez hello e/s et les résultats des statistiques lorsque vous utilisez un index columnstore par rapport à un index b-tree traditionnel.</span><span class="sxs-lookup"><span data-stu-id="e658b-288">In this section, you compare hello IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="e658b-289">Pour l’analytique en temps réel sur une charge de travail OLTP, il est souvent de meilleures toouse un index non cluster.</span><span class="sxs-lookup"><span data-stu-id="e658b-289">For real-time analytics on an OLTP workload, it's often best toouse a nonclustered columnstore index.</span></span> <span data-ttu-id="e658b-290">Pour plus d’informations, consultez [Index columnstore décrits](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="e658b-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-hello-columnstore-analytics-test"></a><span data-ttu-id="e658b-291">Préparer hello columnstore analytique test</span><span class="sxs-lookup"><span data-stu-id="e658b-291">Prepare hello columnstore analytics test</span></span>


1. <span data-ttu-id="e658b-292">Utilisez hello toocreate portail Azure une nouvelle base de données AdventureWorksLT à partir de l’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-292">Use hello Azure portal toocreate a fresh AdventureWorksLT database from hello sample.</span></span>
 - <span data-ttu-id="e658b-293">Utilisez ce nom exact.</span><span class="sxs-lookup"><span data-stu-id="e658b-293">Use that exact name.</span></span>
 - <span data-ttu-id="e658b-294">Choisissez un niveau de service Premium.</span><span class="sxs-lookup"><span data-stu-id="e658b-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="e658b-295">Hello de copie [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="e658b-295">Copy hello [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour clipboard.</span></span>
 - <span data-ttu-id="e658b-296">Hello script T-SQL crée des objets en mémoire nécessaire hello hello AdventureWorksLT base de données exemple que vous avez créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="e658b-296">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="e658b-297">script de Hello crée deux tables de faits et de la table de Dimension hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-297">hello script creates hello Dimension table and two fact tables.</span></span> <span data-ttu-id="e658b-298">tables de faits Hello sont renseignées avec 3,5 millions de lignes chacune.</span><span class="sxs-lookup"><span data-stu-id="e658b-298">hello fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="e658b-299">script de Hello peut prendre 15 minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e658b-299">hello script might take 15 minutes toocomplete.</span></span>

3. <span data-ttu-id="e658b-300">Collez le script T-SQL de hello dans SSMS, puis exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-300">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="e658b-301">Hello **COLUMNSTORE** mot clé Bonjour **CREATE INDEX** instruction est cruciale, comme dans :</span><span class="sxs-lookup"><span data-stu-id="e658b-301">hello **COLUMNSTORE** keyword in hello **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="e658b-302">Définir le niveau de toocompatibility AdventureWorksLT 130 :</span><span class="sxs-lookup"><span data-stu-id="e658b-302">Set AdventureWorksLT toocompatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="e658b-303">Niveau 130 n’est pas fonctionnalités tooIn directement lié, en mémoire.</span><span class="sxs-lookup"><span data-stu-id="e658b-303">Level 130 is not directly related tooIn-Memory features.</span></span> <span data-ttu-id="e658b-304">Mais le niveau 130 offre généralement des performances de requêtes supérieures au niveau 120.</span><span class="sxs-lookup"><span data-stu-id="e658b-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="e658b-305">Tables et index columnstore essentiels</span><span class="sxs-lookup"><span data-stu-id="e658b-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="e658b-306">dbo. FactResellerSalesXL_CCI est une table qui possède un index cluster columnstore, qui bénéficie de la compression à hello avancé *données* niveau.</span><span class="sxs-lookup"><span data-stu-id="e658b-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at hello *data* level.</span></span>

- <span data-ttu-id="e658b-307">dbo. FactResellerSalesXL_PageCompressed est une table qui comporte un équivalent index ordonné en clusters standard, qui est compressé uniquement au hello *page* niveau.</span><span class="sxs-lookup"><span data-stu-id="e658b-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at hello *page* level.</span></span>


#### <a name="key-queries-toocompare-hello-columnstore-index"></a><span data-ttu-id="e658b-308">Index de clé requêtes toocompare hello columnstore</span><span class="sxs-lookup"><span data-stu-id="e658b-308">Key queries toocompare hello columnstore index</span></span>


<span data-ttu-id="e658b-309">Il n’y [plusieurs types de requêtes T-SQL que vous pouvez exécuter](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee des améliorations de performances.</span><span class="sxs-lookup"><span data-stu-id="e658b-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee performance improvements.</span></span> <span data-ttu-id="e658b-310">À l’étape 2 dans hello script T-SQL, payer paire de toothis attention de requêtes.</span><span class="sxs-lookup"><span data-stu-id="e658b-310">In step 2 in hello T-SQL script, pay attention toothis pair of queries.</span></span> <span data-ttu-id="e658b-311">Elles diffèrent uniquement d’une ligne :</span><span class="sxs-lookup"><span data-stu-id="e658b-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="e658b-312">Un index cluster columnstore est Bonjour FactResellerSalesXL\_les table CCI.</span><span class="sxs-lookup"><span data-stu-id="e658b-312">A clustered columnstore index is in hello FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="e658b-313">Hello extrait de script T-SQL suivant imprime des statistiques pour les e/s et l’heure de la requête hello de chaque table.</span><span class="sxs-lookup"><span data-stu-id="e658b-313">hello following T-SQL script excerpt prints statistics for IO and TIME for hello query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

<span data-ttu-id="e658b-314">Dans une base de données avec un niveau de tarification hello P2, attendez-vous à neuf fois gain de performances hello pour cette requête à l’aide d’un index columnstore cluster hello par rapport à un index classique hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-314">In a database with hello P2 pricing tier, you can expect about nine times hello performance gain for this query by using hello clustered columnstore index compared with hello traditional index.</span></span> <span data-ttu-id="e658b-315">Avec P15, vous pouvez vous attendre environ 57 fois hello les gains de performance à l’aide des index columnstore de hello.</span><span class="sxs-lookup"><span data-stu-id="e658b-315">With P15, you can expect about 57 times hello performance gain by using hello columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="e658b-316">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e658b-316">Next steps</span></span>

- [<span data-ttu-id="e658b-317">Démarrage rapide 1 : Technologies OLTP en mémoire pour des performances T-SQL plus rapides</span><span class="sxs-lookup"><span data-stu-id="e658b-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="e658b-318">Utiliser OLTP en mémoire dans une application SQL Azure existante</span><span class="sxs-lookup"><span data-stu-id="e658b-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="e658b-319">[Surveiller le stockage OLTP en mémoire](sql-database-in-memory-oltp-monitoring.md) pour l’OLTP en mémoire</span><span class="sxs-lookup"><span data-stu-id="e658b-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e658b-320">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e658b-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="e658b-321">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e658b-321">Deeper information</span></span>

- [<span data-ttu-id="e658b-322">Découvrez comment le Quorum double la charge de travail de la base de données clé tout en réduisant les DTU de 70 %, grâce à l’OLTP en mémoire dans la SQL Database</span><span class="sxs-lookup"><span data-stu-id="e658b-322">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [<span data-ttu-id="e658b-323">Billet de blog OLTP en mémoire dans Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e658b-323">In-Memory OLTP in Azure SQL Database Blog Post</span></span>](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [<span data-ttu-id="e658b-324">En savoir plus sur In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="e658b-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="e658b-325">En savoir plus sur les index columnstore</span><span class="sxs-lookup"><span data-stu-id="e658b-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="e658b-326">En savoir plus sur l’analytique opérationnelle en temps réel</span><span class="sxs-lookup"><span data-stu-id="e658b-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="e658b-327">Consultez [Modèles de charge de travail courants et considérations relatives à la migration](http://msdn.microsoft.com/library/dn673538.aspx) (qui décrit des modèles de charge de travail où l’OLTP en mémoire apporte généralement des gains de performances significatifs)</span><span class="sxs-lookup"><span data-stu-id="e658b-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="e658b-328">Conception des applications</span><span class="sxs-lookup"><span data-stu-id="e658b-328">Application design</span></span>

- [<span data-ttu-id="e658b-329">In-Memory OLTP (optimisation en mémoire)</span><span class="sxs-lookup"><span data-stu-id="e658b-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="e658b-330">Utiliser OLTP en mémoire dans une application SQL Azure existante</span><span class="sxs-lookup"><span data-stu-id="e658b-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="e658b-331">Outils</span><span class="sxs-lookup"><span data-stu-id="e658b-331">Tools</span></span>

- [<span data-ttu-id="e658b-332">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e658b-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="e658b-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="e658b-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="e658b-334">Outils SQL Server Data Tools (SSDT)</span><span class="sxs-lookup"><span data-stu-id="e658b-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
