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
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a>Interroger des bases de données cloud de schémas différents (version préliminaire)
![Requête sur plusieurs tables dans des bases de données différentes][1]

Les bases de données partitionnées verticalement utilisent différents ensembles de tables sur différentes bases de données. Cela signifie que ce schéma hello est différent sur les différentes bases de données. Par exemple, toutes les tables d’inventaire se trouvent sur une base de données alors que toutes les tables liées à la comptabilité se trouvent dans une seconde base de données. 

## <a name="prerequisites"></a>Composants requis
* utilisateur de Hello doit posséder les autorisations ALTER ANY EXTERNAL DATA SOURCE. Cette autorisation est incluse avec l’autorisation ALTER DATABASE hello.
* Les autorisations ALTER ANY EXTERNAL DATA SOURCE sont toohello nécessaires toorefer source de données sous-jacente.

## <a name="overview"></a>Vue d'ensemble

> [!NOTE]
> À la différence avec le partitionnement horizontal, ces instructions DDL ne dépendent pas définir un niveau de données avec une carte de partitions via la bibliothèque cliente de base de données élastique hello.
>

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CREATE EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a>Créer la clé principale et les informations d’identification de la base de données
informations d’identification Hello sont utilisée par hello requête élastique tooconnect tooyour bases de données distantes.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Vérifiez que hello `<username>` ne comprend aucun **»@servername»** suffixe. 
>

## <a name="create-external-data-sources"></a>Créer des sources de données externes
Syntaxe :

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> paramètre de TYPE Hello doit être défini trop**SGBDR**. 
>

### <a name="example"></a>Exemple
Hello exemple suivant illustre utilisation hello Hello instruction de création de sources de données externes. 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

liste de hello tooretrieve de sources de données externes en cours : 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a>Tables externes
Syntaxe :

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a>Exemple
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

Bonjour à l’exemple suivant montre comment tooretrieve hello la liste des tables externes à partir de la base de données actuelle hello : 

    select * from sys.external_tables; 

### <a name="remarks"></a>Remarques
Requête élastique étend hello table externe syntaxe toodefine externe tables existantes qui utilisent des sources de données externes de type SGBDR. Une définition de la table externe pour le partitionnement vertical couvre hello suivant aspects : 

* **Schéma**: une table externe hello DDL définit un schéma qui permettent de vos requêtes. schéma de Hello fourni dans votre définition de table externe requiert un schéma de hello toomatch de tables hello dans la base de données distante hello où sont stockées les données réelles hello. 
* **Référence de base de données distante**: une table externe hello DDL fait référence la source de données externe tooan. source de données externe Hello Spécifie le nom du serveur logique hello et le nom de la base de données de base de données distante hello où sont stockées les données de la table réelle hello. 

Les tables externes hello syntaxe toocreate à l’aide de source de données externe comme indiqué dans la section précédente de hello, est la suivante : 

clause DATA_SOURCE Hello définit la source de données externe hello (c'est-à-dire hello à distance de base de données en cas de partitionnement vertical) qui est utilisé pour une table externe hello.  

les clauses nom_schéma et nom_objet Hello fournissent hello capacité toomap hello table externe définition tooa table dans un schéma différent sur la base de données distante hello ou table tooa avec un nom différent, respectivement. Cela est utile si vous souhaitez que toodefine une vue de catalogue tooa table externe ou d’une vue de gestion dynamique sur votre base de données à distance - ou toute autre situation où nom de la table distante hello est déjà exécutée localement.  

Hello instruction DDL suivante supprime une définition existante de la table externe à partir du catalogue local d’hello. Il n’affecte pas la base de données distante hello. 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

**Autorisations pour la TABLE externe de CREATE/DROP**: les autorisations ALTER ANY EXTERNAL DATA SOURCE sont nécessaires pour la table externe DDL qui est également nécessaire de source de données sous-jacente toorefer toohello.  

## <a name="security-considerations"></a>Considérations relatives à la sécurité
Les utilisateurs avec une table externe accès toohello automatiquement accéder toohello les tables distantes sous-jacentes sous les informations d’identification hello donné dans la définition de source de données externe hello. Vous devez gérer avec soin de table externe de toohello accès dans l’ordre tooavoid indésirables d’élever les privilèges via les informations d’identification hello hello externe de source de données. Les autorisations SQL régulières peuvent être tooGRANT utilisé ou une table externe de RÉVOQUER l’accès tooan comme s’il s’agissait d’une table normale.  

## <a name="example-querying-vertically-partitioned-databases"></a>Exemple : interrogation de bases de données partitionnées verticalement
Hello requête suivante effectue une jointure tridirectionnelle entre deux tables locales hello pour les commandes et les lignes de commande et de la table distante de hello pour les clients. Il s’agit d’un exemple de cas d’utilisation de données d’hello référence de requête élastique : 

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


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>Procédure stockée pour l’exécution de T-SQL à distance : sp\_execute_remote
Requête élastique présente également une procédure stockée qui offre un accès direct toohello partitions. Hello procédure stockée est appelée [sp\_exécuter \_distant](https://msdn.microsoft.com/library/mt703714) et peut être utilisé tooexecute des procédures stockées distantes ou le code T-SQL sur des bases de données distantes hello. Il prend hello paramètres suivants : 

* Nom de source de données (nvarchar) : nom hello hello externe de source de données de type SGBDR. 
* Requête (nvarchar) : hello T-SQL toobe de requête exécutée sur chaque partition. 
* Déclaration de paramètre (nvarchar) - facultatif : chaîne avec les définitions de type de données pour les paramètres de hello utilisés dans le paramètre de requête hello (comme sp_executesql). 
* Liste de valeurs de paramètre : facultative : valeurs de paramètre de liste séparées par des virgules (par exemple, sp_executesql).

Hello sp\_exécuter\_distant utilise hello prévue hello appel paramètres tooexecute hello donné l’instruction T-SQL sur des bases de données distantes hello de source de données externe. Elle utilise les informations d’identification hello de hello données externes tooconnect toohello shardmap manager base de données source et de bases de données distantes hello.  

Exemple : 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a>Connectivité des outils
Vous pouvez utiliser tooconnect de chaînes de connexion SQL Server standard votre toodatabases d’outils de l’intégration BI et les données sur serveur de base de données SQL hello qui a activé de requête élastique et des tables externes définies. Assurez-vous que SQL Server est pris en charge comme source de données pour votre outil. Faites ensuite référence toohello de requêtes élastique de base de données et ses tables externes comme toute autre base de données de SQL Server que vous devez vous connecter toowith votre outil. 

## <a name="best-practices"></a>Meilleures pratiques
* Vérifiez la que base de données access toohello à distance en activant l’accès pour les Services Azure dans sa configuration de pare-feu de base de données SQL a été donné à cette base de données de point de terminaison de la requête élastique hello. Vérifiez également ces informations d’identification hello fourni dans les données externes hello définition de la source peut se connecter à la base de données distante hello et a la table distante de hello autorisations tooaccess hello.  
* Requête élastique mieux adaptée pour les requêtes où la plupart des calculs de hello peut être effectuée sur les bases de données distantes hello. Vous obtenez généralement de meilleures performances des requêtes hello avec des prédicats de filtre sélectif qui peut être évaluée sur les bases de données distantes hello ou des jointures qui peuvent être effectuées complètement sur la base de données distante hello. Autres modèles de requête peuvent nécessiter des tooload grandes quantités de données à partir de la base de données distante hello et peuvent être lent. 

## <a name="next-steps"></a>Étapes suivantes

* Pour une présentation des requêtes élastiques, consultez [Présentation des requêtes élastiques](sql-database-elastic-query-overview.md).
* Pour le didacticiel sur le partitionnement vertical, consultez [Prise en main des requêtes de bases de données croisées (partitionnement vertical)](sql-database-elastic-query-getting-started-vertical.md).
* Pour commencer le didacticiel sur le partitionnement horizontal (sharding), consultez [Prise en main des requêtes élastiques pour le partitionnement horizontal (sharding)](sql-database-elastic-query-getting-started.md).
* Pour la syntaxe et des exemples de requêtes pour des données partitionnées horizontalement, consultez [Requêtes sur des données partitionnées horizontalement](sql-database-elastic-query-horizontal-partitioning.md)
* Consultez [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) pour une procédure stockée qui exécute une instruction Transact-SQL sur une seule base de données Azure SQL distante ou un ensemble de bases de données servant de partitions dans un schéma de partitionnement horizontal.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
