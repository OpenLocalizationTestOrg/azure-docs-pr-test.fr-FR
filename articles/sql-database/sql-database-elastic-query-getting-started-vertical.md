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
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a>Prise en main des requêtes de bases de données croisées (partitionnement vertical) (version préliminaire)
Requête de base de données élastique (version préliminaire) pour la base de données SQL Azure vous permet de requêtes T-SQL toorun qui s’étendent sur plusieurs bases de données à l’aide d’un point de connexion unique. Cette rubrique s’applique également[partitionné verticalement les bases de données](sql-database-elastic-query-vertical-partitioning.md).  

Issue, vous allez : Découvrez comment tooconfigure et utilisez une base de données SQL Azure de tooperform des requêtes qui couvrent plusieurs bases de données associées. 

Pour plus d’informations sur la fonctionnalité de requête de base de données élastique hello, consultez [présentation des requêtes de base de données SQL Azure de base de données élastique](sql-database-elastic-query-overview.md). 

## <a name="prerequisites"></a>Composants requis

Vous devez posséder l’autorisation ALTER ANY EXTERNAL DATA SOURCE. Cette autorisation est incluse avec l’autorisation ALTER DATABASE hello. Les autorisations ALTER ANY EXTERNAL DATA SOURCE sont toohello nécessaires toorefer source de données sous-jacente.

## <a name="create-hello-sample-databases"></a>Créer des bases de données exemple hello
toostart avec, nous devons toocreate deux bases de données, **clients** et **commandes**, soit dans hello identiques ou différents serveurs logiques.   

Exécutez hello suivant des requêtes de hello **commandes** hello toocreate de base de données **OrderInformation** table et entrée hello exemples de données. 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

Maintenant, exécutez la requête sur hello suivante **clients** hello toocreate de base de données **CustomerInformation** table et entrée hello exemples de données. 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a>Créez des objets de base de données
### <a name="database-scoped-master-key-and-credentials"></a>Clé principale et informations d’identification de la base de données
1. Ouvrez SQL Server Management Studio ou SQL Server Data Tools dans Visual Studio.
2. Connecter la base de données des commandes toohello et exécuter hello suivant de commandes T-SQL :
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    Hello « username » et « password » doivent être nom d’utilisateur hello et mot de passe utilisé toologin dans la base de données des clients hello.
    L’authentification à l’aide d’Azure Active Directory avec des requêtes élastiques n’est pas prise en charge actuellement.

### <a name="external-data-sources"></a>Sources de données externes
toocreate source de données externe, exécutez hello suivant de commande de base de données des commandes hello : 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a>Tables externes
Créer une table externe sur base de données des commandes hello qui correspond à la définition de hello de table de CustomerInformation hello :

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Exécutez un exemple de requête T-SQL de base de données élastique
Une fois que vous avez défini votre source de données externe et de vos tables externes, vous pouvez maintenant utiliser T-SQL tooquery vos tables externes. Exécutez cette requête sur la base de données des commandes hello : 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a>Coût
Actuellement, fonctionnalité de requête de base de données élastique hello est incluse dans le coût de hello de votre base de données SQL Azure.  

Pour plus d’informations sur la tarification, voir [Tarification des bases de données SQL](https://azure.microsoft.com/pricing/details/sql-database). 

## <a name="next-steps"></a>Étapes suivantes

* Pour une présentation des requêtes élastiques, consultez [Présentation des requêtes élastiques](sql-database-elastic-query-overview.md).
* Pour la syntaxe et des exemples de requêtes pour des données partitionnées verticalement, consultez [Requêtes sur des données partitionnées verticalement](sql-database-elastic-query-vertical-partitioning.md)
* Pour commencer le didacticiel sur le partitionnement horizontal (sharding), consultez [Prise en main des requêtes élastiques pour le partitionnement horizontal (sharding)](sql-database-elastic-query-getting-started.md).
* Pour la syntaxe et des exemples de requêtes pour des données partitionnées horizontalement, consultez [Requêtes sur des données partitionnées horizontalement](sql-database-elastic-query-horizontal-partitioning.md)
* Consultez [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) pour une procédure stockée qui exécute une instruction Transact-SQL sur une seule base de données Azure SQL distante ou un ensemble de bases de données servant de partitions dans un schéma de partitionnement horizontal.