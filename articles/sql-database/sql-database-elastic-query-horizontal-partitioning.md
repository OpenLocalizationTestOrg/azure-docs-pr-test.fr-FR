---
title: "aaaReporting sur les bases de données à grande échelle cloud | Documents Microsoft"
description: "Comment tooset les requêtes élastiques sur les partitions horizontales"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="35315-103">Création de rapports sur des bases de données cloud mises à l’échelle (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="35315-103">Reporting across scaled-out cloud databases (preview)</span></span>
![Requête sur plusieurs partitions][1]

<span data-ttu-id="35315-105">Les bases de données partitionnées répartissent des lignes sur une mise à l’échelle vers la couche données.</span><span class="sxs-lookup"><span data-stu-id="35315-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="35315-106">schéma de Hello est identique sur toutes les bases de données participantes, également connus sous le partitionnement horizontal.</span><span class="sxs-lookup"><span data-stu-id="35315-106">hello schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="35315-107">En utilisant une requête élastique, vous pouvez créer des rapports qui couvrent toutes les bases de données d’une base de données partitionnée.</span><span class="sxs-lookup"><span data-stu-id="35315-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="35315-108">Pour démarrer rapidement, consultez la rubrique [Création de rapports sur des bases de données cloud mises à l’échelle](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="35315-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="35315-109">Pour les bases de données non partitionnées, consultez [Interroger plusieurs bases de données cloud avec différents schémas](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="35315-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="35315-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="35315-110">Prerequisites</span></span>
* <span data-ttu-id="35315-111">Créer une carte de partitions à l’aide de la bibliothèque cliente de base de données élastique hello.</span><span class="sxs-lookup"><span data-stu-id="35315-111">Create a shard map using hello elastic database client library.</span></span> <span data-ttu-id="35315-112">Consultez la rubrique [Gestion des cartes de partitions](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="35315-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="35315-113">Ou utilisez l’exemple d’application hello dans [prise en main des outils de base de données élastique](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="35315-113">Or use hello sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="35315-114">Vous pouvez aussi consulter [existant de la migration des bases de données bases de données tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="35315-114">Alternatively, see [Migrate existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="35315-115">utilisateur de Hello doit posséder les autorisations ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="35315-115">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="35315-116">Cette autorisation est incluse avec l’autorisation ALTER DATABASE hello.</span><span class="sxs-lookup"><span data-stu-id="35315-116">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="35315-117">Les autorisations ALTER ANY EXTERNAL DATA SOURCE sont toohello nécessaires toorefer source de données sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="35315-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="35315-118">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="35315-118">Overview</span></span>
<span data-ttu-id="35315-119">Ces instructions créent représentation des métadonnées hello de votre couche données partitionnées dans base de données de requête élastique hello.</span><span class="sxs-lookup"><span data-stu-id="35315-119">These statements create hello metadata representation of your sharded data tier in hello elastic query database.</span></span> 

1. [<span data-ttu-id="35315-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="35315-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="35315-121">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="35315-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="35315-122">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="35315-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="35315-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="35315-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="35315-124">1.1 Créer la clé principale et les informations d’identification de la base de données</span><span class="sxs-lookup"><span data-stu-id="35315-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="35315-125">informations d’identification Hello sont utilisée par hello requête élastique tooconnect tooyour bases de données distantes.</span><span class="sxs-lookup"><span data-stu-id="35315-125">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="35315-126">Vérifiez que hello *»\<nom d’utilisateur\>»* ne comprend aucun *»@servername»* suffixe.</span><span class="sxs-lookup"><span data-stu-id="35315-126">Make sure that hello *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="35315-127">1.2 Créer des sources de données externes</span><span class="sxs-lookup"><span data-stu-id="35315-127">1.2 Create external data sources</span></span>
<span data-ttu-id="35315-128">Syntaxe :</span><span class="sxs-lookup"><span data-stu-id="35315-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="35315-129">Exemple</span><span class="sxs-lookup"><span data-stu-id="35315-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="35315-130">Récupérer la liste de hello de sources de données externes en cours :</span><span class="sxs-lookup"><span data-stu-id="35315-130">Retrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="35315-131">source de données externe Hello fait référence à votre carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="35315-131">hello external data source references your shard map.</span></span> <span data-ttu-id="35315-132">Une requête élastique utilise ensuite la source de données externe hello et hello sous-jacent partition carte tooenumerate hello bases de données participant à la couche de données hello.</span><span class="sxs-lookup"><span data-stu-id="35315-132">An elastic query then uses hello external data source and hello underlying shard map tooenumerate hello databases that participate in hello data tier.</span></span> <span data-ttu-id="35315-133">carte de partitions hello tooread utilisés sont Hello mêmes informations d’identification et tooaccess hello des données sur les partitions hello lors du traitement de hello d’une requête élastique.</span><span class="sxs-lookup"><span data-stu-id="35315-133">hello same credentials are used tooread hello shard map and tooaccess hello data on hello shards during hello processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="35315-134">1.3 Créer des tables externes</span><span class="sxs-lookup"><span data-stu-id="35315-134">1.3 Create external tables</span></span>
<span data-ttu-id="35315-135">Syntaxe :</span><span class="sxs-lookup"><span data-stu-id="35315-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="35315-136">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="35315-136">**Example**</span></span>

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

<span data-ttu-id="35315-137">Récupérer la liste hello des tables externes à partir de la base de données actuelle hello :</span><span class="sxs-lookup"><span data-stu-id="35315-137">Retrieve hello list of external tables from hello current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="35315-138">toodrop des tables externes :</span><span class="sxs-lookup"><span data-stu-id="35315-138">toodrop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="35315-139">Remarques</span><span class="sxs-lookup"><span data-stu-id="35315-139">Remarks</span></span>
<span data-ttu-id="35315-140">Hello données\_clause SOURCE définit la source de données externe hello (une carte de partitions) qui est utilisé pour une table externe hello.</span><span class="sxs-lookup"><span data-stu-id="35315-140">hello DATA\_SOURCE clause defines hello external data source (a shard map) that is used for hello external table.</span></span>  

<span data-ttu-id="35315-141">Hello schéma\_nom et l’objet\_mappent les clauses de nom table de tooa de définition de table externe hello dans un schéma différent.</span><span class="sxs-lookup"><span data-stu-id="35315-141">hello SCHEMA\_NAME and OBJECT\_NAME clauses map hello external table definition tooa table in a different schema.</span></span> <span data-ttu-id="35315-142">Si omis, schéma hello d’objet distant de hello est considéré comme étant toobe « dbo » et son nom est nom de la table externe identiques toohello toobe en cours de définition.</span><span class="sxs-lookup"><span data-stu-id="35315-142">If omitted, hello schema of hello remote object is assumed toobe “dbo” and its name is assumed toobe identical toohello external table name being defined.</span></span> <span data-ttu-id="35315-143">Cela est utile si hello nom de votre table distante est déjà utilisé dans la base de données hello où vous souhaitez une table externe toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="35315-143">This is useful if hello name of your remote table is already taken in hello database where you want toocreate hello external table.</span></span> <span data-ttu-id="35315-144">Par exemple, vous toodefine une tooget table externe une vue agrégée des affichages catalogue ou sur vos données à l’échelle des vues de gestion dynamique de niveau.</span><span class="sxs-lookup"><span data-stu-id="35315-144">For  example, you want toodefine an external table tooget an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="35315-145">Étant donné que les affichages catalogue et vues de gestion dynamique existent déjà localement, vous ne pouvez pas utiliser leur nom pour la définition de la table externe hello.</span><span class="sxs-lookup"><span data-stu-id="35315-145">Since catalog views and DMVs already exist locally, you cannot use their names for hello external table definition.</span></span> <span data-ttu-id="35315-146">Au lieu de cela, utilisez un autre nom et d’utiliser la vue de catalogue hello ou hello nom DMV Bonjour schéma\_nom et/ou objet\_clauses de nom.</span><span class="sxs-lookup"><span data-stu-id="35315-146">Instead, use a different name and use hello catalog view’s or hello DMV’s name in hello SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="35315-147">(Consultez l’exemple hello ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="35315-147">(See hello example below.)</span></span> 

<span data-ttu-id="35315-148">DISTRIBUTION Hello spécifie la distribution des données hello utilisée pour cette table.</span><span class="sxs-lookup"><span data-stu-id="35315-148">hello DISTRIBUTION clause specifies hello data distribution used for this table.</span></span> <span data-ttu-id="35315-149">processeur de requêtes Hello utilise les informations hello fournies dans le plans de requête plus efficace de hello DISTRIBUTION clause toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="35315-149">hello query processor utilizes hello information provided in hello DISTRIBUTION clause toobuild hello most efficient query plans.</span></span>  

1. <span data-ttu-id="35315-150">**PARTITIONNÉE** signifie que les données sont partitionnées horizontalement sur les bases de données hello.</span><span class="sxs-lookup"><span data-stu-id="35315-150">**SHARDED** means data is horizontally partitioned across hello databases.</span></span> <span data-ttu-id="35315-151">Hello clé de partitionnement pour la distribution des données hello est hello **< sharding_column_name >** paramètre.</span><span class="sxs-lookup"><span data-stu-id="35315-151">hello partitioning key for hello data distribution is hello **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="35315-152">**RÉPLIQUÉES** signifie que des copies identiques de la table de hello sont présents sur chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="35315-152">**REPLICATED** means that identical copies of hello table are present on each database.</span></span> <span data-ttu-id="35315-153">Il s’agit de votre tooensure responsabilité que les réplicas hello sont identiques entre les bases de données hello.</span><span class="sxs-lookup"><span data-stu-id="35315-153">It is your responsibility tooensure that hello replicas are identical across hello databases.</span></span>
3. <span data-ttu-id="35315-154">**ROUND\_(Round Robin)** signifie que la table hello est partitionnée horizontalement à l’aide d’une méthode de distribution de dépend de l’application.</span><span class="sxs-lookup"><span data-stu-id="35315-154">**ROUND\_ROBIN** means that hello table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="35315-155">**Couche de données référence**: une table externe hello DDL fait référence la source de données externe tooan.</span><span class="sxs-lookup"><span data-stu-id="35315-155">**Data tier reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="35315-156">source de données externe Hello spécifie une carte de partitions qui procure une table externe hello toolocate nécessaire des informations de hello toutes les bases de données hello dans votre couche données.</span><span class="sxs-lookup"><span data-stu-id="35315-156">hello external data source specifies a shard map which provides hello external table with hello information necessary toolocate all hello databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="35315-157">Considérations relatives à la sécurité</span><span class="sxs-lookup"><span data-stu-id="35315-157">Security considerations</span></span>
<span data-ttu-id="35315-158">Les utilisateurs avec une table externe accès toohello automatiquement accéder toohello les tables distantes sous-jacentes sous les informations d’identification hello donné dans la définition de source de données externe hello.</span><span class="sxs-lookup"><span data-stu-id="35315-158">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="35315-159">Évitez indésirable élévation de privilèges via les informations d’identification hello hello externe de source de données.</span><span class="sxs-lookup"><span data-stu-id="35315-159">Avoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="35315-160">Utilisez GRANT ou REVOKE pour une table externe, comme s'il s'agissait d'une table standard.</span><span class="sxs-lookup"><span data-stu-id="35315-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="35315-161">Une fois votre table externe et votre source de données externe définies, vous pouvez utiliser l’ensemble T-SQL complet sur vos tables externes.</span><span class="sxs-lookup"><span data-stu-id="35315-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="35315-162">Exemple : interrogation de bases de données partitionnées horizontales</span><span class="sxs-lookup"><span data-stu-id="35315-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="35315-163">Hello requête suivante effectue une jointure tridirectionnelle entre entrepôts, les commandes et les lignes de commande et utilise plusieurs agrégats et un filtre sélectif.</span><span class="sxs-lookup"><span data-stu-id="35315-163">hello following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="35315-164">Il suppose que le partitionnement (1) horizontal (partitionnement) et (2) qu’entrepôts, les commandes et les lignes de commande sont partitionnées par la colonne d’id de l’entrepôt hello, et cette requête élastique hello peut colocaliser les jointures hello sur les partitions hello et traiter la partie de la requête hello sur hello coûteuse de hello partitions en parallèle.</span><span class="sxs-lookup"><span data-stu-id="35315-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by hello warehouse id column, and that hello elastic query can co-locate hello joins on hello shards and process hello expensive part of hello query on hello shards in parallel.</span></span> 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="35315-165">Procédure stockée pour l’exécution de T-SQL à distance : sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="35315-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="35315-166">Requête élastique présente également une procédure stockée qui offre un accès direct toohello partitions.</span><span class="sxs-lookup"><span data-stu-id="35315-166">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="35315-167">Hello procédure stockée est appelée [sp\_exécuter \_distant](https://msdn.microsoft.com/library/mt703714) et peut être utilisé tooexecute des procédures stockées distantes ou le code T-SQL sur des bases de données distantes hello.</span><span class="sxs-lookup"><span data-stu-id="35315-167">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="35315-168">Il prend hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="35315-168">It takes hello following parameters:</span></span> 

* <span data-ttu-id="35315-169">Nom de source de données (nvarchar) : nom hello hello externe de source de données de type SGBDR.</span><span class="sxs-lookup"><span data-stu-id="35315-169">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="35315-170">Requête (nvarchar) : hello T-SQL toobe de requête exécutée sur chaque partition.</span><span class="sxs-lookup"><span data-stu-id="35315-170">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="35315-171">Déclaration de paramètre (nvarchar) - facultatif : chaîne avec les définitions de type de données pour les paramètres de hello utilisés dans le paramètre de requête hello (comme sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="35315-171">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="35315-172">Liste de valeurs de paramètre : facultative : valeurs de paramètre de liste séparées par des virgules (par exemple, sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="35315-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="35315-173">Hello sp\_exécuter\_distant utilise hello prévue hello appel paramètres tooexecute hello donné l’instruction T-SQL sur des bases de données distantes hello de source de données externe.</span><span class="sxs-lookup"><span data-stu-id="35315-173">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="35315-174">Elle utilise les informations d’identification hello de hello données externes tooconnect toohello shardmap manager base de données source et de bases de données distantes hello.</span><span class="sxs-lookup"><span data-stu-id="35315-174">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="35315-175">Exemple :</span><span class="sxs-lookup"><span data-stu-id="35315-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="35315-176">Connectivité des outils</span><span class="sxs-lookup"><span data-stu-id="35315-176">Connectivity for tools</span></span>
<span data-ttu-id="35315-177">Utilisez tooconnect de chaînes de connexion SQL Server standard votre application, votre BI et données intégration outils toohello base de données avec vos définitions de table externe.</span><span class="sxs-lookup"><span data-stu-id="35315-177">Use regular SQL Server connection strings tooconnect your application, your BI and data integration tools toohello database with your external table definitions.</span></span> <span data-ttu-id="35315-178">Assurez-vous que SQL Server est pris en charge comme source de données pour votre outil.</span><span class="sxs-lookup"><span data-stu-id="35315-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="35315-179">Ensuite référencer la base de données de requête élastique hello comme tout autre outil de toohello de connexion de base de données SQL Server et utiliser des tables externes à partir de votre application ou un outil comme si elles étaient des tables locales.</span><span class="sxs-lookup"><span data-stu-id="35315-179">Then reference hello elastic query database like any other SQL Server database connected toohello tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="35315-180">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="35315-180">Best practices</span></span>
* <span data-ttu-id="35315-181">Assurez-vous que cette base de données de point de terminaison de la requête élastique hello a reçu toutes les partitions via hello que pare-feu de base de données SQL et la base de données access toohello shardmap.</span><span class="sxs-lookup"><span data-stu-id="35315-181">Ensure that hello elastic query endpoint database has been given access toohello shardmap database and all shards through hello SQL DB firewalls.</span></span>  
* <span data-ttu-id="35315-182">Valider ou appliquer la distribution des données définie par une table externe hello hello.</span><span class="sxs-lookup"><span data-stu-id="35315-182">Validate or enforce hello data distribution defined by hello external table.</span></span> <span data-ttu-id="35315-183">Si la distribution réelle des données est différente de la distribution hello spécifiée dans votre définition de la table, vos requêtes peuvent donner des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="35315-183">If your actual data distribution is different from hello distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="35315-184">Requête élastique actuellement n’effectue pas élimination de partition lorsque les prédicats de clé de partitionnement hello elle permettrait toosafely exclure certaines partitions à partir du traitement.</span><span class="sxs-lookup"><span data-stu-id="35315-184">Elastic query currently does not perform shard elimination when predicates over hello sharding key would allow it toosafely exclude certain shards from processing.</span></span>
* <span data-ttu-id="35315-185">Requête élastique mieux adaptée pour les requêtes où la plupart des calculs de hello peut être effectuée sur les partitions hello.</span><span class="sxs-lookup"><span data-stu-id="35315-185">Elastic query works best for queries where most of hello computation can be done on hello shards.</span></span> <span data-ttu-id="35315-186">Vous obtenez généralement hello meilleurs résultats avec des prédicats de filtre sélectif qui peut être évaluée sur les partitions hello ou des jointures sur hello clés qui peuvent être effectuées de manière alignées sur toutes les partitions de partitionnement.</span><span class="sxs-lookup"><span data-stu-id="35315-186">You typically get hello best query performance with selective filter predicates that can be evaluated on hello shards or joins over hello partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="35315-187">Autres modèles de requête peuvent nécessiter des tooload grandes quantités de données à partir du nœud principal hello partitions toohello et peuvent être lent</span><span class="sxs-lookup"><span data-stu-id="35315-187">Other query patterns may need tooload large amounts of data from hello shards toohello head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="35315-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="35315-188">Next steps</span></span>

* <span data-ttu-id="35315-189">Pour une présentation des requêtes élastiques, consultez [Présentation des requêtes élastiques](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="35315-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="35315-190">Pour le didacticiel sur le partitionnement vertical, consultez [Prise en main des requêtes de bases de données croisées (partitionnement vertical)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="35315-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="35315-191">Pour la syntaxe et des exemples de requêtes pour des données partitionnées verticalement, consultez [Requêtes sur des données partitionnées verticalement](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="35315-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="35315-192">Pour commencer le didacticiel sur le partitionnement horizontal (sharding), consultez [Prise en main des requêtes élastiques pour le partitionnement horizontal (sharding)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="35315-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="35315-193">Consultez [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) pour une procédure stockée qui exécute une instruction Transact-SQL sur une seule base de données Azure SQL distante ou un ensemble de bases de données servant de partitions dans un schéma de partitionnement horizontal.</span><span class="sxs-lookup"><span data-stu-id="35315-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
