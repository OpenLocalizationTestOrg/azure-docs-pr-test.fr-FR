---
title: "Technologies Azure SQL Database en mémoire | Microsoft Docs"
description: "Les technologies Azure SQL Database en mémoire améliorent considérablement les performances des charges de travail transactionnelles et analytiques. Apprenez à tirer parti de ces technologies."
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
ms.openlocfilehash: 4cb45551c486263f26947e5684d54b4f2ecc7410
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="3e3cf-104">Optimisation des performances à l’aide des technologies en mémoire dans SQL Database</span><span class="sxs-lookup"><span data-stu-id="3e3cf-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="3e3cf-105">À l’aide des technologies en mémoire dans Azure SQL Database, vous pouvez obtenir des améliorations des performances pour différentes charges de travail : transactionnelles (traitement transactionnel en ligne (OLTP)), analytiques (traitement analytique en ligne (OLAP)) et mixtes (traitement transactionnel/analytique hybride (HTAP)).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="3e3cf-106">Les technologies en mémoire vous aident également à réduire les coûts grâce à un traitement plus efficace des requêtes et des transactions.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-106">Because of the more efficient query and transaction processing, In-Memory technologies also help you to reduce cost.</span></span> <span data-ttu-id="3e3cf-107">En général, il n’est pas nécessaire de mettre à jour le niveau de tarification de la base de données pour obtenir des gains de performances.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-107">You typically don't need to upgrade the pricing tier of the database to achieve performance gains.</span></span> <span data-ttu-id="3e3cf-108">Dans certains cas, vous pourriez même être en mesure de réduire le niveau de tarification, tout en bénéficiant d’une amélioration des performances grâce aux technologies en mémoire.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-108">In some cases, you might even be able reduce the pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="3e3cf-109">Voici deux exemples illustrant comment la technologie OLTP en mémoire a permis d’améliorer les performances :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-109">Here are two examples of how In-Memory OLTP helped to significantly improve performance:</span></span>

- <span data-ttu-id="3e3cf-110">À l’aide de l’OLTP en mémoire, [Quorum Business Solutions a pu doubler leur charge de travail tout en améliorant les DTU de 70 %](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-110">By using In-Memory OLTP, [Quorum Business Solutions was able to double their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="3e3cf-111">DTU signifie *unité de débit de base de données* et inclut une mesure de la consommation des ressources.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="3e3cf-112">La vidéo suivante montre une amélioration significative de la consommation de ressources avec un exemple de charge de travail : [Vidéo OLTP en mémoire dans Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-112">The following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="3e3cf-113">Pour plus d’informations, voir le billet de blog : [Billet de blog OLTP en mémoire dans Azure SQL Database](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="3e3cf-113">For more details, see the blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="3e3cf-114">Les technologies en mémoire sont disponibles dans toutes les bases de données du niveau Premium, notamment les bases de données dans des pools élastiques Premium.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-114">In-Memory technologies are available in all databases in the Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="3e3cf-115">La vidéo suivante explique les gains de performance potentiels que peuvent apporter les technologies en mémoire dans l’Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-115">The following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="3e3cf-116">N’oubliez pas que le gain de performance que vous remarquez dépend de nombreux facteurs, notamment de la nature de la charge de travail et des données, du modèle d’accès de la base de données, etc.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-116">Remember that the performance gain that you see always depends on many factors, including the nature of the workload and data, access pattern of the database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="3e3cf-117">L’Azure SQL Database comprend les technologies en mémoire suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-117">Azure SQL Database has the following In-Memory technologies:</span></span>

- <span data-ttu-id="3e3cf-118">*L’OLTP en mémoire* augmente le débit et réduit la latence de traitement des transactions.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="3e3cf-119">Les scénarios qui bénéficient de l’OLTP en mémoire sont : le traitement de transactions haut débit, notamment les données commerciales et de jeux, l’ingestion de données d’événements ou d’appareils IoT, la mise en cache, le chargement de données, les tables temporaires et les scénarios de variables de table.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="3e3cf-120">Les *index columnstore en cluster* réduisent l’encombrement de stockage (jusqu'à 10 fois) et améliorent les performances des requêtes d’analyse et de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-120">*Clustered columnstore indexes* reduce your storage footprint (up to 10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="3e3cf-121">Vous pouvez les utiliser avec des tables de faits dans vos mini-Data Warehouses pour faire tenir plus de données dans votre base de données et optimiser les performances.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-121">You can use it with fact tables in your data marts to fit more data in your database and improve performance.</span></span> <span data-ttu-id="3e3cf-122">Vous pouvez également les utiliser avec des données historiques dans votre base de données opérationnelles pour archiver et être en mesure d’interroger jusqu’à 10 fois plus de données.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-122">Also, you can use it with historical data in your operational database to archive and be able to query up to 10 times more data.</span></span>
- <span data-ttu-id="3e3cf-123">Les *index columnstore sans cluster* pour HTAP vous aident à obtenir un aperçu en temps réel de votre activité en interrogeant la base de données opérationnelle directement, sans avoir à exécuter de processus d’extraction, de transformation et de chargement (ETL) coûteux et à attendre que l’entrepôt de données se remplisse.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-123">*Nonclustered columnstore indexes* for HTAP help you to gain real-time insights into your business through querying the operational database directly, without the need to run an expensive extract, transform, and load (ETL) process and wait for the data warehouse to be populated.</span></span> <span data-ttu-id="3e3cf-124">Les index columnstore sans cluster permettent une exécution très rapide des requêtes d’analyse sur la base de données OLTP, tout en réduisant l’impact sur la charge de travail opérationnelle.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on the OLTP database, while reducing the impact on the operational workload.</span></span>
- <span data-ttu-id="3e3cf-125">Vous pouvez également disposer de la combinaison d’une table à mémoire optimisée et d’un index columnstore.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-125">You can also have the combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="3e3cf-126">Cette combinaison permet d’effectuer un traitement transactionnel très rapide, et permet d’exécuter *simultanément* et très rapidement des requêtes Analytics sur les mêmes données.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-126">This combination enables you to perform very fast transaction processing, and to *concurrently* run analytics queries very quickly on the same data.</span></span>

<span data-ttu-id="3e3cf-127">Les index columnstore et la technologie OLTP en mémoire sont inclus dans le produit SQL Server respectivement depuis 2012 et 2014.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-127">Both columnstore indexes and In-Memory OLTP have been part of the SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="3e3cf-128">Azure SQL Database et SQL Server partagent la même implémentation des technologies en mémoire.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-128">Azure SQL Database and SQL Server share the same implementation of In-Memory technologies.</span></span> <span data-ttu-id="3e3cf-129">À l’avenir, les nouvelles fonctionnalités pour ces technologies seront publiées dans Azure SQL Database avant d’être publiées dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="3e3cf-130">Cette rubrique décrit des aspects de l’OLTP en mémoire et des index columnstore qui sont spécifiques à Azure SQL Database, et inclut également des exemples :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific to Azure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="3e3cf-131">Vous verrez l’impact de ces technologies sur le stockage et les limites de taille des données.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-131">You'll see the impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="3e3cf-132">Vous verrez ensuite comment gérer le déplacement de bases de données qui exploitent ces technologies entre les différents niveaux tarifaires.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-132">You'll see how to manage the movement of databases that use these technologies between the different pricing tiers.</span></span>
- <span data-ttu-id="3e3cf-133">Vous verrez deux exemples qui illustrent l’utilisation d’OLTP en mémoire, ainsi que les index columnstore dans la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-133">You'll see two samples that illustrate the use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="3e3cf-134">Pour plus d’informations, consultez les ressources suivantes.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-134">See the following resources for more information.</span></span>

<span data-ttu-id="3e3cf-135">Informations approfondies sur ces technologies :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-135">In-depth information about the technologies:</span></span>

- <span data-ttu-id="3e3cf-136">[Présentation de l’OLTP en mémoire et scénarios d’utilisation](https://msdn.microsoft.com/library/mt774593.aspx) (avec notamment des références à des études de cas client et des informations de prise en main)</span><span class="sxs-lookup"><span data-stu-id="3e3cf-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references to customer case studies and information to get started)</span></span>
- [<span data-ttu-id="3e3cf-137">Documentation pour l’OLTP In-Memory</span><span class="sxs-lookup"><span data-stu-id="3e3cf-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="3e3cf-138">Description des index columnstore</span><span class="sxs-lookup"><span data-stu-id="3e3cf-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="3e3cf-139">Traitement hybride transactionnel et analytique (HTAP), également appelé [analytique opérationnelle en temps réel](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="3e3cf-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="3e3cf-140">Introduction rapide sur l’OLTP en mémoire : [Démarrage rapide 1 : Technologies OLTP en mémoire pour des performances T-SQL plus rapides](http://msdn.microsoft.com/library/mt694156.aspx) (un autre article pour vous aider à commencer)</span><span class="sxs-lookup"><span data-stu-id="3e3cf-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article to help you get started)</span></span>

<span data-ttu-id="3e3cf-141">Vidéos détaillées sur les technologies :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-141">In-depth videos about the technologies:</span></span>

- <span data-ttu-id="3e3cf-142">[OLTP en mémoire dans Azure DQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (avec notamment une démonstration des avantages de performances et les étapes à suivre pour reproduire ces résultats vous-même)</span><span class="sxs-lookup"><span data-stu-id="3e3cf-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps to reproduce these results yourself)</span></span>
- [<span data-ttu-id="3e3cf-143">Vidéos sur l’OLTP en mémoire : qu’est-ce que c’est, et comment l’utiliser</span><span class="sxs-lookup"><span data-stu-id="3e3cf-143">In-Memory OLTP Videos: What it is and When/How to use it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="3e3cf-144">Index Columnstore : vidéos d’analyse en mémoire d’Ignite 2016</span><span class="sxs-lookup"><span data-stu-id="3e3cf-144">Columnstore Index: In-Memory Analytics Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="3e3cf-145">Taille des données et du stockage</span><span class="sxs-lookup"><span data-stu-id="3e3cf-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="3e3cf-146">Seuil de la taille des données et du stockage pour l’OLTP en mémoire</span><span class="sxs-lookup"><span data-stu-id="3e3cf-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="3e3cf-147">l’OLTP en mémoire inclut des tables optimisées en mémoire, qui sont utilisées pour stocker des données de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="3e3cf-148">Le volume de ces tables doit tenir dans la mémoire.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-148">These tables are required to fit in memory.</span></span> <span data-ttu-id="3e3cf-149">Étant donné que vous gérez la mémoire directement dans le service SQL Database, nous disposons du concept de quota pour les données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-149">Because you manage memory directly in the SQL Database service, we have the  concept of a quota for user data.</span></span> <span data-ttu-id="3e3cf-150">Ce concept est appelé *stockage OLTP en mémoire*.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-150">This idea is referred to as *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="3e3cf-151">Chaque niveau tarifaire de base de données autonome pris en charge et chaque niveau tarifaire de pool élastique inclut une certaine quantité de stockage OLTP en mémoire.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="3e3cf-152">Au moment de l’écriture de cet article, vous obtenez un gigaoctet de stockage pour 125 unités de transaction de base de données (DTU) ou unités de transaction de base de données élastique (eDTU).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-152">At the time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="3e3cf-153">L’article [Niveaux de service SQL Database](sql-database-service-tiers.md) contient la liste officielle de stockage OLTP en mémoire disponible pour chaque niveau tarifaire de base de données autonome et de pool élastique pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-153">The [SQL Database service tiers](sql-database-service-tiers.md) article has the official list of the In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="3e3cf-154">Les éléments suivants sont pris en compte dans votre plafond de stockage OLTP en mémoire :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-154">The following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="3e3cf-155">Lignes de données utilisateur actives dans des tables optimisées en mémoire et variables de table.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="3e3cf-156">Notez que les anciennes versions des lignes ne comptent pas dans le seuil.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-156">Note that old row versions don't count toward the cap.</span></span>
- <span data-ttu-id="3e3cf-157">Index de tables optimisées en mémoire.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="3e3cf-158">Coûts de fonctionnement des opérations ALTER TABLE.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="3e3cf-159">Si vous atteignez le seuil, vous recevrez une erreur de quota et vous ne serez plus en mesure d’insérer ou de mettre à jour des données.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-159">If you hit the cap, you receive an out-of-quota error, and you are no longer able to insert or update data.</span></span> <span data-ttu-id="3e3cf-160">Pour atténuer cette erreur, supprimez des données ou augmentez le niveau tarifaire de la base de données ou du pool.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-160">To mitigate this error, delete data or increase the pricing tier of the database or pool.</span></span>

<span data-ttu-id="3e3cf-161">Pour plus d’informations sur la surveillance de l’utilisation du stockage OLTP en mémoire et la configuration des alertes lorsque le seuil est presque atteint, consultez [Surveiller le stockage en mémoire](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit the cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="3e3cf-162">À propos des pools élastiques</span><span class="sxs-lookup"><span data-stu-id="3e3cf-162">About elastic pools</span></span>

<span data-ttu-id="3e3cf-163">Avec les pools élastiques, le stockage OLTP en mémoire est partagé entre toutes les bases de données dans le pool.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-163">With elastic pools, the In-Memory OLTP storage is shared across all databases in the pool.</span></span> <span data-ttu-id="3e3cf-164">Par conséquent, l’utilisation dans une base de données peut potentiellement affecter les autres bases de données.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-164">Therefore, the usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="3e3cf-165">Voici deux solutions :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="3e3cf-166">Configurez un nombre d’eDTU maximal pour les bases de données inférieur au nombre d’eDTU du pool dans son ensemble.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-166">Configure a Max-eDTU for databases that is lower than the eDTU count for the pool as a whole.</span></span> <span data-ttu-id="3e3cf-167">Cette valeur maximale limite l’utilisation du stockage OLTP en mémoire, dans n’importe quelle base de données du pool, à la taille qui correspond au nombre d’eDTU.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-167">This maximum caps the In-Memory OLTP storage utilization, in any database in the pool, to the size that corresponds to the eDTU count.</span></span>
- <span data-ttu-id="3e3cf-168">Configurez un nombre d’eDTU minimal supérieur à 0.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="3e3cf-169">Ce minimum garantit que chaque base de données dans le pool possède la quantité de stockage OLTP en mémoire disponible qui correspond à l’eDTU-Min configuré.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-169">This minimum guarantees that each database in the pool has the amount of available In-Memory OLTP storage that corresponds to the configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="3e3cf-170">Taille des données et stockage pour les index columnstore</span><span class="sxs-lookup"><span data-stu-id="3e3cf-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="3e3cf-171">Le volume des index columntore ne doit pas forcément tenir dans la mémoire.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-171">Columnstore indexes aren't required to fit in memory.</span></span> <span data-ttu-id="3e3cf-172">Par conséquent, le seul seuil de taille des index est la taille de base de données globale maximale décrite dans l’article [Niveaux de service SQL Database](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-172">Therefore, the only cap on the size of the indexes is the maximum overall database size, which is documented in the [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="3e3cf-173">Lors de l’utilisation d’index columnstore en cluster, la compression en colonnes est utilisée pour le stockage de table de base.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-173">When you use clustered columnstore indexes, columnar compression is used for the base table storage.</span></span> <span data-ttu-id="3e3cf-174">Cette compression peut réduire considérablement l’encombrement de stockage des données utilisateur, ce qui signifie que vous pouvez entrer davantage de données dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-174">This compression can significantly reduce the storage footprint of your user data, which means that you can fit more data in the database.</span></span> <span data-ttu-id="3e3cf-175">De plus, la compression peut être accrue d’avantage avec [la compression d’archivage en colonnes](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-175">And the compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="3e3cf-176">Le taux de compression que vous pouvez obtenir dépend de la nature des données, mais une compression égale à 10 fois n’est pas rare.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-176">The amount of compression that you can achieve depends on the nature of the data, but 10 times the compression is not uncommon.</span></span>

<span data-ttu-id="3e3cf-177">Par exemple, si vous disposez d’une base de données avec une taille maximale de 1 téraoctet (To), et que vous atteignez une compression de 10 fois à l’aide d’index columntore, vous pouvez afficher un total de 10 To de données utilisateur dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times the compression by using columnstore indexes, you can fit a total of 10 TB of user data in the database.</span></span>

<span data-ttu-id="3e3cf-178">Lors de l’utilisation d’index columnstore sans cluster, la table de base est toujours stockée au format rowstore traditionnel.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-178">When you use nonclustered columnstore indexes, the base table is still stored in the traditional rowstore format.</span></span> <span data-ttu-id="3e3cf-179">Par conséquent, les économies en stockage ne sont pas aussi importantes qu’avec des index columnstore en cluster.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-179">Therefore, the storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="3e3cf-180">Toutefois, si vous remplacez un nombre d’index sans cluster traditionnels par un index columntore unique, vous pouvez toujours voir une économie globale d’espace de stockage pour la table.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in the storage footprint for the table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="3e3cf-181">Déplacement de bases de données utilisant des technologies en mémoire entre différents niveaux tarifaires</span><span class="sxs-lookup"><span data-stu-id="3e3cf-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="3e3cf-182">Vous ne rencontrerez aucune incompatibilité ou aucun autre problème lorsque vous effectuerez une mise à niveau vers un niveau tarifaire supérieur (ex : Édition Standard vers Édition Premium).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-182">There are never any incompatibilities or other problems when you upgrade to a higher pricing tier, such as from Standard to Premium.</span></span> <span data-ttu-id="3e3cf-183">Les ressources et les fonctionnalités disponibles ne font qu’augmenter.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-183">The available functionality and resources only increase.</span></span>

<span data-ttu-id="3e3cf-184">Cependant la rétrogradation du niveau de tarification peut affecter négativement votre base de données.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-184">But downgrading the pricing tier can negatively impact your database.</span></span> <span data-ttu-id="3e3cf-185">L’impact est particulièrement évident lorsque vous rétrogradez à partir de Premium pour Base ou Standard alors que votre base de données contient des objets de l’OLTP en mémoire.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-185">The impact is especially apparent when you downgrade from Premium to Standard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="3e3cf-186">Les tables à mémoire optimisée et les index columnstore sont indisponibles après la rétrogradation (même si elles restent visibles).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-186">Memory-optimized tables, and columnstore indexes, are unavailable after the downgrade (even if they remain visible).</span></span> <span data-ttu-id="3e3cf-187">Les mêmes considérations s’appliquent lors de la réduction du niveau tarifaire d’un pool élastique ou du déplacement d’une base de données avec des technologies en mémoire vers un pool élastique Standard ou de base.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-187">The same considerations apply when you're lowering the pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="3e3cf-188">OLTP In-Memory.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-188">In-Memory OLTP</span></span>

<span data-ttu-id="3e3cf-189">*Rétrogradation vers le niveau De base/Standard* : l’OLTP en mémoire n’est pas pris en charge dans des bases de données de niveau standard ou de base.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-189">*Downgrading to Basic/Standard*: In-Memory OLTP isn't supported in databases in the Standard or Basic tier.</span></span> <span data-ttu-id="3e3cf-190">En outre, il n’est pas possible de déplacer une base de données qui comporte des objets OLTP en mémoire vers un niveau standard ou de base.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-190">In addition, it isn't possible to move a database that has any In-Memory OLTP objects to the Standard or Basic tier.</span></span>

<span data-ttu-id="3e3cf-191">Avant de rétrograder la base de données vers un niveau standard/de base, supprimez toutes les tables à mémoire optimisée et tous les types de table, ainsi que tous les modules T-SQL compilés en mode natif.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-191">Before you downgrade the database to Standard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="3e3cf-192">Vous pouvez comprendre par programmation si une base de données spécifique prend en charge l’OLTP en mémoire.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-192">There is a programmatic way to understand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="3e3cf-193">Vous pouvez exécuter la requête Transact-SQL suivante :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-193">You can execute the following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="3e3cf-194">Si la requête renvoie **1**, l’OLTP en mémoire est pris en charge dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-194">If the query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="3e3cf-195">*Rétrogradation vers un niveau Premium inférieur* : les données dans des tables à mémoire optimisée doivent tenir dans le stockage OLTP en mémoire qui est associé au niveau tarifaire de la base de données ou disponible dans le pool élastique.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-195">*Downgrading to a lower Premium tier*: Data in memory-optimized tables must fit within the In-Memory OLTP storage that is associated with the pricing tier of the database or is available in the elastic pool.</span></span> <span data-ttu-id="3e3cf-196">L’opération échoue si vous tentez de réduire le niveau tarifaire ou de déplacer la base de données dans un pool qui ne dispose pas d’un stockage OLTP en mémoire suffisant.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-196">If you try to lower the pricing tier or move the database into a pool that doesn't have enough available In-Memory OLTP storage, the operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="3e3cf-197">Index Columnstore</span><span class="sxs-lookup"><span data-stu-id="3e3cf-197">Columnstore indexes</span></span>

<span data-ttu-id="3e3cf-198">*Rétrogradation vers Base ou Standard* : les index columnstore ne sont pris en charge que sur le niveau tarifaire Premium et non sur les niveaux Standard ou Basic.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-198">*Downgrading to Basic or Standard*: Columnstore indexes are supported only on the Premium pricing tier, and not on the Standard or Basic tiers.</span></span> <span data-ttu-id="3e3cf-199">Lors de la rétrogradation de votre base de données vers Standard ou Base, l’index columnstore devient indisponible.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-199">When you downgrade your database to Standard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="3e3cf-200">Le système maintient l’index columnstore, mais il ne tire jamais profit de l’index.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-200">The system maintains your columnstore index, but it never leverages the index.</span></span> <span data-ttu-id="3e3cf-201">Si vous mettez à niveau ultérieurement vers Premium, l’index columnstore est immédiatement prêt à être exploité à nouveau.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-201">If you later upgrade back to Premium, your columnstore index is immediately ready to be leveraged again.</span></span>

<span data-ttu-id="3e3cf-202">Si vous disposez d’un index columnstore **mis en cluster**, la totalité de la table devient indisponible après la rétrogradation de la couche.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-202">If you have a **clustered** columnstore index, the whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="3e3cf-203">Par conséquent, nous vous recommandons d’annuler tous les index columnstore *mis en index* avant de rétrograder votre base de données sous le niveau Premium.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below the Premium tier.</span></span>

<span data-ttu-id="3e3cf-204">*Rétrogradation vers un niveau Premium inférieur* : cette opération réussit tant que la taille de base de données dans son ensemble est inférieure à la taille de base de données maximale correspondant au niveau tarifaire cible ou au stockage disponible dans le pool élastique.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-204">*Downgrading to a lower Premium tier*: This downgrade succeeds if the whole database fits within the maximum database size for the target pricing tier, or within the available storage in the elastic pool.</span></span> <span data-ttu-id="3e3cf-205">Les index columnstore n’ont aucune incidence spécifique.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-205">There is no specific impact from the columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-the-in-memory-oltp-sample"></a><span data-ttu-id="3e3cf-206">1. Installer l’exemple In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="3e3cf-206">1. Install the In-Memory OLTP sample</span></span>

<span data-ttu-id="3e3cf-207">Vous pouvez créer l’exemple de base de données AdventureWorksLT en quelques clics dans le [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-207">You can create the AdventureWorksLT sample database with a few clicks in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="3e3cf-208">Les étapes de cette section expliquent comment enrichir votre base de données AdventureWorksLT d’objets OLTP en mémoire et démontrent les avantages au niveau des performances.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-208">Then, the steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="3e3cf-209">Pour une démonstration plus simple mais intéressante des performances de l’OLTP en mémoire, consultez :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="3e3cf-210">Version : [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="3e3cf-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="3e3cf-211">Code source : [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="3e3cf-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="3e3cf-212">Procédure d’installation :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-212">Installation steps</span></span>

1. <span data-ttu-id="3e3cf-213">Dans le [portail Azure](https://portal.azure.com/), créez une base de données Premium sur un serveur.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-213">In the [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="3e3cf-214">Définissez comme valeur **Source** l’exemple de base de données AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-214">Set the **Source** to the AdventureWorksLT sample database.</span></span> <span data-ttu-id="3e3cf-215">Pour obtenir des instructions détaillées, consultez [Créer votre première base de données SQL Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="3e3cf-216">Connectez-vous à la base de données avec [SQL Server Management Studio (SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-216">Connect to the database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="3e3cf-217">Copiez le [script In-Memory OLTP Transact-SQL](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-217">Copy the [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) to your clipboard.</span></span> <span data-ttu-id="3e3cf-218">Le script T-SQL crée les objets en mémoire nécessaires dans l’exemple de base de données AdventureWorksLT créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-218">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="3e3cf-219">Collez le script T-SQL dans SSMS, puis exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-219">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="3e3cf-220">Les instructions CREATE TABLE de la clause `MEMORY_OPTIMIZED = ON` sont essentielles.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-220">The `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="3e3cf-221">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="3e3cf-222">Erreur 40536</span><span class="sxs-lookup"><span data-stu-id="3e3cf-222">Error 40536</span></span>


<span data-ttu-id="3e3cf-223">Si vous obtenez une erreur 40536 lorsque vous exécutez le script T-SQL, exécutez le script T-SQL suivant pour vérifier que la base de données prend en charge In-Memory :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-223">If you get error 40536 when you run the T-SQL script, run the following T-SQL script to verify whether the database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="3e3cf-224">Un résultat de **0** signifie que la technologie en mémoire n’est pas prise en charge, et un résultat de **1** signifie qu’elle l’est.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="3e3cf-225">Pour diagnostiquer le problème, vérifiez que la base de données se trouve sur le niveau de service Premium.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-225">To diagnose the problem, ensure that the database is at the Premium service tier.</span></span>


#### <a name="about-the-created-memory-optimized-items"></a><span data-ttu-id="3e3cf-226">À propos des éléments créés à mémoire optimisée.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-226">About the created memory-optimized items</span></span>

<span data-ttu-id="3e3cf-227">**Tables**: l’exemple contient les tables à mémoire optimisée suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-227">**Tables**: The sample contains the following memory-optimized tables:</span></span>

- <span data-ttu-id="3e3cf-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="3e3cf-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="3e3cf-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="3e3cf-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="3e3cf-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="3e3cf-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="3e3cf-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="3e3cf-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="3e3cf-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="3e3cf-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="3e3cf-233">Vous pouvez inspecter les tables à mémoire optimisée via **l’Explorateur d’objets** dans SSMS.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-233">You can inspect memory-optimized tables through the **Object Explorer** in SSMS.</span></span> <span data-ttu-id="3e3cf-234">Cliquez avec le bouton droit sur **Tables** > **Filtre** > **Paramètres de filtre** > **Est à mémoire optimisée**.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="3e3cf-235">La valeur est égale à 1.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-235">The value equals 1.</span></span>


<span data-ttu-id="3e3cf-236">Vous pouvez aussi interroger les vues de catalogue, telles que :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-236">Or you can query the catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="3e3cf-237">**Procédure stockée compilée en mode natif** : vous pouvez inspecter SalesLT.usp_InsertSalesOrder_inmem via une requête de vue de catalogue :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-the-sample-oltp-workload"></a><span data-ttu-id="3e3cf-238">Exécuter l’exemple de charge de travail OLTP</span><span class="sxs-lookup"><span data-stu-id="3e3cf-238">Run the sample OLTP workload</span></span>

<span data-ttu-id="3e3cf-239">La seule différence entre les deux *procédures stockées* est que la première utilise les versions à mémoire optimisée des tables, tandis que la deuxième utilise les tables sur disque régulières :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-239">The only difference between the following two *stored procedures* is that the first procedure uses memory-optimized versions of the tables, while the second procedure uses the regular on-disk tables:</span></span>

- <span data-ttu-id="3e3cf-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="3e3cf-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="3e3cf-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="3e3cf-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="3e3cf-242">Dans cette section, vous apprendrez à utiliser l’utilitaire **ostress.exe** , pratique pour exécuter les deux procédures stockées à des niveaux de contrainte élevés.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-242">In this section, you see how to use the handy **ostress.exe** utility to execute the two stored procedures at stressful levels.</span></span> <span data-ttu-id="3e3cf-243">Vous pouvez comparer le temps d’exécution des deux contraintes.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-243">You can compare how long it takes for the two stress runs to finish.</span></span>


<span data-ttu-id="3e3cf-244">Lorsque vous exécutez ostress.exe, nous vous recommandons de transmettre des valeurs de paramètre conçues pour :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of the following:</span></span>

- <span data-ttu-id="3e3cf-245">Exécuter un grand nombre de connexions simultanées, en utilisant -n100.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="3e3cf-246">Répéter chaque boucle de connexion une centaine de fois, en utilisant -r500.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="3e3cf-247">Toutefois, vous pouvez commencer avec des valeurs plus petites, telles que -n10 et -r50 pour vous assurer que tout fonctionne.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-247">However, you might want to start with much smaller values like -n10 and -r50 to ensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="3e3cf-248">Script pour ostress.exe</span><span class="sxs-lookup"><span data-stu-id="3e3cf-248">Script for ostress.exe</span></span>


<span data-ttu-id="3e3cf-249">Cette section affiche le script T-SQL incorporé à la ligne de commande ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-249">This section displays the T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="3e3cf-250">Le script utilise des éléments créés par le script T-SQL installé précédemment.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-250">The script uses items that were created by the T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="3e3cf-251">Le script suivant insère un exemple de commande client avec cinq lignes dans les *tables*à mémoire optimisée suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-251">The following script inserts a sample sales order with five line items into the following memory-optimized *tables*:</span></span>

- <span data-ttu-id="3e3cf-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="3e3cf-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="3e3cf-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="3e3cf-253">SalesLT.SalesOrderDetail_inmem</span></span>


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


<span data-ttu-id="3e3cf-254">Pour créer la version *_ondisk* du script T-SQL précédent pour ostress.exe, il suffit de remplacer les deux occurrences de la sous-chaîne *_inmem* par *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-254">To make the *_ondisk* version of the preceding T-SQL script for ostress.exe, you would replace both occurrences of the *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="3e3cf-255">Ces remplacements affectent les noms des tables et des procédures stockées.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-255">These replacements affect the names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="3e3cf-256">Installer les utilitaires RML et ostress</span><span class="sxs-lookup"><span data-stu-id="3e3cf-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="3e3cf-257">Dans l’idéal, vous devez prévoir d’exécuter ostress.exe sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-257">Ideally, you would plan to run ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="3e3cf-258">Vous devez créer une [machine virtuelle Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) dans la même région géographique Azure que celle où se trouve votre base de données AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in the same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="3e3cf-259">Vous pouvez aussi exécuter ostress.exe sur votre ordinateur portable.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="3e3cf-260">Sur la machine virtuelle (ou sur l’hôte que vous avez choisi d’utiliser), installez les utilitaires RML.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-260">On the VM, or on whatever host you choose, install the Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="3e3cf-261">Ceux-ci incluent ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-261">The utilities include ostress.exe.</span></span>

<span data-ttu-id="3e3cf-262">Pour plus d'informations, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-262">For more information, see:</span></span>
- <span data-ttu-id="3e3cf-263">La discussion sur ostress.exe dans [Exemple de base de données pour OLTP en mémoire](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-263">The ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="3e3cf-264">[Exemple de base de données pour OLTP en mémoire](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="3e3cf-265">Le [blog pour l’installation de ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-265">The [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions to AdventureWorks to Demonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-the-inmem-stress-workload-first"></a><span data-ttu-id="3e3cf-266">Commencer par exécuter la charge de travail de contrainte *_inmem*</span><span class="sxs-lookup"><span data-stu-id="3e3cf-266">Run the *_inmem* stress workload first</span></span>


<span data-ttu-id="3e3cf-267">Vous pouvez utiliser une fenêtre d’ *invite de commande RML* pour exécuter la ligne de commande ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-267">You can use an *RML Cmd Prompt* window to run our ostress.exe command line.</span></span> <span data-ttu-id="3e3cf-268">Les paramètres de ligne de commande indiquent à ostress d’effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-268">The command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="3e3cf-269">Exécuter 100 connexions simultanément (-n100).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="3e3cf-270">Chaque connexion doit exécuter le script T-SQL 50 fois (-r50).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-270">Have each connection run the T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="3e3cf-271">Pour exécuter la ligne de commande ostress.exe précédente :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-271">To run the preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="3e3cf-272">Réinitialisez le contenu de la base de données en exécutant la commande suivante dans SSMS, pour supprimer toutes les données insérées lors des exécutions précédentes :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-272">Reset the database data content by running the following command in SSMS, to delete all the data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="3e3cf-273">Copiez le texte de la ligne de commande ostress.exe qui précède dans le presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-273">Copy the text of the preceding ostress.exe command line to your clipboard.</span></span>

3. <span data-ttu-id="3e3cf-274">Remplacez le `<placeholders>` des paramètres -S - U -P -d par les valeurs réelles correctes.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-274">Replace the `<placeholders>` for the parameters -S -U -P -d with the correct real values.</span></span>

4. <span data-ttu-id="3e3cf-275">Exécutez la ligne de commande que vous avez modifiée dans la fenêtre de commande RML.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="3e3cf-276">Il en résulte une durée</span><span class="sxs-lookup"><span data-stu-id="3e3cf-276">Result is a duration</span></span>


<span data-ttu-id="3e3cf-277">Lorsque ostress.exe est terminé, la durée d’exécution est indiquée sur la dernière ligne de sortie dans la fenêtre de commande RML.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-277">When ostress.exe finishes, it writes the run duration as its final line of output in the RML Cmd window.</span></span> <span data-ttu-id="3e3cf-278">Par exemple, une série de tests plus courte a duré environ 1,5 minute :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="3e3cf-279">Réinitialisez, paramétrez *_ondisk*, puis procédez à une nouvelle exécution.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="3e3cf-280">Une fois le résultat de l’exécution de *_inmem* obtenu, effectuez les opérations suivantes pour l’exécution de *_ondisk* :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-280">After you have the result from the *_inmem* run, perform the following steps for the *_ondisk* run:</span></span>


1. <span data-ttu-id="3e3cf-281">Réinitialisez la base de données en exécutant la commande suivante dans SSMS pour supprimer toutes les données insérées lors de l’exécution précédente :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-281">Reset the database by running the following command in SSMS to delete all the data that was inserted by the previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="3e3cf-282">Modifiez la ligne de commande ostress.exe pour remplacer toutes les occurrences de *_inmem* par *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-282">Edit the ostress.exe command line to replace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="3e3cf-283">Réexécutez ostress.exe une deuxième fois, puis enregistrez le résultat de durée.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-283">Rerun ostress.exe for the second time, and capture the duration result.</span></span>

4. <span data-ttu-id="3e3cf-284">Réinitialisez à nouveau la base de données (pour supprimer une quantité de données de test qui peut s’avérer conséquente).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-284">Again, reset the database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="3e3cf-285">Résultats de la comparaison attendus</span><span class="sxs-lookup"><span data-stu-id="3e3cf-285">Expected comparison results</span></span>

<span data-ttu-id="3e3cf-286">Nos tests en mémoire montrent une multiplication par **9** de l’amélioration des performances pour cette charge de travail simple, avec ostress s’exécutant sur une machine virtuelle Azure dans la même région Azure que la base de données.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in the same Azure region as the database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-the-in-memory-analytics-sample"></a><span data-ttu-id="3e3cf-287">2. Installer l’exemple In-Memory Analytics</span><span class="sxs-lookup"><span data-stu-id="3e3cf-287">2. Install the In-Memory Analytics sample</span></span>


<span data-ttu-id="3e3cf-288">Dans cette section, vous comparez les résultats des statistiques et les résultats d’E/S lors de l’utilisation d’un index columnstore par rapport à un index d’arborescence B traditionnel.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-288">In this section, you compare the IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="3e3cf-289">Pour l’analyse en temps réel sur une charge de travail OLTP, il est souvent préférable d’utiliser un index columnstore sans cluster.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-289">For real-time analytics on an OLTP workload, it's often best to use a nonclustered columnstore index.</span></span> <span data-ttu-id="3e3cf-290">Pour plus d’informations, consultez [Index columnstore décrits](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e3cf-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-the-columnstore-analytics-test"></a><span data-ttu-id="3e3cf-291">Préparer le test d’analyse columnstore</span><span class="sxs-lookup"><span data-stu-id="3e3cf-291">Prepare the columnstore analytics test</span></span>


1. <span data-ttu-id="3e3cf-292">Utilisez le portail Azure pour créer une base de données AdventureWorksLT à partir de l’exemple.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-292">Use the Azure portal to create a fresh AdventureWorksLT database from the sample.</span></span>
 - <span data-ttu-id="3e3cf-293">Utilisez ce nom exact.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-293">Use that exact name.</span></span>
 - <span data-ttu-id="3e3cf-294">Choisissez un niveau de service Premium.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="3e3cf-295">Copiez [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-295">Copy the [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) to your clipboard.</span></span>
 - <span data-ttu-id="3e3cf-296">Le script T-SQL crée les objets en mémoire nécessaires dans l’exemple de base de données AdventureWorksLT créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-296">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="3e3cf-297">Le script crée la table Dimension et deux tables de faits.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-297">The script creates the Dimension table and two fact tables.</span></span> <span data-ttu-id="3e3cf-298">Les tables de faits comprennent 3,5 millions de lignes chacune.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-298">The fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="3e3cf-299">Le script peut prendre 15 minutes pour s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-299">The script might take 15 minutes to complete.</span></span>

3. <span data-ttu-id="3e3cf-300">Collez le script T-SQL dans SSMS, puis exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-300">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="3e3cf-301">Le mot clé **COLUMNSTORE** est essentiel dans l’instruction **CREATE INDEX**, comme dans l’exemple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-301">The **COLUMNSTORE** keyword in the **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="3e3cf-302">Définissez AdventureWorksLT sur le niveau de compatibilité 130 :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-302">Set AdventureWorksLT to compatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="3e3cf-303">Le niveau 130 n’est pas directement lié aux fonctionnalités In-Memory.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-303">Level 130 is not directly related to In-Memory features.</span></span> <span data-ttu-id="3e3cf-304">Mais le niveau 130 offre généralement des performances de requêtes supérieures au niveau 120.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="3e3cf-305">Tables et index columnstore essentiels</span><span class="sxs-lookup"><span data-stu-id="3e3cf-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="3e3cf-306">dbo.FactResellerSalesXL_CCI est une table contenant un index columnstore en cluster, ce qui permet la compression avancée au niveau des *données*.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at the *data* level.</span></span>

- <span data-ttu-id="3e3cf-307">dbo.FactResellerSalesXL_PageCompressed est une table qui possède un index en cluster régulier équivalent, compressé uniquement au niveau de la *page*.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at the *page* level.</span></span>


#### <a name="key-queries-to-compare-the-columnstore-index"></a><span data-ttu-id="3e3cf-308">Requêtes essentielles pour comparer l’index columnstore</span><span class="sxs-lookup"><span data-stu-id="3e3cf-308">Key queries to compare the columnstore index</span></span>


<span data-ttu-id="3e3cf-309">Il existe [plusieurs types de requête T-SQL que vous pouvez exécuter](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) pour mettre en évidence les améliorations des performances.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) to see performance improvements.</span></span> <span data-ttu-id="3e3cf-310">À l’étape 2 dans le script T-SQL, soyez attentif à ces deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-310">In step 2 in the T-SQL script, pay attention to this pair of queries.</span></span> <span data-ttu-id="3e3cf-311">Elles diffèrent uniquement d’une ligne :</span><span class="sxs-lookup"><span data-stu-id="3e3cf-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="3e3cf-312">Un index columnstore en cluster se trouve dans la table FactResellerSalesXL\_CCI.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-312">A clustered columnstore index is in the FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="3e3cf-313">L’extrait de script T-SQL suivant imprime des statistiques d’E/S et d’heure pour la requête de chaque table.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-313">The following T-SQL script excerpt prints statistics for IO and TIME for the query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order to see Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins the Fact Table with dimension tables
-- Note this query will run on the Page Compressed table, Note down the time
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


-- This is the same Prior query on a table with a clustered columnstore index CCI
-- The comparison numbers are even more dramatic the larger the table is (this is an 11 million row table only)
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

<span data-ttu-id="3e3cf-314">Dans une base de données ayant le niveau tarifaire P2, vous pouvez attendre une multiplication par 9 des performances de cette requête avec l’index columnstore en cluster par rapport à l’index traditionnel.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-314">In a database with the P2 pricing tier, you can expect about nine times the performance gain for this query by using the clustered columnstore index compared with the traditional index.</span></span> <span data-ttu-id="3e3cf-315">Avec P15, vous pouvez vous attendre à une multiplication des performances par 57 à l’aide de l’index columnstore.</span><span class="sxs-lookup"><span data-stu-id="3e3cf-315">With P15, you can expect about 57 times the performance gain by using the columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="3e3cf-316">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3e3cf-316">Next steps</span></span>

- [<span data-ttu-id="3e3cf-317">Démarrage rapide 1 : Technologies OLTP en mémoire pour des performances T-SQL plus rapides</span><span class="sxs-lookup"><span data-stu-id="3e3cf-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="3e3cf-318">Utiliser OLTP en mémoire dans une application SQL Azure existante</span><span class="sxs-lookup"><span data-stu-id="3e3cf-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="3e3cf-319">[Surveiller le stockage OLTP en mémoire](sql-database-in-memory-oltp-monitoring.md) pour l’OLTP en mémoire</span><span class="sxs-lookup"><span data-stu-id="3e3cf-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3e3cf-320">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3e3cf-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="3e3cf-321">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3e3cf-321">Deeper information</span></span>

- [<span data-ttu-id="3e3cf-322">Découvrez comment le Quorum double la charge de travail de la base de données clé tout en réduisant les DTU de 70 %, grâce à l’OLTP en mémoire dans la SQL Database</span><span class="sxs-lookup"><span data-stu-id="3e3cf-322">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [<span data-ttu-id="3e3cf-323">Billet de blog OLTP en mémoire dans Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="3e3cf-323">In-Memory OLTP in Azure SQL Database Blog Post</span></span>](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [<span data-ttu-id="3e3cf-324">En savoir plus sur In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="3e3cf-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="3e3cf-325">En savoir plus sur les index columnstore</span><span class="sxs-lookup"><span data-stu-id="3e3cf-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="3e3cf-326">En savoir plus sur l’analytique opérationnelle en temps réel</span><span class="sxs-lookup"><span data-stu-id="3e3cf-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="3e3cf-327">Consultez [Modèles de charge de travail courants et considérations relatives à la migration](http://msdn.microsoft.com/library/dn673538.aspx) (qui décrit des modèles de charge de travail où l’OLTP en mémoire apporte généralement des gains de performances significatifs)</span><span class="sxs-lookup"><span data-stu-id="3e3cf-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="3e3cf-328">Conception des applications</span><span class="sxs-lookup"><span data-stu-id="3e3cf-328">Application design</span></span>

- [<span data-ttu-id="3e3cf-329">In-Memory OLTP (optimisation en mémoire)</span><span class="sxs-lookup"><span data-stu-id="3e3cf-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="3e3cf-330">Utiliser OLTP en mémoire dans une application SQL Azure existante</span><span class="sxs-lookup"><span data-stu-id="3e3cf-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="3e3cf-331">Outils</span><span class="sxs-lookup"><span data-stu-id="3e3cf-331">Tools</span></span>

- [<span data-ttu-id="3e3cf-332">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="3e3cf-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="3e3cf-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="3e3cf-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="3e3cf-334">Outils SQL Server Data Tools (SSDT)</span><span class="sxs-lookup"><span data-stu-id="3e3cf-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
