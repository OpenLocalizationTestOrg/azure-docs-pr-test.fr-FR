---
title: "Création de rapports sur des bases de données cloud mises à l’échelle | Microsoft Docs"
description: "comment configurer des requêtes élastiques sur les partitions horizontales"
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
ms.openlocfilehash: 62b5bcd26aa1ed219fb38970916e0e8847ceb577
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="5c038-103">Création de rapports sur des bases de données cloud mises à l’échelle (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="5c038-103">Reporting across scaled-out cloud databases (preview)</span></span>
![Requête sur plusieurs partitions][1]

<span data-ttu-id="5c038-105">Les bases de données partitionnées répartissent des lignes sur une mise à l’échelle vers la couche données.</span><span class="sxs-lookup"><span data-stu-id="5c038-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="5c038-106">Le schéma est identique sur toutes les bases de données participantes, également connu sous le terme partitionnement horizontal.</span><span class="sxs-lookup"><span data-stu-id="5c038-106">The schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="5c038-107">En utilisant une requête élastique, vous pouvez créer des rapports qui couvrent toutes les bases de données d’une base de données partitionnée.</span><span class="sxs-lookup"><span data-stu-id="5c038-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="5c038-108">Pour démarrer rapidement, consultez la rubrique [Création de rapports sur des bases de données cloud mises à l’échelle](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5c038-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="5c038-109">Pour les bases de données non partitionnées, consultez [Interroger plusieurs bases de données cloud avec différents schémas](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="5c038-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5c038-110">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="5c038-110">Prerequisites</span></span>
* <span data-ttu-id="5c038-111">Créez une carte de partitions à l’aide d’une bibliothèque de base de données élastique cliente.</span><span class="sxs-lookup"><span data-stu-id="5c038-111">Create a shard map using the elastic database client library.</span></span> <span data-ttu-id="5c038-112">Consultez la rubrique [Gestion des cartes de partitions](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="5c038-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="5c038-113">Ou utilisez l’exemple d’application de la rubrique [Prise en main des outils de base de données élastiques](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5c038-113">Or use the sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="5c038-114">Vous pouvez également consulter la rubrique [Migrer des bases de données existantes vers des bases de données mises à l’échelle](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="5c038-114">Alternatively, see [Migrate existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="5c038-115">L’utilisateur doit posséder l’autorisation ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="5c038-115">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="5c038-116">Cette autorisation est incluse dans l’autorisation ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="5c038-116">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="5c038-117">Les autorisations ALTER ANY EXTERNAL DATA SOURCE sont nécessaires pour faire référence à la source de données sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="5c038-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="5c038-118">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5c038-118">Overview</span></span>
<span data-ttu-id="5c038-119">Ces instructions créent une représentation des métadonnées de votre couche de données partitionnées dans la base de données de requête élastique.</span><span class="sxs-lookup"><span data-stu-id="5c038-119">These statements create the metadata representation of your sharded data tier in the elastic query database.</span></span> 

1. [<span data-ttu-id="5c038-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="5c038-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="5c038-121">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="5c038-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="5c038-122">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="5c038-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="5c038-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="5c038-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="5c038-124">1.1 Créer la clé principale et les informations d’identification de la base de données</span><span class="sxs-lookup"><span data-stu-id="5c038-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="5c038-125">Les informations d'identification sont utilisées par la requête élastique pour se connecter à vos bases de données distantes.</span><span class="sxs-lookup"><span data-stu-id="5c038-125">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="5c038-126">Vérifiez que *« \<nom d’utilisateur\> »* ne contient pas le suffixe *« @servername »*.</span><span class="sxs-lookup"><span data-stu-id="5c038-126">Make sure that the *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="5c038-127">1.2 Créer des sources de données externes</span><span class="sxs-lookup"><span data-stu-id="5c038-127">1.2 Create external data sources</span></span>
<span data-ttu-id="5c038-128">Syntaxe :</span><span class="sxs-lookup"><span data-stu-id="5c038-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="5c038-129">Exemple</span><span class="sxs-lookup"><span data-stu-id="5c038-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="5c038-130">Récupérez la liste des sources de données externes actuelles :</span><span class="sxs-lookup"><span data-stu-id="5c038-130">Retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="5c038-131">La source de données externe fait référence au mappage de partitions.</span><span class="sxs-lookup"><span data-stu-id="5c038-131">The external data source references your shard map.</span></span> <span data-ttu-id="5c038-132">Une requête élastique utilise ensuite la source de données externe et le mappage de la partition sous-jacents pour énumérer les bases de données qui interviennent dans les couches de données.</span><span class="sxs-lookup"><span data-stu-id="5c038-132">An elastic query then uses the external data source and the underlying shard map to enumerate the databases that participate in the data tier.</span></span> <span data-ttu-id="5c038-133">Les mêmes informations d’identification sont utilisées pour lire la carte de partitions et accéder aux données présentes sur les partitions pendant le traitement d’une requête élastique.</span><span class="sxs-lookup"><span data-stu-id="5c038-133">The same credentials are used to read the shard map and to access the data on the shards during the processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="5c038-134">1.3 Créer des tables externes</span><span class="sxs-lookup"><span data-stu-id="5c038-134">1.3 Create external tables</span></span>
<span data-ttu-id="5c038-135">Syntaxe :</span><span class="sxs-lookup"><span data-stu-id="5c038-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="5c038-136">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="5c038-136">**Example**</span></span>

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

<span data-ttu-id="5c038-137">Récupérer la liste des tables externes à partir de la base de données en cours :</span><span class="sxs-lookup"><span data-stu-id="5c038-137">Retrieve the list of external tables from the current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="5c038-138">Pour supprimer des bases de données externes :</span><span class="sxs-lookup"><span data-stu-id="5c038-138">To drop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="5c038-139">Remarques</span><span class="sxs-lookup"><span data-stu-id="5c038-139">Remarks</span></span>
<span data-ttu-id="5c038-140">La clause DATA\_SOURCE définit la source de données externe (une carte de partitions dans le cas d’un partitionnement horizontal) qui est utilisée pour la table externe.</span><span class="sxs-lookup"><span data-stu-id="5c038-140">The DATA\_SOURCE clause defines the external data source (a shard map) that is used for the external table.</span></span>  

<span data-ttu-id="5c038-141">Les clauses SCHEMA\_NAME et OBJECT\_NAME mappent la définition de table externe à une table dans un schéma différent.</span><span class="sxs-lookup"><span data-stu-id="5c038-141">The SCHEMA\_NAME and OBJECT\_NAME clauses map the external table definition to a table in a different schema.</span></span> <span data-ttu-id="5c038-142">En cas d’omission, le schéma de l’objet distant est supposé de type « dbo » et son nom est supposé être identique au nom de la table externe en cours de définition.</span><span class="sxs-lookup"><span data-stu-id="5c038-142">If omitted, the schema of the remote object is assumed to be “dbo” and its name is assumed to be identical to the external table name being defined.</span></span> <span data-ttu-id="5c038-143">Ceci est particulièrement utile si le nom de votre table distante est déjà utilisé dans la base de données dans laquelle vous souhaitez créer la table externe.</span><span class="sxs-lookup"><span data-stu-id="5c038-143">This is useful if the name of your remote table is already taken in the database where you want to create the external table.</span></span> <span data-ttu-id="5c038-144">Par exemple, vous souhaitez définir une table externe pour obtenir une vue agrégée des affichages de catalogue ou de vues de gestion dynamiques sur la couche des données mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="5c038-144">For  example, you want to define an external table to get an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="5c038-145">Dans la mesure où les affichages catalogue et les vues de gestion dynamique existent déjà localement, vous ne pouvez pas utiliser leur nom pour la définition de la table externe.</span><span class="sxs-lookup"><span data-stu-id="5c038-145">Since catalog views and DMVs already exist locally, you cannot use their names for the external table definition.</span></span> <span data-ttu-id="5c038-146">Vous devez utiliser un autre nom et le nom de la vue de catalogue ou de la vue de gestion dynamique dans les clauses SCHEMA\_NAME et/ou OBJECT\_NAME.</span><span class="sxs-lookup"><span data-stu-id="5c038-146">Instead, use a different name and use the catalog view’s or the DMV’s name in the SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="5c038-147">(Voir l’exemple ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="5c038-147">(See the example below.)</span></span> 

<span data-ttu-id="5c038-148">La clause DISTRIBUTION spécifie la distribution des données utilisée pour cette table.</span><span class="sxs-lookup"><span data-stu-id="5c038-148">The DISTRIBUTION clause specifies the data distribution used for this table.</span></span> <span data-ttu-id="5c038-149">Le processeur de requêtes utilise les informations fournies dans la clause DISTRIBUTION pour créer les plans de requête les plus efficaces.</span><span class="sxs-lookup"><span data-stu-id="5c038-149">The query processor utilizes the information provided in the DISTRIBUTION clause to build the most efficient query plans.</span></span>  

1. <span data-ttu-id="5c038-150">**SHARDED** signifie que les données sont partitionnées horizontalement entre les bases de données.</span><span class="sxs-lookup"><span data-stu-id="5c038-150">**SHARDED** means data is horizontally partitioned across the databases.</span></span> <span data-ttu-id="5c038-151">La clé de partitionnement pour la distribution des données figure dans le paramètre **<nom_colonne_partitionnement>**.</span><span class="sxs-lookup"><span data-stu-id="5c038-151">The partitioning key for the data distribution is the **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="5c038-152">**REPLICATED** signifie que des copies identiques de la table sont présentes sur chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="5c038-152">**REPLICATED** means that identical copies of the table are present on each database.</span></span> <span data-ttu-id="5c038-153">La responsabilité de vous assurer que les réplicas sont identiques d’une base de données à l’autre vous incombe.</span><span class="sxs-lookup"><span data-stu-id="5c038-153">It is your responsibility to ensure that the replicas are identical across the databases.</span></span>
3. <span data-ttu-id="5c038-154">**ROUND\_ROBIN** signifie que la table est partitionnée horizontalement à l’aide d’une méthode de distribution liée à l’application.</span><span class="sxs-lookup"><span data-stu-id="5c038-154">**ROUND\_ROBIN** means that the table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="5c038-155">**Référence de couche de données**: la table externe DDL fait référence à une source de données externe.</span><span class="sxs-lookup"><span data-stu-id="5c038-155">**Data tier reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="5c038-156">La source de données externe spécifie un mappage de partition qui fournit à la table externe les informations nécessaires à la localisation de toutes les bases de données de votre couche de données.</span><span class="sxs-lookup"><span data-stu-id="5c038-156">The external data source specifies a shard map which provides the external table with the information necessary to locate all the databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="5c038-157">Sécurité</span><span class="sxs-lookup"><span data-stu-id="5c038-157">Security considerations</span></span>
<span data-ttu-id="5c038-158">Les utilisateurs ayant accès à la table externe acquièrent un accès automatique aux tables distantes sous-jacentes avec les informations d’identification fournies dans la définition de source de données externe.</span><span class="sxs-lookup"><span data-stu-id="5c038-158">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="5c038-159">Évitez une élévation de privilèges non souhaitée par le biais d’informations d'identification de la source de données externe.</span><span class="sxs-lookup"><span data-stu-id="5c038-159">Avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="5c038-160">Utilisez GRANT ou REVOKE pour une table externe, comme s'il s'agissait d'une table standard.</span><span class="sxs-lookup"><span data-stu-id="5c038-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="5c038-161">Une fois votre table externe et votre source de données externe définies, vous pouvez utiliser l’ensemble T-SQL complet sur vos tables externes.</span><span class="sxs-lookup"><span data-stu-id="5c038-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="5c038-162">Exemple : interrogation de bases de données partitionnées horizontales</span><span class="sxs-lookup"><span data-stu-id="5c038-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="5c038-163">La requête suivante effectue une jonction tridirectionnelle entre les entrepôts, les commandes et les lignes de commande, et utilise plusieurs agrégats et un filtre sélectif.</span><span class="sxs-lookup"><span data-stu-id="5c038-163">The following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="5c038-164">Elle suppose (1) un partitionnement horizontal (partitionnement) et (2) que les entrepôts, les commandes et lignes de commande sont partitionnées par la colonne d’id de l’entrepôt et que la requête élastique peut placer des jointures sur les partitions et traiter la partie coûteuse de la requête sur les partitions en parallèle.</span><span class="sxs-lookup"><span data-stu-id="5c038-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by the warehouse id column, and that the elastic query can co-locate the joins on the shards and process the expensive part of the query on the shards in parallel.</span></span> 

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

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="5c038-165">Procédure stockée pour l’exécution de T-SQL à distance : sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="5c038-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="5c038-166">La requête élastique introduit également une procédure stockée qui offre un accès direct aux partitions.</span><span class="sxs-lookup"><span data-stu-id="5c038-166">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="5c038-167">La procédure stockée est appelée [sp\_execute\_remote](https://msdn.microsoft.com/library/mt703714) et peut être utilisée pour exécuter le code T-SQL ou les procédures stockées distantes sur des bases de données distantes.</span><span class="sxs-lookup"><span data-stu-id="5c038-167">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="5c038-168">Les paramètres suivants sont pris en compte :</span><span class="sxs-lookup"><span data-stu-id="5c038-168">It takes the following parameters:</span></span> 

* <span data-ttu-id="5c038-169">Nom de la source de données (nvarchar) : nom de la source de données externe de type SGBDR.</span><span class="sxs-lookup"><span data-stu-id="5c038-169">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="5c038-170">Requête (nvarchar) : requête T-SQL à exécuter sur chaque partition.</span><span class="sxs-lookup"><span data-stu-id="5c038-170">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="5c038-171">Déclaration de paramètre (nvarchar) : facultatif : chaîne contenant des définitions de type de données correspondant aux paramètres utilisés dans le paramètre de requête (par exemple, sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="5c038-171">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="5c038-172">Liste de valeurs de paramètre : facultative : valeurs de paramètre de liste séparées par des virgules (par exemple, sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="5c038-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="5c038-173">sp\_execute\_remote utilise la source de données externe fournie dans les paramètres d’appel pour exécuter l’instruction T-SQL donnée sur toutes les bases de données distantes.</span><span class="sxs-lookup"><span data-stu-id="5c038-173">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="5c038-174">Il utilise les informations d’identification de la source de données externe pour se connecter à la base de données shardmap et aux bases de données distantes.</span><span class="sxs-lookup"><span data-stu-id="5c038-174">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="5c038-175">Exemple :</span><span class="sxs-lookup"><span data-stu-id="5c038-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="5c038-176">Connectivité des outils</span><span class="sxs-lookup"><span data-stu-id="5c038-176">Connectivity for tools</span></span>
<span data-ttu-id="5c038-177">Utilisez des chaînes de connexion SQL Server standard pour connecter votre application, vos outils d’intégration BI et des données de la base de données avec vos définitions de table externe.</span><span class="sxs-lookup"><span data-stu-id="5c038-177">Use regular SQL Server connection strings to connect your application, your BI and data integration tools to the database with your external table definitions.</span></span> <span data-ttu-id="5c038-178">Assurez-vous que SQL Server est pris en charge comme source de données pour votre outil.</span><span class="sxs-lookup"><span data-stu-id="5c038-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="5c038-179">Référencez la base de données de requête élastique comme n’importe quelle autre base de données SQL Server connectée à l’outil et utilisez des tables externes à partir de votre outil ou votre application comme s’il s’agissait de tables locales.</span><span class="sxs-lookup"><span data-stu-id="5c038-179">Then reference the elastic query database like any other SQL Server database connected to the tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="5c038-180">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="5c038-180">Best practices</span></span>
* <span data-ttu-id="5c038-181">Assurez-vous que la base de données du point de terminaison de requête élastique est autorisée à accéder à la base de données de mappage de partition et à toutes les partitions via les pare-feu de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="5c038-181">Ensure that the elastic query endpoint database has been given access to the shardmap database and all shards through the SQL DB firewalls.</span></span>  
* <span data-ttu-id="5c038-182">Validez ou appliquez la distribution de données définie par la table externe.</span><span class="sxs-lookup"><span data-stu-id="5c038-182">Validate or enforce the data distribution defined by the external table.</span></span> <span data-ttu-id="5c038-183">Si la distribution réelle des données est différente de la distribution spécifiée dans la définition de votre table, vos requêtes peuvent donner des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="5c038-183">If your actual data distribution is different from the distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="5c038-184">La requête élastique n’effectue pas d’élimination de partition lorsque les prédicats de clé de partitionnement permettent d’exclure en toute sécurité certaines partitions du traitement.</span><span class="sxs-lookup"><span data-stu-id="5c038-184">Elastic query currently does not perform shard elimination when predicates over the sharding key would allow it to safely exclude certain shards from processing.</span></span>
* <span data-ttu-id="5c038-185">Une requête élastique est mieux adaptée aux requêtes dont la plus grande partie du calcul peut être effectuée sur les partitions.</span><span class="sxs-lookup"><span data-stu-id="5c038-185">Elastic query works best for queries where most of the computation can be done on the shards.</span></span> <span data-ttu-id="5c038-186">De manière générale, vous obtenez les meilleures performances de requête avec des prédicats de filtres sélectifs pouvant être évalués sur des partitions ou des jonctions via les clés de partitionnement qui peuvent être effectuées de manière alignée sur toutes les partitions.</span><span class="sxs-lookup"><span data-stu-id="5c038-186">You typically get the best query performance with selective filter predicates that can be evaluated on the shards or joins over the partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="5c038-187">D’autres modèles de requête peuvent nécessiter le chargement de grandes quantités de données dans le nœud principal, à partir des partitions, ce qui peut nuire aux performances.</span><span class="sxs-lookup"><span data-stu-id="5c038-187">Other query patterns may need to load large amounts of data from the shards to the head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c038-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5c038-188">Next steps</span></span>

* <span data-ttu-id="5c038-189">Pour une présentation des requêtes élastiques, consultez [Présentation des requêtes élastiques](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c038-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="5c038-190">Pour le didacticiel sur le partitionnement vertical, consultez [Prise en main des requêtes de bases de données croisées (partitionnement vertical)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="5c038-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="5c038-191">Pour la syntaxe et des exemples de requêtes pour des données partitionnées verticalement, consultez [Requêtes sur des données partitionnées verticalement](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="5c038-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="5c038-192">Pour commencer le didacticiel sur le partitionnement horizontal (sharding), consultez [Prise en main des requêtes élastiques pour le partitionnement horizontal (sharding)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5c038-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="5c038-193">Consultez [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) pour une procédure stockée qui exécute une instruction Transact-SQL sur une seule base de données Azure SQL distante ou un ensemble de bases de données servant de partitions dans un schéma de partitionnement horizontal.</span><span class="sxs-lookup"><span data-stu-id="5c038-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
