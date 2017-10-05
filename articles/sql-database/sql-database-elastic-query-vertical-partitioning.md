---
title: "Interroger des bases de données cloud de schémas différents | Documents Microsoft Azure"
description: "configuration de requêtes de bases de données croisées sur les partitions verticales"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: e9036f92f6c76e8c4738ee981efa8a7b9791dcc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="0f3ac-103">Interroger des bases de données cloud de schémas différents (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="0f3ac-103">Query across cloud databases with different schemas (preview)</span></span>
![Requête sur plusieurs tables dans des bases de données différentes][1]

<span data-ttu-id="0f3ac-105">Les bases de données partitionnées verticalement utilisent différents ensembles de tables sur différentes bases de données.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="0f3ac-106">Cela signifie que le schéma est différent sur des bases de données différentes.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-106">That means that the schema is different on different databases.</span></span> <span data-ttu-id="0f3ac-107">Par exemple, toutes les tables d’inventaire se trouvent sur une base de données alors que toutes les tables liées à la comptabilité se trouvent dans une seconde base de données.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0f3ac-108">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="0f3ac-108">Prerequisites</span></span>
* <span data-ttu-id="0f3ac-109">L’utilisateur doit posséder l’autorisation ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-109">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="0f3ac-110">Cette autorisation est incluse dans l’autorisation ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-110">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="0f3ac-111">Les autorisations ALTER ANY EXTERNAL DATA SOURCE sont nécessaires pour faire référence à la source de données sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="0f3ac-112">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0f3ac-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="0f3ac-113">Contrairement au partitionnement horizontal, ces instructions DDL ne dépendent pas de la définition d’une couche de données avec un mappage de partition via la bibliothèque client de base de données élastique.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through the elastic database client library.</span></span>
>

1. [<span data-ttu-id="0f3ac-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="0f3ac-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="0f3ac-115">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="0f3ac-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="0f3ac-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="0f3ac-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="0f3ac-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="0f3ac-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="0f3ac-118">Créer la clé principale et les informations d’identification de la base de données</span><span class="sxs-lookup"><span data-stu-id="0f3ac-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="0f3ac-119">Les informations d'identification sont utilisées par la requête élastique pour se connecter à vos bases de données distantes.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-119">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="0f3ac-120">Veillez à ce que `<username>` ne contienne pas le suffixe **« @servername »**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-120">Ensure that the `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="0f3ac-121">Créer des sources de données externes</span><span class="sxs-lookup"><span data-stu-id="0f3ac-121">Create external data sources</span></span>
<span data-ttu-id="0f3ac-122">Syntaxe :</span><span class="sxs-lookup"><span data-stu-id="0f3ac-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="0f3ac-123">Le paramètre TYPE doit être défini sur **RDBMS**.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-123">The TYPE parameter must be set to **RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="0f3ac-124">Exemple</span><span class="sxs-lookup"><span data-stu-id="0f3ac-124">Example</span></span>
<span data-ttu-id="0f3ac-125">L’exemple suivant illustre l’utilisation de l’instruction CREATE pour les sources de données externes.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-125">The following example illustrates the use of the CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="0f3ac-126">Pour récupérer la liste des sources de données externes actuelles :</span><span class="sxs-lookup"><span data-stu-id="0f3ac-126">To retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="0f3ac-127">Tables externes</span><span class="sxs-lookup"><span data-stu-id="0f3ac-127">External Tables</span></span>
<span data-ttu-id="0f3ac-128">Syntaxe :</span><span class="sxs-lookup"><span data-stu-id="0f3ac-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="0f3ac-129">Exemple</span><span class="sxs-lookup"><span data-stu-id="0f3ac-129">Example</span></span>
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

<span data-ttu-id="0f3ac-130">L’exemple suivant illustre comment récupérer la liste des tables externes à partir de la base de données en cours :</span><span class="sxs-lookup"><span data-stu-id="0f3ac-130">The following example shows how to retrieve the list of external tables from the current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="0f3ac-131">Remarques</span><span class="sxs-lookup"><span data-stu-id="0f3ac-131">Remarks</span></span>
<span data-ttu-id="0f3ac-132">La requête élastique étend la syntaxe de la table externe existante pour définir des tables externes qui utilisent des sources de données externes de type SGBDR.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-132">Elastic query extends the existing external table syntax to define external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="0f3ac-133">Une définition de table externe pour le partitionnement vertical couvre les aspects suivants :</span><span class="sxs-lookup"><span data-stu-id="0f3ac-133">An external table definition for vertical partitioning covers the following aspects:</span></span> 

* <span data-ttu-id="0f3ac-134">**Schéma**: la table externe DDL définit un schéma que vos requêtes peuvent utiliser.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-134">**Schema**: The external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="0f3ac-135">Le schéma fourni dans votre définition de la table externe doit correspondre au schéma des tables appartenant à la base de données externe sur lesquelles sont stockées les données réelles.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-135">The schema provided in your external table definition needs to match the schema of the tables in the remote database where the actual data is stored.</span></span> 
* <span data-ttu-id="0f3ac-136">**Base de données distante**: la table externe DDL fait référence à une source de données externe.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-136">**Remote database reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="0f3ac-137">La source de données externe spécifie le nom du serveur logique et le nom de la base de données distante dans laquelle sont stockées les données réelles du tableau.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-137">The external data source specifies the logical server name and database name of the remote database where the actual table data is stored.</span></span> 

<span data-ttu-id="0f3ac-138">La syntaxe permettant de créer des tables externes à l’aide de sources de données externes comme indiqué dans la section précédente est la suivante :</span><span class="sxs-lookup"><span data-stu-id="0f3ac-138">Using an external data source as outlined in the previous section, the syntax to create external tables is as follows:</span></span> 

<span data-ttu-id="0f3ac-139">La clause DATA_SOURCE définit la source de données externe (par exemple, la base de données distante en cas de partitionnement horizontal) utilisée pour la table externe.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-139">The DATA_SOURCE clause defines the external data source (i.e. the remote database in case of vertical partitioning) that is used for the external table.</span></span>  

<span data-ttu-id="0f3ac-140">Les clauses SCHEMA_NAME et OBJECT_NAME offrent la possibilité de mapper une définition de table externe sur une table dans un autre schéma base de données, ou sur une table portant un autre nom, respectivement.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-140">The SCHEMA_NAME and OBJECT_NAME clauses provide the ability to map the external table definition to a table in a different schema on the remote database, or to a table with a different name, respectively.</span></span> <span data-ttu-id="0f3ac-141">Cela s’avère utile si vous souhaitez définir une table externe sur une vue de catalogue ou une vue de gestion dynamique sur votre base de données distante, ou dans toute autre situation dans laquelle le nom de table distant est déjà utilisé en local.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-141">This is useful if you want to define an external table to a catalog view or DMV on your remote database - or any other situation where the remote table name is already taken locally.</span></span>  

<span data-ttu-id="0f3ac-142">L’instruction DDL suivante supprime une définition de table externe existante du catalogue local.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-142">The following DDL statement drops an existing external table definition from the local catalog.</span></span> <span data-ttu-id="0f3ac-143">Elle n’affecte pas la base de données distante.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-143">It does not impact the remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="0f3ac-144">**Autorisations CREATE/DROP EXTERNAL TABLE** : les autorisations ALTER ANY EXTERNAL DATA SOURCE sont nécessaires à la table DDL externe et à la source de données sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed to refer to the underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="0f3ac-145">Sécurité</span><span class="sxs-lookup"><span data-stu-id="0f3ac-145">Security considerations</span></span>
<span data-ttu-id="0f3ac-146">Les utilisateurs ayant accès à la table externe acquièrent un accès automatique aux tables distantes sous-jacentes avec les informations d’identification fournies dans la définition de source de données externe.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-146">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="0f3ac-147">Vous devez gérer l’accès à la table externe avec beaucoup d’attention pour éviter une élévation de privilèges non souhaitée par le biais d’informations d’identification de la source de données externe.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-147">You should carefully manage access to the external table in order to avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="0f3ac-148">Les autorisations SQL standard permettent de GRANT (OCTROYER) ou de REVOKE (RÉVOQUER) l’accès à une table externe comme s’il s’agissait d’une table normale.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-148">Regular SQL permissions can be used to GRANT or REVOKE access to an external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="0f3ac-149">Exemple : interrogation de bases de données partitionnées verticalement</span><span class="sxs-lookup"><span data-stu-id="0f3ac-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="0f3ac-150">La requête suivante effectue une jointure tridirectionnelle entre les deux tables locales pour les commandes, et les lignes de commande et la table distante pour les clients.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-150">The following query performs a three-way join between the two local tables for orders and order lines and the remote table for customers.</span></span> <span data-ttu-id="0f3ac-151">Voici un exemple de cas d’utilisation de données de référence pour requête élastique :</span><span class="sxs-lookup"><span data-stu-id="0f3ac-151">This is an example of the reference data use case for elastic query:</span></span> 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="0f3ac-152">Procédure stockée pour l’exécution de T-SQL à distance : sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="0f3ac-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="0f3ac-153">La requête élastique introduit également une procédure stockée qui offre un accès direct aux partitions.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-153">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="0f3ac-154">La procédure stockée est appelée [sp\_execute\_remote](https://msdn.microsoft.com/library/mt703714) et peut être utilisée pour exécuter le code T-SQL ou les procédures stockées distantes sur des bases de données distantes.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-154">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="0f3ac-155">Les paramètres suivants sont pris en compte :</span><span class="sxs-lookup"><span data-stu-id="0f3ac-155">It takes the following parameters:</span></span> 

* <span data-ttu-id="0f3ac-156">Nom de la source de données (nvarchar) : nom de la source de données externe de type SGBDR.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-156">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="0f3ac-157">Requête (nvarchar) : requête T-SQL à exécuter sur chaque partition.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-157">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="0f3ac-158">Déclaration de paramètre (nvarchar) : facultatif : chaîne contenant des définitions de type de données correspondant aux paramètres utilisés dans le paramètre de requête (par exemple, sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="0f3ac-158">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="0f3ac-159">Liste de valeurs de paramètre : facultative : valeurs de paramètre de liste séparées par des virgules (par exemple, sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="0f3ac-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="0f3ac-160">sp\_execute\_remote utilise la source de données externe fournie dans les paramètres d’appel pour exécuter l’instruction T-SQL donnée sur toutes les bases de données distantes.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-160">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="0f3ac-161">Il utilise les informations d’identification de la source de données externe pour se connecter à la base de données shardmap et aux bases de données distantes.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-161">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="0f3ac-162">Exemple :</span><span class="sxs-lookup"><span data-stu-id="0f3ac-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="0f3ac-163">Connectivité des outils</span><span class="sxs-lookup"><span data-stu-id="0f3ac-163">Connectivity for tools</span></span>
<span data-ttu-id="0f3ac-164">Vous pouvez utiliser des chaînes de connexion SQL Server standard pour connecter votre BI et vos outils d’intégration aux bases de données sur le serveur SQL DB dont la requête élastique est activée et les tables externes définies.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-164">You can use regular SQL Server connection strings to connect your BI and data integration tools to databases on the SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="0f3ac-165">Assurez-vous que SQL Server est pris en charge comme source de données pour votre outil.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="0f3ac-166">Reportez-vous ensuite à la requête de base de données élastique et à ses tables externes comme s’il s’agissait de n’importe quelle autre base de données SQL Server à laquelle vous vous connectez avec votre outil.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-166">Then refer to the elastic query database and its external tables just like any other SQL Server database that you would connect to with your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="0f3ac-167">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="0f3ac-167">Best practices</span></span>
* <span data-ttu-id="0f3ac-168">Assurez-vous que la base de données du point de terminaison de requête élastique est autorisée à accéder à la base de données distante en autorisant l’accès des Services Azure dans sa configuration de pare-feu SQL DB.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-168">Ensure that the elastic query endpoint database has been given access to the remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="0f3ac-169">Vérifiez également que les informations d’identification fournies dans la définition de source de données externe peuvent se connecter à la base de données distante et qu’elles bénéficient des autorisations d’accès à la table distante.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-169">Also ensure that the credential provided in the external data source definition can successfully log into the remote database and has the permissions to access the remote table.</span></span>  
* <span data-ttu-id="0f3ac-170">Une requête élastique est mieux adaptée aux requêtes dont la plus grande partie du calcul peut être effectuée sur les bases de données distantes.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-170">Elastic query works best for queries where most of the computation can be done on the remote databases.</span></span> <span data-ttu-id="0f3ac-171">De manière générale, vous obtenez les meilleures performances de requête avec des prédicats de filtres sélectifs pouvant être évalués sur les bases de données ou des jointures distantes pouvant être exécutées en totalité sur la base de données distante.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-171">You typically get the best query performance with selective filter predicates that can be evaluated on the remote databases or joins that can be performed completely on the remote database.</span></span> <span data-ttu-id="0f3ac-172">D’autres modèles de requête peuvent nécessiter le chargement de grandes quantités de données de la base de données distante et s’exécuter de façon médiocre.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-172">Other query patterns may need to load large amounts of data from the remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0f3ac-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0f3ac-173">Next steps</span></span>

* <span data-ttu-id="0f3ac-174">Pour une présentation des requêtes élastiques, consultez [Présentation des requêtes élastiques](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f3ac-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="0f3ac-175">Pour le didacticiel sur le partitionnement vertical, consultez [Prise en main des requêtes de bases de données croisées (partitionnement vertical)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="0f3ac-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="0f3ac-176">Pour commencer le didacticiel sur le partitionnement horizontal (sharding), consultez [Prise en main des requêtes élastiques pour le partitionnement horizontal (sharding)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="0f3ac-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="0f3ac-177">Pour la syntaxe et des exemples de requêtes pour des données partitionnées horizontalement, consultez [Requêtes sur des données partitionnées horizontalement](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="0f3ac-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="0f3ac-178">Consultez [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) pour une procédure stockée qui exécute une instruction Transact-SQL sur une seule base de données Azure SQL distante ou un ensemble de bases de données servant de partitions dans un schéma de partitionnement horizontal.</span><span class="sxs-lookup"><span data-stu-id="0f3ac-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
