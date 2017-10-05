---
title: "Créer des rapports sur des bases de données cloud avec montée en charge (partitionnement horizontal) | Microsoft Docs"
description: "comment utiliser des requêtes entre plusieurs bases de données"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: 8eb56d44c3a261f6325d4fc91f169d09bf108160
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="d669f-103">Créer des rapports sur des bases de données cloud avec montée en charge (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="d669f-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="d669f-104">Vous pouvez créer des rapports tirés de plusieurs bases de données SQL Azure à partir d’un point de connexion unique par le biais d’une [requête élastique](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d669f-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="d669f-105">Les bases de données doivent être partitionnées horizontalement.</span><span class="sxs-lookup"><span data-stu-id="d669f-105">The databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="d669f-106">Si vous avez déjà une base de données, consultez [Migrer des bases de données existantes vers des bases de données mises à l’échelle](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="d669f-106">If you have an existing database, see [Migrating existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="d669f-107">Pour connaître les objets SQL requis dans le cadre d’une requête, consultez [Interroger plusieurs bases de données partitionnées horizontalement](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="d669f-107">To understand the SQL objects needed to query, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d669f-108">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="d669f-108">Prerequisites</span></span>
<span data-ttu-id="d669f-109">Téléchargez et exécutez l’exemple de la rubrique [Prise en main des outils de base de données élastique](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d669f-109">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="d669f-110">Créez un gestionnaire des cartes de partitions à l’aide de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="d669f-110">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="d669f-111">Ici vous allez créer un gestionnaire des cartes de partitions avec plusieurs partitions, puis insérer des données dans les partitions.</span><span class="sxs-lookup"><span data-stu-id="d669f-111">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="d669f-112">Si vos partitions comportent déjà des données partitionnées, vous pouvez ignorer ces étapes et passer à la section suivante.</span><span class="sxs-lookup"><span data-stu-id="d669f-112">If you happen to already have shards setup with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="d669f-113">Créez et exécutez l’exemple d’application de la rubrique **Prise en main des outils de base de données élastique** .</span><span class="sxs-lookup"><span data-stu-id="d669f-113">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="d669f-114">Suivez la procédure jusqu’à l’étape 7 dans la section [Télécharger et exécuter l’exemple d’application](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="d669f-114">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="d669f-115">À la fin de l’étape 7, vous verrez l’invite de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d669f-115">At the end of Step 7, you will see the following command prompt:</span></span>

    ![invite de commande][1]
2. <span data-ttu-id="d669f-117">Dans la fenêtre de commande, entrez « 1 » et appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="d669f-117">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="d669f-118">Cela crée le gestionnaire des cartes de partitions et ajoute deux partitions sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="d669f-118">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="d669f-119">Tapez « 3 », puis appuyez sur **Entrée**. Répétez l’action quatre fois.</span><span class="sxs-lookup"><span data-stu-id="d669f-119">Then type "3" and press **Enter**; repeat the action four times.</span></span> <span data-ttu-id="d669f-120">Cela permet d’insérer des lignes d’exemples de données dans vos partitions.</span><span class="sxs-lookup"><span data-stu-id="d669f-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="d669f-121">Le [portail Azure](https://portal.azure.com) doit alors montrer trois nouvelles bases de données dans votre serveur :</span><span class="sxs-lookup"><span data-stu-id="d669f-121">The [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Confirmation Visual Studio][2]

   <span data-ttu-id="d669f-123">À ce stade, les requêtes de bases de données croisées sont prises en charge via les bibliothèques clientes de bases de données élastiques.</span><span class="sxs-lookup"><span data-stu-id="d669f-123">At this point, cross-database queries are supported through the Elastic Database client libraries.</span></span> <span data-ttu-id="d669f-124">Par exemple, utilisez l’option 4 dans la fenêtre de commande.</span><span class="sxs-lookup"><span data-stu-id="d669f-124">For example, use option 4 in the command window.</span></span> <span data-ttu-id="d669f-125">Les résultats d’une requête de plusieurs partitions sont toujours un élément **UNION ALL** des résultats de toutes les partitions.</span><span class="sxs-lookup"><span data-stu-id="d669f-125">The results from a multi-shard query are always a **UNION ALL** of the results from all shards.</span></span>

   <span data-ttu-id="d669f-126">Dans la section suivante, nous créons un exemple de point de terminaison de base de données qui prend en charge une interrogation plus riche des données entre les partitions.</span><span class="sxs-lookup"><span data-stu-id="d669f-126">In the next section, we create a sample database endpoint that supports richer querying of the data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="d669f-127">Créez une base de données de requête élastique</span><span class="sxs-lookup"><span data-stu-id="d669f-127">Create an elastic query database</span></span>
1. <span data-ttu-id="d669f-128">Ouvrez le [portail Azure](https://portal.azure.com) et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="d669f-128">Open the [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="d669f-129">Créez une nouvelle base de données SQL Azure dans le même serveur que votre partition configurée.</span><span class="sxs-lookup"><span data-stu-id="d669f-129">Create a new Azure SQL database in the same server as your shard setup.</span></span> <span data-ttu-id="d669f-130">Nommez la base de données « ElasticDBQuery ».</span><span class="sxs-lookup"><span data-stu-id="d669f-130">Name the database "ElasticDBQuery."</span></span>

    ![Portail Azure et tarification][3]

    > [!NOTE]
    > <span data-ttu-id="d669f-132">Vous pouvez utiliser une base de données existante.</span><span class="sxs-lookup"><span data-stu-id="d669f-132">you can use an existing database.</span></span> <span data-ttu-id="d669f-133">Si c’est le cas, il ne doit pas s’agir de l’une des partitions sur laquelle vous souhaitez exécuter les requêtes.</span><span class="sxs-lookup"><span data-stu-id="d669f-133">If you can do so, it must not be one of the shards that you would like to execute your queries on.</span></span> <span data-ttu-id="d669f-134">Cette base de données sera utilisée pour la création d’objets de métadonnées pour une requête de base de données élastique.</span><span class="sxs-lookup"><span data-stu-id="d669f-134">This database will be used for creating the metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="d669f-135">Créez des objets de base de données</span><span class="sxs-lookup"><span data-stu-id="d669f-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="d669f-136">Clé principale et informations d’identification de la base de données</span><span class="sxs-lookup"><span data-stu-id="d669f-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="d669f-137">Celles-ci sont utilisées pour se connecter au gestionnaire des cartes de partition et aux partitions :</span><span class="sxs-lookup"><span data-stu-id="d669f-137">These are used to connect to the shard map manager and the shards:</span></span>

1. <span data-ttu-id="d669f-138">Ouvrez SQL Server Management Studio ou SQL Server Data Tools dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d669f-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="d669f-139">Connectez-vous à la base de données ElasticDBQuery et exécutez les commandes T-SQL suivantes :</span><span class="sxs-lookup"><span data-stu-id="d669f-139">Connect to ElasticDBQuery database and execute the following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="d669f-140">Le nom d’utilisateur et le mot de passe doivent être les mêmes que les informations de connexion utilisées à l’étape 6 de la rubrique [Télécharger et exécuter l’exemple d’application](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) dans [Prise en main des outils de base de données élastique](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d669f-140">"username" and "password" should be the same as login information used in step 6 of [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="d669f-141">Sources de données externes</span><span class="sxs-lookup"><span data-stu-id="d669f-141">External data sources</span></span>
<span data-ttu-id="d669f-142">Pour créer une source de données externe, exécutez la commande suivante sur la base de données ElasticDBQuery :</span><span class="sxs-lookup"><span data-stu-id="d669f-142">To create an external data source, execute the following command on the ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="d669f-143">« CustomerIDShardMap » est le nom de la carte de partition, si vous avez créé la carte de partition et le gestionnaire des cartes de partition à l’aide de l’exemple d’outils souples de la base de données.</span><span class="sxs-lookup"><span data-stu-id="d669f-143">"CustomerIDShardMap" is the name of the shard map, if you created the shard map and shard map manager using the elastic database tools sample.</span></span> <span data-ttu-id="d669f-144">Toutefois, si vous avez utilisé l’installation personnalisée pour cet exemple, le nom de carte de partition doit correspondre au nom choisi dans l’application.</span><span class="sxs-lookup"><span data-stu-id="d669f-144">However, if you used your custom setup for this sample, then it should be the shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="d669f-145">Tables externes</span><span class="sxs-lookup"><span data-stu-id="d669f-145">External tables</span></span>
<span data-ttu-id="d669f-146">Créez une table externe qui correspond à la table des clients sur les partitions en exécutant la commande suivante sur la base de données ElasticDBQuery :</span><span class="sxs-lookup"><span data-stu-id="d669f-146">Create an external table that matches the Customers table on the shards by executing the following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="d669f-147">Exécutez un exemple de requête T-SQL de base de données élastique</span><span class="sxs-lookup"><span data-stu-id="d669f-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="d669f-148">Après avoir défini vos tables externes et votre source de données externe, vous pouvez utiliser l’ensemble T-SQL sur vos tables externes.</span><span class="sxs-lookup"><span data-stu-id="d669f-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="d669f-149">Exécutez cette requête sur la base de données ElasticDBQuery :</span><span class="sxs-lookup"><span data-stu-id="d669f-149">Execute this query on the ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="d669f-150">Vous remarquerez que la requête regroupe les résultats de toutes les partitions et donne le résultat suivant :</span><span class="sxs-lookup"><span data-stu-id="d669f-150">You will notice that the query aggregates results from all the shards and gives the following output:</span></span>

![Détails des résultats][4]

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="d669f-152">Importez les résultats de la requête de base de données élastique dans Excel</span><span class="sxs-lookup"><span data-stu-id="d669f-152">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="d669f-153">Vous pouvez importer les résultats d’une requête vers un fichier Excel.</span><span class="sxs-lookup"><span data-stu-id="d669f-153">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="d669f-154">Lancez Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="d669f-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="d669f-155">Accédez au ruban **Données** .</span><span class="sxs-lookup"><span data-stu-id="d669f-155">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="d669f-156">Cliquez sur **À partir d’autres sources** et sur **À partir de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="d669f-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importation au format Excel à partir d’autres sources][5]
4. <span data-ttu-id="d669f-158">Dans l’ **Assistant de connexion de données** saisissez le nom du serveur et les informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="d669f-158">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="d669f-159">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d669f-159">Then click **Next**.</span></span>
5. <span data-ttu-id="d669f-160">Dans la boîte de dialogue **Sélectionner la base de données qui contient les données que vous souhaitez**, sélectionnez la base de données **ElasticDBQuery**.</span><span class="sxs-lookup"><span data-stu-id="d669f-160">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="d669f-161">Sélectionnez la table **Clients** dans la liste et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d669f-161">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="d669f-162">Puis, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="d669f-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="d669f-163">Dans le formulaire **Importer des données**, sous **Sélectionner le mode d’affichage des données dans votre classeur**, sélectionnez **Table** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d669f-163">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="d669f-164">Toutes les lignes de la table **Clients** , stockées dans des partitions différentes, remplissent la feuille Excel.</span><span class="sxs-lookup"><span data-stu-id="d669f-164">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

<span data-ttu-id="d669f-165">Vous pouvez maintenant utiliser les fonctions de visualisation de données puissantes d’Excel.</span><span class="sxs-lookup"><span data-stu-id="d669f-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="d669f-166">Vous pouvez utiliser la chaîne de connexion avec votre nom de serveur, votre nom de base de données et les informations d’identification pour vous connecter vos outils d’intégration BI et de données dans la base de données de requête élastique.</span><span class="sxs-lookup"><span data-stu-id="d669f-166">You can use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="d669f-167">Assurez-vous que SQL Server est pris en charge comme source de données pour votre outil.</span><span class="sxs-lookup"><span data-stu-id="d669f-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="d669f-168">Vous pouvez vous traiter la base de données de requête élastique et les tables externes comme n’importe quelles bases de données SQL Server et tables SQL Server auxquelles vous vous connectez avec votre outil.</span><span class="sxs-lookup"><span data-stu-id="d669f-168">You can refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="d669f-169">Coût</span><span class="sxs-lookup"><span data-stu-id="d669f-169">Cost</span></span>
<span data-ttu-id="d669f-170">La fonction de requête de base de données élastique n’entraîne aucuns frais supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="d669f-170">There is no additional charge for using the Elastic Database Query feature.</span></span>

<span data-ttu-id="d669f-171">Pour plus d’informations sur la tarification, consultez la page [Tarification - Base de données SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="d669f-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d669f-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d669f-172">Next steps</span></span>

* <span data-ttu-id="d669f-173">Pour une présentation des requêtes élastiques, consultez [Présentation des requêtes élastiques](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d669f-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="d669f-174">Pour le didacticiel sur le partitionnement vertical, consultez [Prise en main des requêtes de bases de données croisées (partitionnement vertical)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="d669f-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="d669f-175">Pour la syntaxe et des exemples de requêtes pour des données partitionnées verticalement, consultez [Requêtes sur des données partitionnées verticalement](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="d669f-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="d669f-176">Pour la syntaxe et des exemples de requêtes pour des données partitionnées horizontalement, consultez [Requêtes sur des données partitionnées horizontalement](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="d669f-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="d669f-177">Consultez [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) pour une procédure stockée qui exécute une instruction Transact-SQL sur une seule base de données Azure SQL distante ou un ensemble de bases de données servant de partitions dans un schéma de partitionnement horizontal.</span><span class="sxs-lookup"><span data-stu-id="d669f-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
