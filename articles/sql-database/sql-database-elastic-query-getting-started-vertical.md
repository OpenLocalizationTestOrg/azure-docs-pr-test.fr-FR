---
title: "aaaGet a démarré avec des requêtes de bases de données croisées (partitionnement vertical) | Documents Microsoft"
description: "la requête de base de données élastique toouse avec partitionné verticalement les bases de données"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: e5b44b10-c432-4f96-b20e-08615ff4d5dd
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: torsteng
ms.openlocfilehash: 9e6183268e8bf87e3ac28f502711fcc05a7a3f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="c421c-103">Prise en main des requêtes de bases de données croisées (partitionnement vertical) (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="c421c-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="c421c-104">Requête de base de données élastique (version préliminaire) pour la base de données SQL Azure vous permet de requêtes T-SQL toorun qui s’étendent sur plusieurs bases de données à l’aide d’un point de connexion unique.</span><span class="sxs-lookup"><span data-stu-id="c421c-104">Elastic database query (preview) for Azure SQL Database allows you toorun T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="c421c-105">Cette rubrique s’applique également[partitionné verticalement les bases de données](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="c421c-105">This topic applies too[vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="c421c-106">Issue, vous allez : Découvrez comment tooconfigure et utilisez une base de données SQL Azure de tooperform des requêtes qui couvrent plusieurs bases de données associées.</span><span class="sxs-lookup"><span data-stu-id="c421c-106">When completed, you will: learn how tooconfigure and use an Azure SQL Database tooperform queries that span multiple related databases.</span></span> 

<span data-ttu-id="c421c-107">Pour plus d’informations sur la fonctionnalité de requête de base de données élastique hello, consultez [présentation des requêtes de base de données SQL Azure de base de données élastique](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c421c-107">For more information about hello elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c421c-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c421c-108">Prerequisites</span></span>

<span data-ttu-id="c421c-109">Vous devez posséder l’autorisation ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="c421c-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="c421c-110">Cette autorisation est incluse avec l’autorisation ALTER DATABASE hello.</span><span class="sxs-lookup"><span data-stu-id="c421c-110">This permission is included with hello ALTER DATABASE permission.</span></span> <span data-ttu-id="c421c-111">Les autorisations ALTER ANY EXTERNAL DATA SOURCE sont toohello nécessaires toorefer source de données sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="c421c-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="create-hello-sample-databases"></a><span data-ttu-id="c421c-112">Créer des bases de données exemple hello</span><span class="sxs-lookup"><span data-stu-id="c421c-112">Create hello sample databases</span></span>
<span data-ttu-id="c421c-113">toostart avec, nous devons toocreate deux bases de données, **clients** et **commandes**, soit dans hello identiques ou différents serveurs logiques.</span><span class="sxs-lookup"><span data-stu-id="c421c-113">toostart with, we need toocreate two databases, **Customers** and **Orders**, either in hello same or different logical servers.</span></span>   

<span data-ttu-id="c421c-114">Exécutez hello suivant des requêtes de hello **commandes** hello toocreate de base de données **OrderInformation** table et entrée hello exemples de données.</span><span class="sxs-lookup"><span data-stu-id="c421c-114">Execute hello following queries on hello **Orders** database toocreate hello **OrderInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="c421c-115">Maintenant, exécutez la requête sur hello suivante **clients** hello toocreate de base de données **CustomerInformation** table et entrée hello exemples de données.</span><span class="sxs-lookup"><span data-stu-id="c421c-115">Now, execute following query on hello **Customers** database toocreate hello **CustomerInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="c421c-116">Créez des objets de base de données</span><span class="sxs-lookup"><span data-stu-id="c421c-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="c421c-117">Clé principale et informations d’identification de la base de données</span><span class="sxs-lookup"><span data-stu-id="c421c-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="c421c-118">Ouvrez SQL Server Management Studio ou SQL Server Data Tools dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c421c-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="c421c-119">Connecter la base de données des commandes toohello et exécuter hello suivant de commandes T-SQL :</span><span class="sxs-lookup"><span data-stu-id="c421c-119">Connect toohello Orders database and execute hello following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="c421c-120">Hello « username » et « password » doivent être nom d’utilisateur hello et mot de passe utilisé toologin dans la base de données des clients hello.</span><span class="sxs-lookup"><span data-stu-id="c421c-120">hello "username" and "password" should be hello username and password used toologin into hello Customers database.</span></span>
    <span data-ttu-id="c421c-121">L’authentification à l’aide d’Azure Active Directory avec des requêtes élastiques n’est pas prise en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="c421c-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="c421c-122">Sources de données externes</span><span class="sxs-lookup"><span data-stu-id="c421c-122">External data sources</span></span>
<span data-ttu-id="c421c-123">toocreate source de données externe, exécutez hello suivant de commande de base de données des commandes hello :</span><span class="sxs-lookup"><span data-stu-id="c421c-123">toocreate an external data source, execute hello following command on hello Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="c421c-124">Tables externes</span><span class="sxs-lookup"><span data-stu-id="c421c-124">External tables</span></span>
<span data-ttu-id="c421c-125">Créer une table externe sur base de données des commandes hello qui correspond à la définition de hello de table de CustomerInformation hello :</span><span class="sxs-lookup"><span data-stu-id="c421c-125">Create an external table on hello Orders database, which matches hello definition of hello CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="c421c-126">Exécutez un exemple de requête T-SQL de base de données élastique</span><span class="sxs-lookup"><span data-stu-id="c421c-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="c421c-127">Une fois que vous avez défini votre source de données externe et de vos tables externes, vous pouvez maintenant utiliser T-SQL tooquery vos tables externes.</span><span class="sxs-lookup"><span data-stu-id="c421c-127">Once you have defined your external data source and your external tables you can now use T-SQL tooquery your external tables.</span></span> <span data-ttu-id="c421c-128">Exécutez cette requête sur la base de données des commandes hello :</span><span class="sxs-lookup"><span data-stu-id="c421c-128">Execute this query on hello Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="c421c-129">Coût</span><span class="sxs-lookup"><span data-stu-id="c421c-129">Cost</span></span>
<span data-ttu-id="c421c-130">Actuellement, fonctionnalité de requête de base de données élastique hello est incluse dans le coût de hello de votre base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c421c-130">Currently, hello elastic database query feature is included into hello cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="c421c-131">Pour plus d’informations sur la tarification, voir [Tarification des bases de données SQL](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="c421c-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c421c-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c421c-132">Next steps</span></span>

* <span data-ttu-id="c421c-133">Pour une présentation des requêtes élastiques, consultez [Présentation des requêtes élastiques](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c421c-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="c421c-134">Pour la syntaxe et des exemples de requêtes pour des données partitionnées verticalement, consultez [Requêtes sur des données partitionnées verticalement](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="c421c-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="c421c-135">Pour commencer le didacticiel sur le partitionnement horizontal (sharding), consultez [Prise en main des requêtes élastiques pour le partitionnement horizontal (sharding)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c421c-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="c421c-136">Pour la syntaxe et des exemples de requêtes pour des données partitionnées horizontalement, consultez [Requêtes sur des données partitionnées horizontalement](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="c421c-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="c421c-137">Consultez [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) pour une procédure stockée qui exécute une instruction Transact-SQL sur une seule base de données Azure SQL distante ou un ensemble de bases de données servant de partitions dans un schéma de partitionnement horizontal.</span><span class="sxs-lookup"><span data-stu-id="c421c-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>