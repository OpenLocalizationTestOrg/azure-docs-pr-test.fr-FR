---
title: "aaaQuery sur cloud aux bases de données autre schéma | Documents Microsoft"
description: "Comment tooset les requêtes entre bases de données sur les partitions verticales"
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
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="64e23-103">Interroger des bases de données cloud de schémas différents (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="64e23-103">Query across cloud databases with different schemas (preview)</span></span>
![Requête sur plusieurs tables dans des bases de données différentes][1]

<span data-ttu-id="64e23-105">Les bases de données partitionnées verticalement utilisent différents ensembles de tables sur différentes bases de données.</span><span class="sxs-lookup"><span data-stu-id="64e23-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="64e23-106">Cela signifie que ce schéma hello est différent sur les différentes bases de données.</span><span class="sxs-lookup"><span data-stu-id="64e23-106">That means that hello schema is different on different databases.</span></span> <span data-ttu-id="64e23-107">Par exemple, toutes les tables d’inventaire se trouvent sur une base de données alors que toutes les tables liées à la comptabilité se trouvent dans une seconde base de données.</span><span class="sxs-lookup"><span data-stu-id="64e23-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="64e23-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="64e23-108">Prerequisites</span></span>
* <span data-ttu-id="64e23-109">utilisateur de Hello doit posséder les autorisations ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="64e23-109">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="64e23-110">Cette autorisation est incluse avec l’autorisation ALTER DATABASE hello.</span><span class="sxs-lookup"><span data-stu-id="64e23-110">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="64e23-111">Les autorisations ALTER ANY EXTERNAL DATA SOURCE sont toohello nécessaires toorefer source de données sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="64e23-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="64e23-112">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="64e23-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="64e23-113">À la différence avec le partitionnement horizontal, ces instructions DDL ne dépendent pas définir un niveau de données avec une carte de partitions via la bibliothèque cliente de base de données élastique hello.</span><span class="sxs-lookup"><span data-stu-id="64e23-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through hello elastic database client library.</span></span>
>

1. [<span data-ttu-id="64e23-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="64e23-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="64e23-115">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="64e23-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="64e23-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="64e23-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="64e23-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="64e23-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="64e23-118">Créer la clé principale et les informations d’identification de la base de données</span><span class="sxs-lookup"><span data-stu-id="64e23-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="64e23-119">informations d’identification Hello sont utilisée par hello requête élastique tooconnect tooyour bases de données distantes.</span><span class="sxs-lookup"><span data-stu-id="64e23-119">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="64e23-120">Vérifiez que hello `<username>` ne comprend aucun **»@servername»** suffixe.</span><span class="sxs-lookup"><span data-stu-id="64e23-120">Ensure that hello `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="64e23-121">Créer des sources de données externes</span><span class="sxs-lookup"><span data-stu-id="64e23-121">Create external data sources</span></span>
<span data-ttu-id="64e23-122">Syntaxe :</span><span class="sxs-lookup"><span data-stu-id="64e23-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="64e23-123">paramètre de TYPE Hello doit être défini trop**SGBDR**.</span><span class="sxs-lookup"><span data-stu-id="64e23-123">hello TYPE parameter must be set too**RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="64e23-124">Exemple</span><span class="sxs-lookup"><span data-stu-id="64e23-124">Example</span></span>
<span data-ttu-id="64e23-125">Hello exemple suivant illustre utilisation hello Hello instruction de création de sources de données externes.</span><span class="sxs-lookup"><span data-stu-id="64e23-125">hello following example illustrates hello use of hello CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="64e23-126">liste de hello tooretrieve de sources de données externes en cours :</span><span class="sxs-lookup"><span data-stu-id="64e23-126">tooretrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="64e23-127">Tables externes</span><span class="sxs-lookup"><span data-stu-id="64e23-127">External Tables</span></span>
<span data-ttu-id="64e23-128">Syntaxe :</span><span class="sxs-lookup"><span data-stu-id="64e23-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="64e23-129">Exemple</span><span class="sxs-lookup"><span data-stu-id="64e23-129">Example</span></span>
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

<span data-ttu-id="64e23-130">Bonjour à l’exemple suivant montre comment tooretrieve hello la liste des tables externes à partir de la base de données actuelle hello :</span><span class="sxs-lookup"><span data-stu-id="64e23-130">hello following example shows how tooretrieve hello list of external tables from hello current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="64e23-131">Remarques</span><span class="sxs-lookup"><span data-stu-id="64e23-131">Remarks</span></span>
<span data-ttu-id="64e23-132">Requête élastique étend hello table externe syntaxe toodefine externe tables existantes qui utilisent des sources de données externes de type SGBDR.</span><span class="sxs-lookup"><span data-stu-id="64e23-132">Elastic query extends hello existing external table syntax toodefine external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="64e23-133">Une définition de la table externe pour le partitionnement vertical couvre hello suivant aspects :</span><span class="sxs-lookup"><span data-stu-id="64e23-133">An external table definition for vertical partitioning covers hello following aspects:</span></span> 

* <span data-ttu-id="64e23-134">**Schéma**: une table externe hello DDL définit un schéma qui permettent de vos requêtes.</span><span class="sxs-lookup"><span data-stu-id="64e23-134">**Schema**: hello external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="64e23-135">schéma de Hello fourni dans votre définition de table externe requiert un schéma de hello toomatch de tables hello dans la base de données distante hello où sont stockées les données réelles hello.</span><span class="sxs-lookup"><span data-stu-id="64e23-135">hello schema provided in your external table definition needs toomatch hello schema of hello tables in hello remote database where hello actual data is stored.</span></span> 
* <span data-ttu-id="64e23-136">**Référence de base de données distante**: une table externe hello DDL fait référence la source de données externe tooan.</span><span class="sxs-lookup"><span data-stu-id="64e23-136">**Remote database reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="64e23-137">source de données externe Hello Spécifie le nom du serveur logique hello et le nom de la base de données de base de données distante hello où sont stockées les données de la table réelle hello.</span><span class="sxs-lookup"><span data-stu-id="64e23-137">hello external data source specifies hello logical server name and database name of hello remote database where hello actual table data is stored.</span></span> 

<span data-ttu-id="64e23-138">Les tables externes hello syntaxe toocreate à l’aide de source de données externe comme indiqué dans la section précédente de hello, est la suivante :</span><span class="sxs-lookup"><span data-stu-id="64e23-138">Using an external data source as outlined in hello previous section, hello syntax toocreate external tables is as follows:</span></span> 

<span data-ttu-id="64e23-139">clause DATA_SOURCE Hello définit la source de données externe hello (c'est-à-dire hello à distance de base de données en cas de partitionnement vertical) qui est utilisé pour une table externe hello.</span><span class="sxs-lookup"><span data-stu-id="64e23-139">hello DATA_SOURCE clause defines hello external data source (i.e. hello remote database in case of vertical partitioning) that is used for hello external table.</span></span>  

<span data-ttu-id="64e23-140">les clauses nom_schéma et nom_objet Hello fournissent hello capacité toomap hello table externe définition tooa table dans un schéma différent sur la base de données distante hello ou table tooa avec un nom différent, respectivement.</span><span class="sxs-lookup"><span data-stu-id="64e23-140">hello SCHEMA_NAME and OBJECT_NAME clauses provide hello ability toomap hello external table definition tooa table in a different schema on hello remote database, or tooa table with a different name, respectively.</span></span> <span data-ttu-id="64e23-141">Cela est utile si vous souhaitez que toodefine une vue de catalogue tooa table externe ou d’une vue de gestion dynamique sur votre base de données à distance - ou toute autre situation où nom de la table distante hello est déjà exécutée localement.</span><span class="sxs-lookup"><span data-stu-id="64e23-141">This is useful if you want toodefine an external table tooa catalog view or DMV on your remote database - or any other situation where hello remote table name is already taken locally.</span></span>  

<span data-ttu-id="64e23-142">Hello instruction DDL suivante supprime une définition existante de la table externe à partir du catalogue local d’hello.</span><span class="sxs-lookup"><span data-stu-id="64e23-142">hello following DDL statement drops an existing external table definition from hello local catalog.</span></span> <span data-ttu-id="64e23-143">Il n’affecte pas la base de données distante hello.</span><span class="sxs-lookup"><span data-stu-id="64e23-143">It does not impact hello remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="64e23-144">**Autorisations pour la TABLE externe de CREATE/DROP**: les autorisations ALTER ANY EXTERNAL DATA SOURCE sont nécessaires pour la table externe DDL qui est également nécessaire de source de données sous-jacente toorefer toohello.</span><span class="sxs-lookup"><span data-stu-id="64e23-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed toorefer toohello underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="64e23-145">Considérations relatives à la sécurité</span><span class="sxs-lookup"><span data-stu-id="64e23-145">Security considerations</span></span>
<span data-ttu-id="64e23-146">Les utilisateurs avec une table externe accès toohello automatiquement accéder toohello les tables distantes sous-jacentes sous les informations d’identification hello donné dans la définition de source de données externe hello.</span><span class="sxs-lookup"><span data-stu-id="64e23-146">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="64e23-147">Vous devez gérer avec soin de table externe de toohello accès dans l’ordre tooavoid indésirables d’élever les privilèges via les informations d’identification hello hello externe de source de données.</span><span class="sxs-lookup"><span data-stu-id="64e23-147">You should carefully manage access toohello external table in order tooavoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="64e23-148">Les autorisations SQL régulières peuvent être tooGRANT utilisé ou une table externe de RÉVOQUER l’accès tooan comme s’il s’agissait d’une table normale.</span><span class="sxs-lookup"><span data-stu-id="64e23-148">Regular SQL permissions can be used tooGRANT or REVOKE access tooan external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="64e23-149">Exemple : interrogation de bases de données partitionnées verticalement</span><span class="sxs-lookup"><span data-stu-id="64e23-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="64e23-150">Hello requête suivante effectue une jointure tridirectionnelle entre deux tables locales hello pour les commandes et les lignes de commande et de la table distante de hello pour les clients.</span><span class="sxs-lookup"><span data-stu-id="64e23-150">hello following query performs a three-way join between hello two local tables for orders and order lines and hello remote table for customers.</span></span> <span data-ttu-id="64e23-151">Il s’agit d’un exemple de cas d’utilisation de données d’hello référence de requête élastique :</span><span class="sxs-lookup"><span data-stu-id="64e23-151">This is an example of hello reference data use case for elastic query:</span></span> 

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


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="64e23-152">Procédure stockée pour l’exécution de T-SQL à distance : sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="64e23-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="64e23-153">Requête élastique présente également une procédure stockée qui offre un accès direct toohello partitions.</span><span class="sxs-lookup"><span data-stu-id="64e23-153">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="64e23-154">Hello procédure stockée est appelée [sp\_exécuter \_distant](https://msdn.microsoft.com/library/mt703714) et peut être utilisé tooexecute des procédures stockées distantes ou le code T-SQL sur des bases de données distantes hello.</span><span class="sxs-lookup"><span data-stu-id="64e23-154">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="64e23-155">Il prend hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="64e23-155">It takes hello following parameters:</span></span> 

* <span data-ttu-id="64e23-156">Nom de source de données (nvarchar) : nom hello hello externe de source de données de type SGBDR.</span><span class="sxs-lookup"><span data-stu-id="64e23-156">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="64e23-157">Requête (nvarchar) : hello T-SQL toobe de requête exécutée sur chaque partition.</span><span class="sxs-lookup"><span data-stu-id="64e23-157">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="64e23-158">Déclaration de paramètre (nvarchar) - facultatif : chaîne avec les définitions de type de données pour les paramètres de hello utilisés dans le paramètre de requête hello (comme sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="64e23-158">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="64e23-159">Liste de valeurs de paramètre : facultative : valeurs de paramètre de liste séparées par des virgules (par exemple, sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="64e23-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="64e23-160">Hello sp\_exécuter\_distant utilise hello prévue hello appel paramètres tooexecute hello donné l’instruction T-SQL sur des bases de données distantes hello de source de données externe.</span><span class="sxs-lookup"><span data-stu-id="64e23-160">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="64e23-161">Elle utilise les informations d’identification hello de hello données externes tooconnect toohello shardmap manager base de données source et de bases de données distantes hello.</span><span class="sxs-lookup"><span data-stu-id="64e23-161">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="64e23-162">Exemple :</span><span class="sxs-lookup"><span data-stu-id="64e23-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="64e23-163">Connectivité des outils</span><span class="sxs-lookup"><span data-stu-id="64e23-163">Connectivity for tools</span></span>
<span data-ttu-id="64e23-164">Vous pouvez utiliser tooconnect de chaînes de connexion SQL Server standard votre toodatabases d’outils de l’intégration BI et les données sur serveur de base de données SQL hello qui a activé de requête élastique et des tables externes définies.</span><span class="sxs-lookup"><span data-stu-id="64e23-164">You can use regular SQL Server connection strings tooconnect your BI and data integration tools toodatabases on hello SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="64e23-165">Assurez-vous que SQL Server est pris en charge comme source de données pour votre outil.</span><span class="sxs-lookup"><span data-stu-id="64e23-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="64e23-166">Faites ensuite référence toohello de requêtes élastique de base de données et ses tables externes comme toute autre base de données de SQL Server que vous devez vous connecter toowith votre outil.</span><span class="sxs-lookup"><span data-stu-id="64e23-166">Then refer toohello elastic query database and its external tables just like any other SQL Server database that you would connect toowith your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="64e23-167">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="64e23-167">Best practices</span></span>
* <span data-ttu-id="64e23-168">Vérifiez la que base de données access toohello à distance en activant l’accès pour les Services Azure dans sa configuration de pare-feu de base de données SQL a été donné à cette base de données de point de terminaison de la requête élastique hello.</span><span class="sxs-lookup"><span data-stu-id="64e23-168">Ensure that hello elastic query endpoint database has been given access toohello remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="64e23-169">Vérifiez également ces informations d’identification hello fourni dans les données externes hello définition de la source peut se connecter à la base de données distante hello et a la table distante de hello autorisations tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="64e23-169">Also ensure that hello credential provided in hello external data source definition can successfully log into hello remote database and has hello permissions tooaccess hello remote table.</span></span>  
* <span data-ttu-id="64e23-170">Requête élastique mieux adaptée pour les requêtes où la plupart des calculs de hello peut être effectuée sur les bases de données distantes hello.</span><span class="sxs-lookup"><span data-stu-id="64e23-170">Elastic query works best for queries where most of hello computation can be done on hello remote databases.</span></span> <span data-ttu-id="64e23-171">Vous obtenez généralement de meilleures performances des requêtes hello avec des prédicats de filtre sélectif qui peut être évaluée sur les bases de données distantes hello ou des jointures qui peuvent être effectuées complètement sur la base de données distante hello.</span><span class="sxs-lookup"><span data-stu-id="64e23-171">You typically get hello best query performance with selective filter predicates that can be evaluated on hello remote databases or joins that can be performed completely on hello remote database.</span></span> <span data-ttu-id="64e23-172">Autres modèles de requête peuvent nécessiter des tooload grandes quantités de données à partir de la base de données distante hello et peuvent être lent.</span><span class="sxs-lookup"><span data-stu-id="64e23-172">Other query patterns may need tooload large amounts of data from hello remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="64e23-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="64e23-173">Next steps</span></span>

* <span data-ttu-id="64e23-174">Pour une présentation des requêtes élastiques, consultez [Présentation des requêtes élastiques](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64e23-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="64e23-175">Pour le didacticiel sur le partitionnement vertical, consultez [Prise en main des requêtes de bases de données croisées (partitionnement vertical)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="64e23-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="64e23-176">Pour commencer le didacticiel sur le partitionnement horizontal (sharding), consultez [Prise en main des requêtes élastiques pour le partitionnement horizontal (sharding)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="64e23-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="64e23-177">Pour la syntaxe et des exemples de requêtes pour des données partitionnées horizontalement, consultez [Requêtes sur des données partitionnées horizontalement](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="64e23-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="64e23-178">Consultez [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) pour une procédure stockée qui exécute une instruction Transact-SQL sur une seule base de données Azure SQL distante ou un ensemble de bases de données servant de partitions dans un schéma de partitionnement horizontal.</span><span class="sxs-lookup"><span data-stu-id="64e23-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
