---
title: "aaaReport sur les bases de données à grande échelle cloud (partitionnement horizontal) | Documents Microsoft"
description: "Comment toouse franchissent les requêtes de base de données de base de données"
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
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="830a7-103">Créer des rapports sur des bases de données cloud avec montée en charge (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="830a7-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="830a7-104">Vous pouvez créer des rapports tirés de plusieurs bases de données SQL Azure à partir d’un point de connexion unique par le biais d’une [requête élastique](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="830a7-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="830a7-105">bases de données Hello doivent être partitionnées horizontalement (également appelé « partitionnée »).</span><span class="sxs-lookup"><span data-stu-id="830a7-105">hello databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="830a7-106">Si vous avez une base de données existante, consultez [existant de la migration des bases de données bases de données tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="830a7-106">If you have an existing database, see [Migrating existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="830a7-107">les objets SQL toounderstand hello nécessaires tooquery, consultez [interroger plusieurs bases de données partitionnées horizontalement](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="830a7-107">toounderstand hello SQL objects needed tooquery, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="830a7-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="830a7-108">Prerequisites</span></span>
<span data-ttu-id="830a7-109">Téléchargez et exécutez hello [mise en route avec l’exemple des outils de base de données élastique](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="830a7-109">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="830a7-110">Créer une carte de partitions manager à l’aide de hello, exemple d’application</span><span class="sxs-lookup"><span data-stu-id="830a7-110">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="830a7-111">Ici vous allez créer une carte de partitions manager ainsi que plusieurs partitions, suivie de l’insertion de données dans les partitions hello.</span><span class="sxs-lookup"><span data-stu-id="830a7-111">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="830a7-112">Si vous vous trouvez tooalready contiennent le programme d’installation de partitions avec des données partitionnées, vous pouvez ignorer hello comme suit et déplacer la section suivante de toohello.</span><span class="sxs-lookup"><span data-stu-id="830a7-112">If you happen tooalready have shards setup with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="830a7-113">Générez et exécutez hello **prise en main des outils de base de données élastique** exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="830a7-113">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="830a7-114">Hello comme suit avant l’étape 7 de la section de hello [télécharger et exécuter l’exemple d’application hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="830a7-114">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="830a7-115">Extrémité hello de l’étape 7, vous verrez hello après l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="830a7-115">At hello end of Step 7, you will see hello following command prompt:</span></span>

    ![invite de commande][1]
2. <span data-ttu-id="830a7-117">Dans la fenêtre de commande hello, tapez « 1 » et appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="830a7-117">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="830a7-118">Cela crée le Gestionnaire de carte de partitions hello et ajoute le serveur de toohello deux partitions.</span><span class="sxs-lookup"><span data-stu-id="830a7-118">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="830a7-119">Tapez « 3 », puis appuyez sur **entrée**; Répétez l’action de hello quatre fois.</span><span class="sxs-lookup"><span data-stu-id="830a7-119">Then type "3" and press **Enter**; repeat hello action four times.</span></span> <span data-ttu-id="830a7-120">Cela permet d’insérer des lignes d’exemples de données dans vos partitions.</span><span class="sxs-lookup"><span data-stu-id="830a7-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="830a7-121">Hello [portail Azure](https://portal.azure.com) doivent s’afficher trois nouvelles bases de données dans votre serveur :</span><span class="sxs-lookup"><span data-stu-id="830a7-121">hello [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Confirmation Visual Studio][2]

   <span data-ttu-id="830a7-123">À ce stade, les requêtes de bases de données croisées sont pris en charge via les bibliothèques clientes hello élastique de base de données.</span><span class="sxs-lookup"><span data-stu-id="830a7-123">At this point, cross-database queries are supported through hello Elastic Database client libraries.</span></span> <span data-ttu-id="830a7-124">Par exemple, utilisez l’option 4 dans la fenêtre de commande hello.</span><span class="sxs-lookup"><span data-stu-id="830a7-124">For example, use option 4 in hello command window.</span></span> <span data-ttu-id="830a7-125">Hello les résultats d’une requête de plusieurs partition sont toujours un **UNION ALL** de résultats hello à partir de toutes les partitions.</span><span class="sxs-lookup"><span data-stu-id="830a7-125">hello results from a multi-shard query are always a **UNION ALL** of hello results from all shards.</span></span>

   <span data-ttu-id="830a7-126">Dans la section suivante de hello, nous créer un point de terminaison de base de données exemple qui prend en charge l’interrogation plus riche de données de hello entre les partitions.</span><span class="sxs-lookup"><span data-stu-id="830a7-126">In hello next section, we create a sample database endpoint that supports richer querying of hello data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="830a7-127">Créez une base de données de requête élastique</span><span class="sxs-lookup"><span data-stu-id="830a7-127">Create an elastic query database</span></span>
1. <span data-ttu-id="830a7-128">Ouvrez hello [portail Azure](https://portal.azure.com) et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="830a7-128">Open hello [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="830a7-129">Créer une nouvelle base de données SQL Azure Bonjour même serveur que votre programme d’installation de la partition.</span><span class="sxs-lookup"><span data-stu-id="830a7-129">Create a new Azure SQL database in hello same server as your shard setup.</span></span> <span data-ttu-id="830a7-130">Nom de la base de données hello « ElasticDBQuery ».</span><span class="sxs-lookup"><span data-stu-id="830a7-130">Name hello database "ElasticDBQuery."</span></span>

    ![Portail Azure et tarification][3]

    > [!NOTE]
    > <span data-ttu-id="830a7-132">Vous pouvez utiliser une base de données existante.</span><span class="sxs-lookup"><span data-stu-id="830a7-132">you can use an existing database.</span></span> <span data-ttu-id="830a7-133">Si vous pouvez le faire, il ne doit pas être une des partitions hello que vous aimeriez tooexecute vos requêtes sur.</span><span class="sxs-lookup"><span data-stu-id="830a7-133">If you can do so, it must not be one of hello shards that you would like tooexecute your queries on.</span></span> <span data-ttu-id="830a7-134">Cette base de données sera utilisé pour la création d’objets de métadonnées pour une requête de base de données élastique hello.</span><span class="sxs-lookup"><span data-stu-id="830a7-134">This database will be used for creating hello metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="830a7-135">Créez des objets de base de données</span><span class="sxs-lookup"><span data-stu-id="830a7-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="830a7-136">Clé principale et informations d’identification de la base de données</span><span class="sxs-lookup"><span data-stu-id="830a7-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="830a7-137">Il s’agit de gestionnaire de carte de partitions toohello tooconnect utilisés et les partitions hello :</span><span class="sxs-lookup"><span data-stu-id="830a7-137">These are used tooconnect toohello shard map manager and hello shards:</span></span>

1. <span data-ttu-id="830a7-138">Ouvrez SQL Server Management Studio ou SQL Server Data Tools dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="830a7-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="830a7-139">Se connecter tooElasticDBQuery de base de données et exécutez hello suivant de commandes T-SQL :</span><span class="sxs-lookup"><span data-stu-id="830a7-139">Connect tooElasticDBQuery database and execute hello following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="830a7-140">« username » et « password » doit être hello même en tant qu’informations de connexion utilisées à l’étape 6 de [télécharger et exécuter l’exemple d’application hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) dans [prise en main des outils de base de données élastique](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="830a7-140">"username" and "password" should be hello same as login information used in step 6 of [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="830a7-141">Sources de données externes</span><span class="sxs-lookup"><span data-stu-id="830a7-141">External data sources</span></span>
<span data-ttu-id="830a7-142">toocreate source de données externe, exécutez hello suivant de commande de base de données ElasticDBQuery hello :</span><span class="sxs-lookup"><span data-stu-id="830a7-142">toocreate an external data source, execute hello following command on hello ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="830a7-143">« CustomerIDShardMap » est le nom hello de carte de partitions hello, si vous avez créé carte de partitions et de carte de partitions hello manager à l’aide des exemples d’outils hello élastique de base de données.</span><span class="sxs-lookup"><span data-stu-id="830a7-143">"CustomerIDShardMap" is hello name of hello shard map, if you created hello shard map and shard map manager using hello elastic database tools sample.</span></span> <span data-ttu-id="830a7-144">Toutefois, si vous avez utilisé votre installation personnalisée pour cet exemple, il doit être nom de mappage de partitions hello choisis dans votre application.</span><span class="sxs-lookup"><span data-stu-id="830a7-144">However, if you used your custom setup for this sample, then it should be hello shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="830a7-145">Tables externes</span><span class="sxs-lookup"><span data-stu-id="830a7-145">External tables</span></span>
<span data-ttu-id="830a7-146">Créer une table externe qui correspond à celui de la table de clients de hello sur les partitions hello en exécutant la commande suivante sur la base de données ElasticDBQuery de hello :</span><span class="sxs-lookup"><span data-stu-id="830a7-146">Create an external table that matches hello Customers table on hello shards by executing hello following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="830a7-147">Exécutez un exemple de requête T-SQL de base de données élastique</span><span class="sxs-lookup"><span data-stu-id="830a7-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="830a7-148">Après avoir défini vos tables externes et votre source de données externe, vous pouvez utiliser l’ensemble T-SQL sur vos tables externes.</span><span class="sxs-lookup"><span data-stu-id="830a7-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="830a7-149">Exécutez cette requête sur la base de données ElasticDBQuery hello :</span><span class="sxs-lookup"><span data-stu-id="830a7-149">Execute this query on hello ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="830a7-150">Vous remarquerez cette requête hello regroupe les résultats à partir de toutes les partitions hello et donne hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="830a7-150">You will notice that hello query aggregates results from all hello shards and gives hello following output:</span></span>

![Détails des résultats][4]

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="830a7-152">Importer tooExcel de résultats de requête de base de données élastique</span><span class="sxs-lookup"><span data-stu-id="830a7-152">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="830a7-153">Vous pouvez importer les résultats hello à partir d’un fichier Excel de tooan requête.</span><span class="sxs-lookup"><span data-stu-id="830a7-153">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="830a7-154">Lancez Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="830a7-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="830a7-155">Accédez toohello **données** ruban.</span><span class="sxs-lookup"><span data-stu-id="830a7-155">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="830a7-156">Cliquez sur **À partir d’autres sources** et sur **À partir de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="830a7-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importation au format Excel à partir d’autres sources][5]
4. <span data-ttu-id="830a7-158">Bonjour **Assistant connexion de données** tapez hello des informations d’identification nom et la connexion de serveur.</span><span class="sxs-lookup"><span data-stu-id="830a7-158">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="830a7-159">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="830a7-159">Then click **Next**.</span></span>
5. <span data-ttu-id="830a7-160">Dans la boîte de dialogue hello **base de données hello Select qui contient les données hello**, sélectionnez hello **ElasticDBQuery** base de données.</span><span class="sxs-lookup"><span data-stu-id="830a7-160">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="830a7-161">Sélectionnez hello **clients** de table dans la vue de liste hello et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="830a7-161">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="830a7-162">Puis, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="830a7-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="830a7-163">Bonjour **importer des données** formulaire sous **Choisissez comment vous voulez que tooview ces données dans votre classeur**, sélectionnez **Table** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="830a7-163">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="830a7-164">Tous les hello des lignes à partir de **clients** table, stockée dans des partitions différentes remplir la feuille de calcul Excel hello.</span><span class="sxs-lookup"><span data-stu-id="830a7-164">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

<span data-ttu-id="830a7-165">Vous pouvez maintenant utiliser les fonctions de visualisation de données puissantes d’Excel.</span><span class="sxs-lookup"><span data-stu-id="830a7-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="830a7-166">Vous pouvez utiliser de chaîne de connexion hello avec le nom de votre serveur, nom de la base de données et que vous les informations d’identification tooconnect votre BI et données intégration outils toohello requête élastique de base de données.</span><span class="sxs-lookup"><span data-stu-id="830a7-166">You can use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="830a7-167">Assurez-vous que SQL Server est pris en charge comme source de données pour votre outil.</span><span class="sxs-lookup"><span data-stu-id="830a7-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="830a7-168">Vous pouvez consulter la base de données de requête élastique toohello et des tables externes comme toute autre base de données SQL Server et des tables SQL Server que vous devez vous connecter toowith votre outil.</span><span class="sxs-lookup"><span data-stu-id="830a7-168">You can refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="830a7-169">Coût</span><span class="sxs-lookup"><span data-stu-id="830a7-169">Cost</span></span>
<span data-ttu-id="830a7-170">Il n’existe aucun frais supplémentaire pour à l’aide de la fonctionnalité de requête de base de données élastique hello.</span><span class="sxs-lookup"><span data-stu-id="830a7-170">There is no additional charge for using hello Elastic Database Query feature.</span></span>

<span data-ttu-id="830a7-171">Pour plus d’informations sur la tarification, consultez la page [Tarification - Base de données SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="830a7-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="830a7-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="830a7-172">Next steps</span></span>

* <span data-ttu-id="830a7-173">Pour une présentation des requêtes élastiques, consultez [Présentation des requêtes élastiques](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="830a7-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="830a7-174">Pour le didacticiel sur le partitionnement vertical, consultez [Prise en main des requêtes de bases de données croisées (partitionnement vertical)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="830a7-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="830a7-175">Pour la syntaxe et des exemples de requêtes pour des données partitionnées verticalement, consultez [Requêtes sur des données partitionnées verticalement](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="830a7-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="830a7-176">Pour la syntaxe et des exemples de requêtes pour des données partitionnées horizontalement, consultez [Requêtes sur des données partitionnées horizontalement](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="830a7-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="830a7-177">Consultez [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) pour une procédure stockée qui exécute une instruction Transact-SQL sur une seule base de données Azure SQL distante ou un ensemble de bases de données servant de partitions dans un schéma de partitionnement horizontal.</span><span class="sxs-lookup"><span data-stu-id="830a7-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
